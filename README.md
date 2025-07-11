# lsp
how to basically use Claude

一、基础命令
1.claude  --启动交互模式
<img width="159" height="216" alt="image" src="https://github.com/user-attachments/assets/a924007f-bdf0-4ac7-84c7-e7b654376974" />


2.claude “需求”  --无需进入交互模式，直接启用
举例：clude “帮我写一个系统监控脚本”
<img width="200" height="220" alt="image" src="https://github.com/user-attachments/assets/e3de7349-a218-4ade-b761-bc710fbcd244" />


3.cat ....py ｜ claude "解释" 管道处理，直接处理文件内容
举例：cat utils.py | claude -p "explain in chinese" 
<img width="205" height="157" alt="image" src="https://github.com/user-attachments/assets/97284596-eee3-473d-8c91-a2cb25925633" />
tips：utils.py是我自己创建的，"-p"会显示纯文本（可不用）


4。git diff | claude "..."   --总结自己的改动
举例：git diff | claude "解释这次改动"   --总结自己的改动
<img width="432" height="12" alt="image" src="https://github.com/user-attachments/assets/99a448bf-2e40-4b0a-b77e-17d8c0b160ec" />

5. claude -p “…（需求）” > query.sql
举例：claude -p “生成MySQL的SQL的JOIN语句案例” > query.sql
<img width="366" height="46" alt="image" src="https://github.com/user-attachments/assets/f6470b67-3ddc-4743-a368-91ccbfda6d6c" />
cat query.sql  --查看刚才的案例
<img width="432" height="28" alt="image" src="https://github.com/user-attachments/assets/8bd195f8-fa6f-4649-bdcb-ae97e3436db3" />
 tips:query.sql的意思是运行完就退出交互模式
对比：claude "生成MySQL的SQL的JOIN语句案例" > query.sql   
cat query.sql
<img width="179" height="41" alt="image" src="https://github.com/user-attachments/assets/391e0e7e-0777-47fe-9e7c-5174067a4ab4" />

6.claude –help   --查看帮助
<img width="432" height="14" alt="image" src="https://github.com/user-attachments/assets/9b100aaa-b56c-4608-a629-0d062812411a" />

二、配置管理
cladue config list   --显示当前使用的模型、API密钥等信息。
<img width="432" height="30" alt="image" src="https://github.com/user-attachments/assets/a7da4e50-d193-482f-abff-be8ec78b29d6" />

三、MCP命令
1. claude mcp list  --查看 MCP列表
<img width="432" height="28" alt="image" src="https://github.com/user-attachments/assets/903cef2f-0c61-4e9e-8430-cbb5427c2e6e" />

2. claude mcp get playwright（需提前安装）   --查看某个 MCP 的详细配置
<img width="432" height="28" alt="image" src="https://github.com/user-attachments/assets/76f02465-14d4-4e3d-add8-3f1ef55d0cf8" />

3. claude mcp remove "playwright" -s user   --删除某个 MCP
<img width="432" height="28" alt="image" src="https://github.com/user-attachments/assets/97950d17-d6a7-40e8-beb6-ae8f047cf8ba" />

4. /mcp  --查看 mcp 状态
<img width="229" height="59" alt="image" src="https://github.com/user-attachments/assets/0563f3b8-23dd-4a79-8c43-37e3a3bed14b" />

5.claude mcp add playwright -s user -- npx @playwright/mcp@latest  --安装 MCP
<img width="432" height="25" alt="image" src="https://github.com/user-attachments/assets/261bc59e-6bd5-4e45-95d2-c930c6e06816" />

四、实战
1.连接 GitHub
（1） 安装 GitHub MCP
claude mcp add github-server -e GITHUB_PERSONAL_ACCESS_TOKEN=YOUR_TOKEN -- npx "@modelcontextprotocol/server-github"（在 GitHub 中给权限）
<img width="165" height="167" alt="image" src="https://github.com/user-attachments/assets/8928bcb3-4c85-40d1-999c-b3c3976f8b81" />
（2）使用  --无需进入 GitHub 可直接看见内容（需要重新加入令牌，改变环境变量）
     brew install gh  --安装 GitHub CLI
     gh auth login   --登入
     gh repo list  --查看仓库
<img width="335" height="63" alt="image" src="https://github.com/user-attachments/assets/61ddedbf-58ed-4b15-9e68-260d79c0518e" />

（3）claude –continue         --持续对话模式
    claude -r     --恢复某次对话

（4）claude -p "生成MySQL的SQL的JOIN语句案例" --output-format json > query.json    --指定输出格式（JSON
（5）创建命令别名
alias cc="claude"
alias ccr="claude 'code review这段代码'"
alias cct="claude '为这段代码写测试'"
cat quicksort.py | ccr  
<img width="344" height="147" alt="image" src="https://github.com/user-attachments/assets/bac59b7c-1658-4b1f-9d1e-180842373a14" />
cat utils.py | cct<img width="432" height="25" alt="image" src="https://github.com/user-attachments/assets/075dc48c-324a-4126-8db4-8fd529bda939" />

（6）claude --dangerously-skip-permissions   --狂飙模式（yolo）
<img width="432" height="26" alt="image" src="https://github.com/user-attachments/assets/d921e8d5-991f-4c5b-8fe1-b7dffeffd3b9" />

2.真实工作流
 （1）Git工作流集成
git diff --staged | claude "检查这些改动是否有问题"   --提交前检查
<img width="432" height="54" alt="image" src="https://github.com/user-attachments/assets/7d3b26e0-c2ca-4e6f-8352-d2aee26d161d" />

（2）git diff --staged | claude "生成符合conventional commits的提交信息"  --生成提交信息
<img width="432" height="26" alt="image" src="https://github.com/user-attachments/assets/8fd3270e-5904-4de0-ad98-4cb0dde21d2b" />

（3）git log master..feature-dev1 --oneline | claude "生成PR描述"  --生成 PR 描述
<img width="432" height="26" alt="image" src="https://github.com/user-attachments/assets/77a5746e-aa21-4328-a8f8-85d4ab756a00" />

（2）自动化文档生成
echo "# API Documentation\n" > API.md
find . -name "*.py" -type f | while read file; do
   echo "\n## $file\n" >> API.md
   cat "$file" | claude -p "提取并文档化所有导出的函数" >> API.md
done
<img width="432" height="104" alt="image" src="https://github.com/user-attachments/assets/4a862933-5641-49e0-b7f3-5d3439a8e279" />

（3）代码质量检查
#!/bin/bash
echo "开始代码质量检查..."
find . -name "*.py" | while read file; do
      complexity=$(cat "$file" | claude -p "评估代码复杂度，只返回数字1-10")
      echo ">>>>>>>> complexity: ${complexity} <<<<<<<<<<"
      if [ "$complexity" -gt 7 ]; then
          echo "⚠️  $file 复杂度过高: $complexity"
          cat "$file" | claude "建议如何降低复杂度"
      fi
done 
<img width="432" height="200" alt="image" src="https://github.com/user-attachments/assets/d71ac7d9-30ff-4ad7-a765-e25f272eccf0" />

sh -x code_eval.sh   --执行评估 <img width="432" height="14" alt="image" src="https://github.com/user-attachments/assets/40ab0354-c3b5-4e4d-a77c-f7a05848c4e9" />

 
 










