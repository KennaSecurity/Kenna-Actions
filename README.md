
# GitHub Action for Kenna Toolkit

This is a GitHub Action for invoking the [Kenna Toolkit](https://github.com/KennaPublicSamples/toolkit) and uploading data  APIs to Kenna.

## Example Workflows

We will add more example workflows to this section as they are tested and verified.

### AWS Inspector

As configured this action will run every hour, and upload data to the [Kenna API](https://apidocs.kennasecurity.com/reference) from the [AWS Inspector](https://aws.amazon.com/inspector/) run inside your AWS environment.

For this example, you will need to configure [encrypted secrets](https://docs.github.com/en/free-pro-team@latest/actions/reference/encrypted-secrets ) in your repository for the following variables:

- aws_access_key
- aws_secret_key
- kenna_api_key

```yaml

name: Inspector-Action

on:
  schedule:
    - cron: "0 0 * * *"
  
jobs:
   Kenna-Action:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout Toolkit Repo
      uses: actions/checkout@v2
      with:
        repository: KennaPublicSamples/toolkit
    - name: Set up Ruby
      uses: ruby/setup-ruby@v1
      with:
        ruby-version: 2.6
    - name: Install dependencies
      run: bundle install --without development test
    - name:  Run Toolkit
      run : exec bundle exec ruby toolkit.rb  task=aws_inspector aws_access_key=${aws_access_key} aws_secret_key=${aws_secret_key} kenna_api_host=api.kennasecurity.com kenna_connector_id=156863 kenna_api_key=${kenna_api_key} -v
      env:
        aws_access_key: "${{secrets.aws_access_key}}"
        aws_secret_key=: "${{secrets.aws_secret_key}}"
        kenna_api_key=: "${{secrets.kenna_api_key}}"
```

For demonstration purposes, this example runs in this repo hourly.

![Kenna-Inspector-Action](https://github.com/KennaPublicSamples/Kenna-Action/workflows/Kenna-Action/badge.svg)

### Security Scorecard

As configured this action will run every hour, and upload data to the [Kenna API](https://apidocs.kennasecurity.com/reference) from [Security Scorecard](https://www.securityscorecard.com/).

For this example, you will need to configure [encrypted secrets](https://docs.github.com/en/free-pro-team@latest/actions/reference/encrypted-secrets ) in your repository for the following variables:

- aws_access_key
- aws_secret_key
- kenna_api_key

```yaml

name: Security-Scorecard-Action

on:
  schedule:
    - cron: "0 * * * *"
    # Schedule Configuration From Github Actions. 
    # https://docs.github.com/en/free-pro-team@latest/actions/reference/events-that-trigger-workflows#scheduled-events
  
jobs:
   Kenna-Action:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout Toolkit Repo
      uses: actions/checkout@v2
      with:
        repository: KennaPublicSamples/toolkit
    - name: Set up Ruby
      uses: ruby/setup-ruby@v1
      with:
        ruby-version: 2.6
    - name: Install dependencies
      run: bundle install --without development test
    - name:  Run Toolkit
      run : exec bundle exec ruby toolkit.rb task=security_scorecard ssc_api_key=${SSC_API_KEY} kenna_api_host=api.us.kennasecurity.com kenna_connector_id=164377 kenna_api_key=${kenna_api_key} -v
      env:
        SSC_API_KEY=: "${{secrets.SSC_API_KEY}}"
        kenna_api_key=: "${{secrets.kenna_api_key}}"
```

### Important Considrations

While this repository is public to demo the action, we strongly suggest you run this in a [private repository](https://docs.github.com/en/free-pro-team@latest/github/administering-a-repository/setting-repository-visibility) to stop publicly exposing the logs which may contain hostnames and vulnerability data.

## More Information

For documentation on the Kenna Toolkit itself, including other output capabilities, see the [Kenna Toolkit](https://github.com/KennaPublicSamples/toolkit).
