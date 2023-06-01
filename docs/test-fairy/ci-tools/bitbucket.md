---
id: bitbucket
title: Bitbucket Pipelines
sidebar_label: Bitbucket Pipelines
---

import useBaseUrl from '@docusaurus/useBaseUrl';
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

Set up Bitbucket Pipelines to upload your build artifacts (IPA or APK) directly to TestFairy for distribution.

## Setting Up

1. Open your Bitbucket repository, and select **Settings** > **Pipelines** > **Environment Variables**

   <img src={useBaseUrl('/img/test-fairy/ci-tools/bitbucket-pipelines-0.png')} alt="screenshot of Bitbucket pipelines"/>

2. Fill in **variable** and **value**:

   - **Variable**: TESTFAIRY_API_KEY
   - **Value**: _Your API application key. See https://app.testfairy.com/settings for details._
   - **Secured**: Y

   When done, click **Add**.

   <img src={useBaseUrl('/img/test-fairy/ci-tools/bitbucket-pipelines-1.png')} alt="screenshot of Bitbucket pipelines"/>

3. Edit your `bitbucket-pipelines.yml` and add this command to your `script` section:

   ```bash
   curl https://app.testfairy.com/api/upload -F api_key=${TESTFAIRY_API_KEY} -F file=@MyApplicationFile.apk -F format=readable
   ```

:::note
Do not forget to replace `MyApplicationFile.apk` with the path to your APK or IPA files.
:::

Additional optional parameters such as `testers-groups`, `notify`, and `comment` can be added to this line. Refer to the [Upload API reference guide](/test-fairy/api-reference/upload-api) for more information and examples.

Here, for example, is a screenshot of a sample `bitbucket-pipelines.yml` file:

<img src={useBaseUrl('/img/test-fairy/ci-tools/bitbucket-pipelines-2.png')} alt="screenshot of Bitbucket pipelines"/>