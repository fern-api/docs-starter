# Fern Docs Starter Repo

```text
Start building beautiful documentation in under 5 minutes.
```

What this repo produces: [helloworld.docs.buildwithfern.com](https://helloworld.docs.buildwithfern.com)

## Quick start 

### Step 1: Use this template

Select "Use this template" and then "Create a new repository." Choose the appropriate organization and then name the repo. It is common to name the repo `docs`.

### Step 2: Open in VS Code

Or your IDE of choice.

### Step 3: Add your organization name

In the file `fern.config.json` change the **organization name**. For example:

```json
{
    "organization": "HelloWorld",
    "version": "0.15.0"
}
```

In the file `docs.yml` change the **docs url**. For example:

```yml
instances:
  - url: helloworld.docs.buildwithfern.com
```

### Step 4: Generate your docs

Install the Fern CLI by running:

```bash
npm install -g fern-api
```

Generate docs:

```bash
fern generate --docs
```

You'll be asked to login and connect your GitHub account.


Once the docs are generated, you'll see the URL your docs published to. For example:

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
