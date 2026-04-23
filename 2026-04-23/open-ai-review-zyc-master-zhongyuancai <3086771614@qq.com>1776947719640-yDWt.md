根据提供的Git diff记录，以下是对于代码变更的评审：

### `.github/workflows/main-maven-jar.yml` 文件变更：

1. **分支变更**：
   - 从`master`分支变更为`master-close`分支。
   - 这意味着工作流将仅在特定的`master-close`分支上触发，而不是所有的`master`分支的push或pull request。需要确认这种变更的意图和原因。

2. **评审**：
   - 如果`master-close`分支是特定的里程碑或稳定的分支，这个变更是有意义的。
   - 如果所有`master`分支的push和pull request都应该触发这个工作流，那么这个变更可能是一个错误，应该回滚到`master`分支。

### `.github/workflows/main-remote-jar.yml` 文件新增：

1. **工作流描述**：
   - 新增的工作流名为`Build and Run OpenAiCodeReview By Main Remote Jar`，它似乎是为了构建和运行远程JAR文件而设计的。

2. **步骤分析**：
   - 使用`actions/checkout@v2`来检出代码。
   - 设置JDK 11环境。
   - 创建一个`libs`目录用于存放依赖的JAR文件。
   - 下载特定的`openai-code-review-sdk-1.0.jar`文件。
   - 获取仓库、分支、提交作者和提交信息。
   - 运行`openai-code-review-sdk-1.0.jar`并传递环境变量以配置不同的服务（如GitHub、微信、OpenAi - ChatGLM）。

3. **评审**：
   - 工作流的结构合理，步骤清晰。
   - 确保所有的`secrets`（如`CODE_REVIEW_LOG_URI`、`CODE_TOKEN`等）在GitHub仓库中已经安全地配置。
   - 使用`wget`下载JAR文件可能需要检查是否有权限或更稳定的下载方法。
   - 确保环境变量设置正确，以避免任何配置错误。
   - 运行`openai-code-review-sdk-1.0.jar`之前，确保该JAR文件包含所有必要的运行时依赖。
   - 考虑到工作流可能会执行一些敏感操作，可能需要增加日志记录来帮助调试和审计。

### 总结：

- 变更似乎是针对特定需求进行的，需要确认这些变更是否满足实际业务需求。
- 新增的工作流提供了详细的构建和运行步骤，但需要确保所有配置和环境变量都是正确的。
- 代码变更应该经过充分的测试以确保工作流的稳定性和安全性。