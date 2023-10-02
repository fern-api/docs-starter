# Fern Docs Starter Repo

```text
Start building beautiful documentation in under 5 minutes.
```

What this repo produces: [helloworld.docs.buildwithfern.com](https://helloworld.docs.buildwithfern.com)

![Hello World Docs](fern/docs/assets/helloworld.png)

## Quick start 

### Step 1: Use this template.

### Step 2: Generating "Hello World" docs

Install the Fern CLI by running:

```bash
npm install -g fern-api
```

Now that the CLI is installed, generate docs:

```bash
fern generate --docs
```

You'll be asked to login. Enter `y` which will walk you through connecting your GitHub account.


When the docs are generated, Fern automatically publishes them to the domain configured in `docs.yml`. After successfully generating docs, you'll see:

```text
┌─
│ ✓  helloworld.docs.buildwithfern.com
└─
```

### Step 3: Customize your docs 

To start, swap the OpenAPI spec for your own. Then revise the markdown pages in the [content](fern/docs/content/) directory. You'll find additional configurations in [docs.yml](fern/docs.yml) that allow you to tailor your docs to fit your brand.

### Step 4: Setup a custom domain 

To set up a subdomain like `docs.your-website.com` or a subdirectory like `your-website.com/docs`, subscribe to the Fern [Starter plan](https://buildwithfern.com/pricing). Once subscribed, update your `docs.yml` to add:

``` yaml
 - url: {your-organization}.docs.buildwithfern.com
   custom-domain: docs.{your-organization}.com
```

### Step 5: You've advanced!
Looking to use **advanced features**? Head to the [Fern Docs Advanced Repo](https://github.com/fern-api/docs-advanced).

**Advanced features** include:
- Versioning 
- Changelog
- Multiple APIs
- Custom background
- Bring your own fonts
