<div align="center">

<img alt="seekdb logo" src="images/logo.svg" width="360">

</div>

# seekdb

**Write. Search. Fork. 面向 AI Agent 的状态存储。**

seekdb 是一个 MySQL 兼容的数据库，为 Agent 负载而设计：流式写入不拖累并发检索，写时复制的沙箱供探索使用，向量、全文、关系三种检索可以写进同一条 SQL。

本仓库是 **2026 年 OceanBase 数据库大赛 · seekdb 赛道** 的工作分支，上游项目位于 [oceanbase/seekdb](https://github.com/oceanbase/seekdb)。

## 30 秒跑起来

```bash
docker run -d --name seekdb -p 2881:2881 \
  quay.io/oceanbase/seekdb:latest

mysql -h127.0.0.1 -P2881 -uroot
```

```sql
CREATE DATABASE demo;
USE demo;

CREATE TABLE docs (
  id INT PRIMARY KEY,
  title VARCHAR(200),
  body TEXT,
  embedding VECTOR(768)
);

INSERT INTO docs VALUES (1, 'hello', 'the state store for agents', '[0.1,0.2,0.3]');
SELECT id, title FROM docs ORDER BY embedding <-> '[0.1,0.2,0.3]' LIMIT 3;
```

## 有了 seekdb，哪些事情变了

### 边写边搜，P99 不抖

写入只落到 redo log 就返回，索引维护在后台以「增量 HNSW + 快照 HNSW」两级结构异步完成。查询从不等待写入，所以当摄入量涨上去时 p99 依然平稳。

### 写时复制的沙箱

像切换代码分支一样切换数据库。Agent 可以拉一个沙箱去跑高风险负载，跑完直接丢弃，不必复制一份数据。

### 一条 SQL 做完混合检索

向量距离、全文相关度、普通关系谓词进入同一个执行计划，而不是在应用层拼三次请求。

### MySQL 兼容、有事务、可嵌入

标准 MySQL 协议与语法，事务和崩溃恢复齐备，二进制体积可以小到跟应用一起交付。

## 从源码构建

前置条件：C++20 工具链、CMake 3.20+，以及常规构建工具（`gcc`／`clang`、`make` 或 `ninja`）。

```bash
git clone https://github.com/zzh20071105/seekdb-2026-competition.git
cd seekdb-2026-competition

./build.sh          # 构建入口；./build.sh --help 查看全部参数
```

第三方依赖放在 `deps/` 下，由构建脚本拉取。首次构建耗时很长，之后增量构建很快。

回归用例在 `tools/obtest`，单元测试在 `unittest/`，各自的入口见目录内说明。

## 进一步了解

- 上游项目与发布： [oceanbase/seekdb](https://github.com/oceanbase/seekdb)
- 大赛文档： [OceanBase seekdb 赛道](https://oceanbase.yuque.com/org-wiki-obtech-vh7w9r/hc3pio)
- 贡献者与 Agent 的仓库约定： [AGENTS.md](AGENTS.md)
- 代码如何评审： [REVIEW.md](REVIEW.md)

## 贡献者

见 [contributors 图](https://github.com/zzh20071105/seekdb-2026-competition/graphs/contributors)。本分支的比赛工作记录在提交历史与提交给上游的 Pull Request 中。

## 许可证

Apache License 2.0，详见 [LICENSE](LICENSE)。
