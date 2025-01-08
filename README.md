# mail2rss

Zero cost method for converting newsletter to RSS:

- [Cloudflare Workers](https://workers.cloudflare.com/) 
- [testmail.app](https://testmail.app/)

Cloudflare Workers allows for 100,000 free requests per day.  

testmail.app's free tier enables you to receive 100 emails per month and the email are saved for one day.

If you are a student then you can apply for GitHub Student Developer Pack and for free get the testmail essential tier which allows you to receive 10,000 emails per month instead.

## Quick Start

1. Sign up for Cloudflare and testmail.app and activate them both.
2. [Setting up testmail.app](#setting-up-testmailapp)
3. [Deploying to Cloudflare Workers](#deploying-to-cloudflare-workers)
4. [Setting up RSS reader](#setting-up-rss-reader)

## Setting up testmail.app

1. Navigate to <https://testmail.app/console> to get the `<testmail-namespace>` and `<testmail-api-key>`.
2. Keep the browser tab and the values are required for <#deploying-to-cloudflare-workers>

**Remarks: General**

testmail provides a rich API for getting emails, including filtering tags, matching tag prefixes, limiting counts, and support for GraphQL queries.

The official documentation is here: <https://testmail.app/docs/>

**Remarks: Example**

Suppose the namespace is `diyyy`，One can construct such an email address like `diyyy.{tag}@inbox.testmail.app` where `{tag}` can be replaced by anything.

For example，one can use `diyyy.quartz@inbox.testmail.app` to subscribe to _Quartz_'s newsletter，or use `diyyy.stefanjudis@inbox.testmail.app` to subscribe to _Stefan's web dev journey_.

## Deploying to Cloudflare Workers

1. Create a new worker, if one hasn't been yet created and deploy the default _Hello World_.
2. Setup Cloudflare [environment variables](https://developers.cloudflare.com/workers/platform/environment-variables/#environment-variables-via-the-dashboard) by creating two new _Text_ variables named
    ```
    TESTMAIL_NAMESPACE : <testmail-namespace>
    TESTMAIL_API_KEY : <testmail-api-key>
    ```
    and use the testmail credentials.
3. Edit the code in the online editor and replace it with `mail2rss.js` and deploy.

## Setting up RSS reader

1. Navigate in a browser to 
    ```
    https://<name-of-worker>.<cloudflare-username>.workers.dev/
    ```
2. Add a specific tag e.g. `<my-cool-tag>`.
3. Copy the generated email for the newsletter e.g. 
    ```
    <testmail-namespace>.<my-cool-tag>@inbox.testmail.app
    ```
4. Copy the generated subscribe address into a RSS feed reader app e.g. 
    ```
    https://<name-of-worker>.<cloudflare-username>.workers.dev/<my-cool-tag>
    ```

**Remarks**

Subscribing to `https://<name-of-worker>.<cloudflare-username>.workers.dev/` will result in an empty feed as no _tag_ is defined.

## Debugging Tools

These tools can help with debugging:

- Cloudflare's online code editor: within the editor one can create a request directly to `https://<name-of-worker>.<cloudflare-username>.workers.dev/{tag}` and debug using the integrated Developer's Tools
- <https://www.rssboard.org/rss-validator/check.cgi>: to check the validity of the generated RSS feed
- <https://html.onlineviewer.net/>: to view the HTML of the newsletter

## [Mandarin documentation here](README_ZH.md)

## Contributors

- [barefootstache](https://github.com/barefootstache)
- [Artin](https://github.com/bytemain) (original author)
