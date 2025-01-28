name: Update README with Blog Posts

on:
  schedule:
    - cron: '0 */6 * * *'
  workflow_dispatch:

jobs:
  update:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

      - name: Fetch blog posts
        run: |
          echo "### Latest Blog Posts" > README.md
          curl -s https://example.com/rss | grep -E '<title>|link' | sed -e 's/<title>//g' -e 's/<\/title>//g' -e 's/<link>//g' -e 's/<\/link>//g' >> README.md

      - name: Commit and push changes
        run: |
          git config --global user.name "Your Name"
          git config --global user.email "your-email@example.com"
          git add README.md
          git commit -m "Updated README with latest blog posts"
          git push
