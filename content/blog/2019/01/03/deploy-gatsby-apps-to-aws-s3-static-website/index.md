---
title: Deploy Gatsby Apps to AWS S3 static website
date: '2019-01-03T22:12:03.284Z'
---

## Setup

<br/>

> Install AWS CLI
<br/>

```bash
curl "https://s3.amazonaws.com/aws-cli/awscli-bundle.zip" -o "awscli-bundle.zip"
unzip awscli-bundle.zip
sudo ./awscli-bundle/install -i /usr/local/aws -b /usr/local/bin/aws
```

<br/>

> Add Script to package.json
<br/>

```javascript
"scripts": {
    ...
    "deploy": "aws s3 sync ./public s3://[Bucket Name] --delete"
}
```

## Manually Deploy App


```bash
npm run deploy
```

## Deploy from Travis CI

<br/>

> Create **.travis.yml** file and add the follow:
<br/>

```yaml
language: node_js

node_js: 'node'

os: osx

before_script:
  - curl "https://s3.amazonaws.com/aws-cli/awscli-bundle.zip" -o "awscli-bundle.zip"
  - unzip awscli-bundle.zip
  - sudo ./awscli-bundle/install -i /usr/local/aws -b /usr/local/bin/aws

script:
  - npm install
  - npm run build
  - npm run deploy
```
