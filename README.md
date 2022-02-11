# Sarif to BitBucket

A script to pipe sarif to BitBucket reports

## Getting Started 

Install:

`npm i -g sarif-to-bb`

BitBucket Configuration:

Create Repository Variables `BB_USER` and `BB_APP_PASSWORD` corresponding to a username / app password with BitBucket API access

## Usage in BitBucket Pipeline

```
image: atlassian/default-image:3

pipelines:
  pull-requests:
    '**': # any source branch 
      - step:
          name: Run Sarif to BitBucket 
          script:
            - npm i -g sarif-to-bb
            - npm i -g snyk
            - snyk test --sarif | npx sarif-to-bb --user $BB_USER --password $BB_APP_PASSWORD --repo $BITBUCKET_REPO_SLUG --commit $BITBUCKET_COMMIT --workspace $BITBUCKET_WORKSPACE
            - snyk code test --sarif | npx sarif-to-bb --user $BB_USER --password $BB_APP_PASSWORD --repo $BITBUCKET_REPO_SLUG --commit $BITBUCKET_COMMIT --workspace $BITBUCKET_WORKSPACE
```

## Sample Snyk Open Source Report

<img width="650" src="https://raw.githubusercontent.com/dylansnyk/sarif-to-bitbucket/cacde4869575e3b67527670e247f677a7064a7f2/assets/snyk-open-source-sample-report.png">

## Sample Snyk Code Report

<img width="650" src="https://raw.githubusercontent.com/dylansnyk/sarif-to-bitbucket/cacde4869575e3b67527670e247f677a7064a7f2/assets/snyk-code-sample-report.png">
