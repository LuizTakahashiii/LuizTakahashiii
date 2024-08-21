# Steps represent a sequence of tasks that will be executed as part of the job
steps:
  - name: Clone repo
    uses: actions/checkout@v3

  - name: Generate the snake files in './dist/'
    uses: Platane/snk@v3
    id: snake-gif
    with:
      github_user_name: ${{ github.repository_owner }}
      outputs: |     
        dist/github-contribution-grid-snake.gif
        dist/github-contribution-grid-snake.svg
    env:
       GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

  - name: Show build status
    run: git status

  - name: Push new files to the output branch
    uses: crazy-max/ghaction-github-pages@v3.1.0
    with:
      target_branch: output
      build_dir: dist
      commit_message: Update snake animations
    env:
      GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
