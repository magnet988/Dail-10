name: Auto Green

on:
  schedule:
    - cron: '0 0 * * *' # هر روز ساعت ۱۲ شب به وقت گرینویچ اجرا میشه
  workflow_dispatch: # این گزینه بهت اجازه میده خودت هم دستی دکمه اجرا رو بزنی

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Make changes
        run: |
          echo "Last update: $(date)" > update.txt

      - name: Commit and Push changes
        run: |
          git config --local user.email "action@github.com"
          git config --local user.name "GitHub Action"
          git add update.txt
          git commit -m "Auto green commit [skip ci]" || exit 0
          git push
