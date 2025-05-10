# Привет, я [Твой ник]! 👋  

🚀 Пишу код на `Python` / `JavaScript`.  
🎯 Люблю open-source, автоматизацию и кофе.  

📊 **Моя статистика:**  
[![GitHub stats](https://github-readme-stats.vercel.app/api?nousway=nousway&show_icons=true&theme=radical)](https://github.com/nousway)  

📫 **Как связаться:**  
[![Telegram](https://img.shields.io/badge/-Telegram-26A5E4?logo=telegram)](https://t.me/tsm_ai)  

# .github/workflows/update-readme.yml
name: Update README
on:
  schedule:
    - cron: '0 0 * * *'  # Раз в день
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - run: echo "Обновлено: $(date)" >> README.md
      - uses: actions/github-script@v5
        with:
          script: |
            github.rest.repos.update({
              owner: context.repo.owner,
              repo: context.repo.repo,
              message: "Auto-update README",
              content: Buffer.from(require('fs').readFileSync('README.md')).toString('base64')
            })
