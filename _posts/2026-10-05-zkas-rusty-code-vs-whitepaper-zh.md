---
layout: post
title: "信任,但要读代码:zkas-rusty 对照自家白皮书"
date: 2026-10-05 10:30:00 +0000
categories: [cryptocurrency, proof-of-work, zkas]
lang: zh
---

白皮书是承诺,代码库才是真相。上周我们介绍了 ZKas 纸面上的设计——Kaspa 的 BlockDAG 之上的 Orchard 隐私、turnstile 不变量、可验证的公平启动。这周我们做了件不那么光鲜的事:把 [zkas-rusty](https://github.com/firecash/zkas-rusty) 克隆下来,逐条核对代码是否兑现了纸上的承诺。简短的答案是:兑现了,而且诚实得反常——而最有意思的部分,恰恰是代码与论文礼貌地不一致的地方。

---

**心脏是真的,而且有测试。** 白皮书中唯一真正的新组件——搭 GHOSTDAG 接受顺序便车的屏蔽状态转换——位于 `shielded-core/src/state.rs`,文件头的文档注释几乎逐字复述了论文里的五个步骤:解决 nullifier 冲突(先到先得)、插入幸存者、把该区块的子树追加到全局树、检查 turnstile、发布锚点。更妙的是,这套算法被刻意保持*纯粹*——不依赖 rocksdb 和共识管线——专门为了让那个"成败攸关"的确定性属性可以被单元测试。而它确实被测了:测试套件包含并行双花测试(两个区块花费同一张票据,恰有一笔存活,每个节点推出相同锚点)、turnstile 超支拒绝,以及跨多个区块的手续费重铸检查。论文宣称"在算法层和共识层都经过测试验证",这不是套话,它就在那儿。

**创世块逐字节可查。** 论文要求你不凭信任去验证的一切,都在 `consensus/core/src/config/genesis.rs` 里:难度 bits `0x1b02d093`(从第一个区块起就是约 50 TH/s 的真实目标)、coinbase 补贴 `0x05f5e100`——1 亿 sompi,恰好 1 ZKAS——支付给一个仅含 `0x00` 即 OP_FALSE 的脚本,证明无法花费;以及 ASCII 锚记 `zkas-mainnet btc#959713` 和对应的 Bitcoin 区块哈希。在这里,"无预挖"不是一句口号,而是一个你能 grep 到的常量。

**锚点、合并挖矿、发行——全都在。** 锚点规则(只能针对成熟期内的锚点花费,窗口为 `[shielded_anchor_depth, max_shielded_anchor_age]`,且其来源区块必须是选定链上的规范祖先)在 virtual processor 中强制执行,并由一组把"成熟"与"规范"拆开单独测试的扎实测试组来检验。合并挖矿是实打实的管线:consensus-core 里的 `AuxPow` 类型、原生与辅助区块头的双重接纳、经 borsh 编码穿过 p2p 层并附往返测试。发行同样吻合:`deflationary_phase_daa_score = 0`(衰减自创世即开始,没有平台期)、以每笔补贴的千分之五十定义的开发费,以及 `coinbase.rs` 里的三个月半衰期。Halo 2 批量验证也如宣传所言,在 `shielded-core/src/verify.rs` 中通过 Orchard 的 `BatchValidator` 实现。

---

**接下来是缺点——因为诚实的评测不能省略这部分。**

- **这个仓库有前科,哦不,前身。** 整个项目从 "FireCash" 改名而来,而过去不断渗出来:挖矿诊断文档仍写着 "FireCash targets 10 blocks/sec",辅助脚本引用 `/root/firecash/wallets`,crate 名字也带着历史。虽然只是表面问题,但它让审计变复杂——你得不停在同一条网络的两个名字之间翻译,而且过时的文档说 10 BPS,论文却说 1 BPS。
- **运维杂物会告密。** 仓库根目录躺着 `reap.py`(2026 年 9 月一次钱包恢复事故后清理孤立扫描备份的脚本)、`restore_baks.py`,以及一个 385 行的 `zkas-anchor-pins.tsv`,标注着"已过时——勿应用,仅作取证记录"。值得称赞的是,他们把这些取证材料公开保留而没有删除。但这也证实:这条年轻的链已经经历过至少一次需要手工手术的钱包状态事故——白皮书对此自然只字未提。
- **一个自己坦白了的性能 bug。** 工作区的 `Cargo.toml` 里有一段懊恼的自白:密码学 crate 移植并改名为 `zakura-*`(orchard、halo2、pasta curves)时,release 配置里的性能覆盖项沿用旧包名,于是"悄悄地不再匹配任何包"——结果是所有曲线和证明 crate 都开着溢出检查编译,恰好拖累了那些覆盖项本想加速的热点运算。这段注释诚实得可爱;但这个 bug 也实实在在地烧了好几个星期的钱包 CPU。还有一点:整套密码学栈是改了名的分叉,这切断了与上游经审计 crate 的直观 diff——可以理解(总得有人打上 2026 年 Orchard 漏洞的补丁),但它让独立验证变难了,而不是变容易。
- **休眠的接缝。** 桥接与销毁机制——peg-out、退出凭证、扩展了 `pegged_in` 和 `burns` 项的 turnstile——写好了,测过了,然后被 `BRIDGE_ENABLED = false` 的开关锁住,外加纵深防御,即便某个 burn 侥幸抵达状态转换也会被拒绝。这是发布半成品功能的正确姿势,但半成品终究是半成品。

---

**结论。** 印象最深的是注释文化:代码不只陈述*是什么*,还会论证*为什么*——为什么负的 value balance 必须在提取阶段拒绝,为什么退出 nullifier 可以继承双花防护,为什么一个 profile 覆盖项会失效。这是预期会被审计、并打算扛过审计的工程师的笔调。白皮书的核心主张——状态转换、turnstile、创世、发行——全部在代码树里,忠实且有测试。差距在边缘地带:一套需要自己审计轨迹的改名依赖栈、在两个品牌名和两个区块速率之间漂移的文档,以及一条已经挨过几拳的主网留下的化石记录。而对一条三个月大的链来说,这终究是你能要求的最健康的组合:一份说真话的论文,和一套承认自己何时没说真话的代码。

*来源:[GitHub 上的 zkas-rusty](https://github.com/firecash/zkas-rusty)、[ZKas 白皮书](https://zkas.info/whitepaper.html)*
