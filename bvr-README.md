# Running cml application 

Clone given repository or create the project files 
```
git clone https://github.com/iterative-test/cml-example-base.git

```

Create folders 

```
mkdir .github
mkdir .github\workflows

```

Create ci-cd.yaml inside .github\workflows

```
name: model-training
on: [push]
jobs:
  run:
    runs-on: ubuntu-latest
    permissions:
      contents: write
      pull-requests: write
      repository-projects: write
    container : docker://ghcr.io/iterative/cml:0-dvc2-base1
    steps:
      - uses: actions/checkout@v3
      - name: Train model
        env:
          repo_token : ${{ secrets.GITHUB_TOKEN }}
        run: |
          pip install -r requirements.txt
          python train.py

          cat metrics.txt >> report.md

          echo "![](./plot.png)" >> report.md
          cml comment create report.md 


```

Change permissions in github repo properties 

```


    Go to repository "Settings".
    After that it will show you a left pane where you will find "Actions"
    Expand "Actions" tab
    Click on "General" under options tab.
    Now on new page scroll down and you will fine "Workflow Permissions"
    Select "Read and Write" under "Workflow Permissions".


```


Commit the changes automatically flow will be started 

```

git add .
git commit -m "first commit"
git push -u origin main

```



```
view under Actions tab 
```



