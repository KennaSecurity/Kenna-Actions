
# GitHub Action for Kenna Toolkit

This is a GitHub Action for invoking the [Kenna Toolkit](https://github.com/KennaPublicSamples/toolkit) and uploading data  APIs to Kenna.

## Example Workflows

We will add more example workflows to this section as they are tested and verified.

## AWS GurardDuty

This example action will run every hour, and upload data to the [Kenna API](https://apidocs.kennasecurity.com/reference) from the [AWS GuardDuty][(https://aws.amazon.com/inspector/](https://aws.amazon.com/guardduty/)) run inside your AWS environment.

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
      run : exec bundle exec ruby toolkit.rb  task=aws_guardduty aws_access_key=${aws_access_key} aws_secret_key=${aws_secret_key} kenna_api_host=api.kennasecurity.com kenna_connector_id=156863 kenna_api_key=${kenna_api_key} -v
      env:
        aws_access_key: "${{secrets.aws_access_key}}"
        aws_secret_key=: "${{secrets.aws_secret_key}}"
        kenna_api_key=: "${{secrets.kenna_api_key}}"
```

## AWS Inspector

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

## BitSight

As configured this action will run every hour, and upload data to the [Kenna API](https://apidocs.kennasecurity.com/reference) from [BitSight](https://www.bitsight.com/).

For this example, you will need to configure [encrypted secrets](https://docs.github.com/en/free-pro-team@latest/actions/reference/encrypted-secrets ) in your repository for the following variables:

- snyk_api_secret
- kenna_api_key

```yaml
name: Bitsight-Action

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
      run : exec bundle exec ruby toolkit.rb task=bitsight bitsight_api_key=${secrets.bitsight_api_key} kenna_api_host=api.us.kennasecurity.com kenna_connector_id=164377 kenna_api_key=${kenna_api_key} -v
      env:
        bitsight_api_key=: "${{secrets.bitsight_api_key}}"
        kenna_api_key=: "${{secrets.kenna_api_key}}"
```

## Expanse

As configured this action will run every hour, and upload data to the [Kenna API](https://apidocs.kennasecurity.com/reference) from [Expanse](https://expanse.co/).

For this example, you will need to configure [encrypted secrets](https://docs.github.com/en/free-pro-team@latest/actions/reference/encrypted-secrets ) in your repository for the following variables:

- expanse_api_key
- kenna_api_key

```yaml
name: Expanse-Action

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
      run : exec bundle exec ruby toolkit.rb task=expanse expanse_api_key=${expanse_api_key} kenna_api_host=api.us.kennasecurity.com kenna_connector_id=164377 kenna_api_key=${kenna_api_key} -v
      env:
        expanse_api_key=: "${{secrets.expanse_api_key}}"
        kenna_api_key=: "${{secrets.kenna_api_key}}"
```

## Microsoft Defender ATP

As configured this action will run every hour, and upload data to the [Kenna API](https://apidocs.kennasecurity.com/reference) from [Microsoft Defender ATP](https://docs.microsoft.com/en-us/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection).

For this example, you will need to configure [encrypted secrets](https://docs.github.com/en/free-pro-team@latest/actions/reference/encrypted-secrets ) in your repository for the following variables:

- atp_client_id
- atp_client_secret
- atp_tenant_id
- kenna_api_key

```yaml
name: MS-Defender-ATP-Action

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
      run : exec bundle exec rubytask=ms_defender_atp atp_client_id=${atp_client_id}  atp_client_secret=${atp_client_secret} atp_tenant_id=${atp_tenant_id} batch_page_size=1 kenna_api_host=api.us.kennasecurity.com kenna_connector_id=164377 kenna_api_key=${kenna_api_key} -v
      env:
        atp_client_id=: "${{secrets.atp_client_id}}"
        atp_client_secret=: "${{secrets.atp_client_secret}}"
        atp_tenant_id=: "${{secrets.atp_tenant_id}}"
        kenna_api_key=: "${{secrets.kenna_api_key}}"
```

## Nozomi Networks

As configured this action will run every hour, and upload data to the [Kenna API](https://apidocs.kennasecurity.com/reference) from [Nozomi Networks](https://www.nozominetworks.com/).

For this example, you will need to configure [encrypted secrets](https://docs.github.com/en/free-pro-team@latest/actions/reference/encrypted-secrets ) in your repository for the following variables:

- nozomi_api_host
- nozomi_user
- nozomi_password
- kenna_api_key

```yaml
name: Nozomi-Action

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
      run : exec bundle exec ruby toolkit.rb task=nozomi nozomi_user=${nozomi_user} nozomi_password=${nozomi_password} nozomi_api_host=${nozomi_api_host} nozomi_page_size=500 kenna_api_host=api.us.kennasecurity.com kenna_connector_id=164377 kenna_api_key=${kenna_api_key} -v
      env:
        nozomi_api_host=: "${{secrets.nozomi_api_host}"
        nozomi_user=: "${{secrets.nozomi_user}}"
        nozomi_password=: "${{secrets.nozomi_password}}"
        kenna_api_key=: "${{secrets.kenna_api_key}}"
```

## Security Scorecard

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

## Snyk

As configured this action will run every hour, and upload data to the [Kenna API](https://apidocs.kennasecurity.com/reference) from [Snyk](https://snyk.io/).

For this example, you will need to configure [encrypted secrets](https://docs.github.com/en/free-pro-team@latest/actions/reference/encrypted-secrets ) in your repository for the following variables:

- snyk_api_secret
- kenna_api_key

```yaml
name: Snyk-Action

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
      run : exec bundle exec ruby toolkit.rb task=snyk snyk_api_secret=${snyk_api_secret} kenna_api_host=api.us.kennasecurity.com kenna_connector_id=164377 kenna_api_key=${kenna_api_key} -v
      env:
        snyk_api_secret=: "${{secrets.snyk_api_secret}}"
        kenna_api_key=: "${{secrets.kenna_api_key}}"

```

## RiskIQ

As configured this action will run every hour, and upload data to the [Kenna API](https://apidocs.kennasecurity.com/reference) from [RiskIQ](https://www.riskiq.com/).

For this example, you will need to configure [encrypted secrets](https://docs.github.com/en/free-pro-team@latest/actions/reference/encrypted-secrets ) in your repository for the following variables:

- riskiq_api_key
- riskiq_api_secret
- kenna_api_key

```yaml
name: RiskIQ-Action

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
      run : exec bundle exec ruby toolkit.rb task=riskiq riskiq_api_key=${riskiq_api_key} riskiq_api_secret=${riskiq_api_secret} riskiq_create_ssl_misconfigs=NO riskiq_create_open_ports=NO riskiq_create_cves=YES kenna_api_host=api.us.kennasecurity.com kenna_connector_id=164377 kenna_api_key=${kenna_api_key} -v
      env:
        riskiq_api_key=: "${{secrets.riskiq_api_key}}"
        riskiq_api_secret=: "${{secrets.riskiq_api_secret}}"
        kenna_api_key=: "${{secrets.kenna_api_key}}"
```

## Important Considrations

While this repository is public to demo the action, we strongly suggest you run this in a [private repository](https://docs.github.com/en/free-pro-team@latest/github/administering-a-repository/setting-repository-visibility) to stop publicly exposing the logs which may contain hostnames and vulnerability data.

## Todo

- Better Documention

## More Information

For documentation on the Kenna Toolkit itself, including other output capabilities, see the [Kenna Toolkit](https://github.com/KennaPublicSamples/toolkit).
