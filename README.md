<br/>
<div align="center">
  <a href="https://www.buildwithfern.com/?utm_source=github&utm_medium=readme&utm_campaign=docs-starter&utm_content=logo">
    <img src="fern.png" height="120" align="center" alt="header" />
  </a>
  
  <br/>

# Quickstart

[![Contributors](https://img.shields.io/github/contributors/fern-api/starter-docs.svg)](https://GitHub.com/dotnet/docs/graphs/contributors/)
[![Pulls-opened](https://img.shields.io/github/issues-pr/fern-api/starter-docs.svg)](https://GitHub.com/starter-docs/docs/pulls?q=is%3Aissue+is%3Aopened)
[![Pulls-merged](https://img.shields.io/github/issues-search/fern-api/starter-docs?label=merged%20pull%20requests&query=is%3Apr%20is%3Aclosed%20is%3Amerged&color=darkviolet)](https://github.com/starter-docs/docs/pulls?q=is%3Apr+is%3Aclosed+is%3Amerged)

[![Discord](https://img.shields.io/badge/Join%20Our%20Community-black?logo=discord)](https://discord.com/invite/JkkXumPzcG)

</div>

```text
Start building beautiful documentation in under 5 minutes.
```

**See the Docs this repo generates**  ->  [https://helloworld.docs.buildwithfern.com](https://helloworld.docs.buildwithfern.com)

---

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

### Step 5: Customize your docs 

To start, swap the OpenAPI spec for your own. Then revise the markdown pages in the [content](fern/docs/content/) directory. You'll find additional configurations in [docs.yml](fern/docs.yml) that allow you to tailor your docs to fit your brand.

### Step 6: Setup a custom domain 

To set up a subdomain like `docs.your-website.com` or a subdirectory like `your-website.com/docs`, subscribe to the Fern [Starter plan](https://buildwithfern.com/pricing). Once subscribed, update your `docs.yml` to add:

``` yaml
 - url: {your-organization}.docs.buildwithfern.com
   custom-domain: docs.{your-organization}.com
```

### Step 7: You've advanced!
Looking to use **advanced features**? Head to the [Fern Docs Advanced Repo](https://github.com/fern-api/docs-advanced).

**Advanced features** include:
- Versioning 
- Changelog
- Multiple APIs
- Custom background
- Bring your own fonts
