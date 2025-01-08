# mail2rss

## [Mandarin documentation here](README_ZN.md).

---

Zero cost method for converting newsletter to RSS:

- [Cloudflare WWrkers](https://workers.cloudflare.com/) 
- [testmail.app](https://testmail.app/).

Cloudflare Workers allows for 100,000 free requests per day.  

testmail.app's free tier enables you to receive 100 emails per month, and the email are saved for one day.

If you are a student then you can apply for GitHub Student Developer Pack and for free get the testmail essential tier which allows you to receive 10,000 emails per month instead.

## Setting up testmail.app

After you register, you will get your own namespace, through which different email addresses can be constructed.

Suppose the namespace is `diyyy`，One can construct such an email address like `diyyy.{tag}@inbox.testmail.app` where `{tag}` can be replaced by anything.

For example，one can use `diyyy.quartz@inbox.testmail.app` to subscribe to _Quartz_'s newsletter，or use `diyyy.stefanjudis@inbox.testmail.app` to subscribe to _Stefan's web dev journey_.

testmail provides a rich API for getting emails, including filtering tags, matching tag prefixes, limiting counts, and support for GraphQL queries.

The official documentation is here: <https://testmail.app/docs/>

After signing in，get your `namespace` and `api keys` at <https://testmail.app/console>, which are both required later.

## Deploying to Cloudflare Workers

1. Create a new worker, if one hasn't been yet created and deploy the default _Hello World_.
2. Setup Cloudflare [environment variables](https://developers.cloudflare.com/workers/platform/environment-variables/#environment-variables-via-the-dashboard) by creating two new _Text_ variables named
    ```js
    TESTMAIL_NAMESPACE : xxxx; // testmail's namespace
    TESTMAIL_API_KEY : xxxxxxxxxxxxxxx; // testmail's api key - it's recommended to use encryption for this field
    ```
    and use the testmail credentials.
3. Edit the code in the online editor and replace it with `mail2rss.js` and deploy.

## Setting up RSS reader

After you deploy to workers，you can use `{namespace}.{tag}@inbox.testmail.app` to subscribe to a newsletter，and subscribe to `https://xxx.xxx.workers.dev/{tag}` in your RSS reader.

Subscribing to `https://<name-of-worker>.<cloudflare-username>.workers.dev/` will result in an empty feed as no tag is defined.

Suppose the namespace is diyyy，then use `diyyy.quartz@inbox.testmail.app` to subscribe _Quartz_'s newsletter，then subscribe to `https://<name-of-worker>.<cloudflare-username>.workers.dev/quartz`.

## Remarks

These tools can help with debugging:

- Cloudflare's online code editor: within the editor one can create a request directly to `https://<name-of-worker>.<cloudflare-username>.workers.dev/{tag}` and debug using the integrated Developer's Tools
- <https://www.rssboard.org/rss-validator/check.cgi>: to check the validity of the generated RSS feed
- <https://html.onlineviewer.net/>: to view the HTML of the newsletter

## Contributors

- [Artin](https://github.com/bytemain): original author
