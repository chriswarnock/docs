---
id: contributing_to_milvus.md
---

# Milvus 贡献指南

这里是 Milvus 项目贡献指南，如果你在参与 Milvus 的贡献中遇到了问题，请 [创建一个 Issue](https://github.com/milvus-io/community/issues/new) 反馈给我们。



## 交流

我们的交流平台如下：

-   [GitHub Issues](https://github.com/milvus-io/milvus/issues)：用于记录 Milvus 项目的功能和 BUG，与之有关的内容都可以在 Issue 下讨论
-   [Milvus Technical-Discuss 邮件列表](https://lists.lfaidata.foundation/g/milvus-technical-discuss)：用于 Milvus 项目的技术讨论，这里有所有的技术讨论
-   [Slack Channels](https://join.slack.com/t/milvusio/shared_invite/zt-e0u4qu3k-bI2GDNys3ZqX1YCJ9OM~GQ)：实时交流的平台



## GitHub flow

为了能够更好地进行多人的协作，我们约定在 Milvus 项目上以 [GitHub flow](https://docs.github.com/en/get-started/quickstart/github-flow) 的方式修改和提交内容。简单的说，以分支的方式面向主分支开发。当你要做任何修改的时候，先从主分支创建出一个分支，修改提交后在 GitHub 上创建合并请求，通过合并请求将代码集成到 Milvus 的主分支上。



## 创建合并请求（Pull Request）

在 GitHub 上，代码的合并是通过创建 Pull Request（一般简称为 PR）实现的，流程上与 GitHub 上标准的 PR 流程无异。在这个基础上，Milvus 项目还集成了一个 prow 机器人，用于帮助 PR 流程的运转。

只要你创建过 PR，你就会在 GitHub 上见过这个机器人，它会自动地给你的 PR 设置标签和 Reviewer。除了设置标签和 Reviewer，你还可以通过在评论里使用一些命令来做更多事情，命令请参阅 [命令参考文档](https://prow.zilliz.cc/command-help) 。

新贡献者 PR 中常遇到的问题：

-   DCO检查失败，请参考 [DCO页面](https://github.com/apps/dco) 以解决问题
-   测试运行失败，若与你的修改无关，通过 re-run 以解决问题
-   在 git commit message 中包含@（如@person）或者可以关闭 Issue 的[关键字](https://help.github.com/en/articles/closing-issues-using-keywords)（例如 fixes #xxxx）



## 代码审查（Code Review）

代码审查是 PR 的一个必经步骤，目的是保证代码背后的想法是合理的，并且修改是正确且完整的。

为了让你的 PR 更快地被接收，你需要：

-   代码风格遵循 Effictive Go，参考：https://golang.org/doc/effective_go
-   编写良好的 commit message，参考：https://chris.beams.io/posts/git-commit
-   将大的修改分解成一系列小的修改，每个小的修改解决一小部分问题从而在总体上来解决更大的问题
-   给 PR 加上合适的标签

注意：如果你的 PR 没有得到及时的回复，你可以在 Slack 上的 [#pr-reviews](https://milvusio.slack.com/messages/pr-reviews) 频道来寻找 Reviewer。



## 最佳实践

-   编写清晰且有意义的 git commit message。
-   如果 PR 将“完全”修复某一个 Issue，请在创建 PR 时将 `fixes #123` 加入 PR 正文中（其中 123 是 PR 将修复的 Issue 编号，这将在 PR 合并时自动关闭该问题）。
-   确保你的 git commit message 中没有包含 `@mentions` 或 `fixes` 关键字，这些应该包含在 PR 正文中。
-   请压缩（squash）你的提交，以便我们可以维护更清晰的 git 历史记录。
-   确保 PR 包含清晰详细的描述，解释更改的原因，让 Reviewer 了解你的 PR。



## 测试

贡献者需要确保提交的代码通过测试，如果遇到了问题，可以在 GitHub 评论中 @milvus-io/sig-testing 获得帮助。

Milvus 中包含多种测试，不同类型的测试用例的测试目标也不一样：

-   单元测试：用于验证某一个单元的功能按照预期运行。通过在 Golang 文件中导入 testing 这个包来进行单元测试。每一个 PR 都需要通过所有的单元测试，才能够被合并进入主分支。单元测试代码在每个 Golang 文件旁，例如：`milvus/internal/allocator/global_id.go` 中的函数将在 `milvus/internal/allocator/global_id_test.go` 中进行测试。
-   集成测试：关键的功能测试，旨在保证 PR 一定程度正确性的情况下能够更快地被合并到主分支上。这部分测试使用 Python 编写，存储在 `milvus/tests/python_test` 和 `milvus/tests20/python_client` 目录下，可通过 `pytest --tags=smoke .` 运行。
-   端到端测试：完整的功能性测试用例。这部分测试使用 Python 编写，存储在 `milvus/tests/python_test` 和 `milvus/tests20/python_client` 目录下，可通过 `pytest .` 运行。

CI 将会在 PR 上运行单元测试和集成测试，结果会更新在 GitHub Pull Request Status 上，任何测试的失败都会导致代码无法合并进入主分支。



## 问题管理或分类

你可能会注意到 Milvus 仓库有很多未解决的 Issue，帮助管理或分类这些未解决的问题可能是一项巨大的贡献，也是了解项目各个领域的绝佳机会。我们使用各类的 Label 来标记 Issue，从而更快地让合适的人看到。