<br/>
<div align="center">
  <a href="https://www.buildwithfern.com/?utm_source=github&utm_medium=readme&utm_campaign=docs-starter&utm_content=logo">
    <img src="/fern/docs/assets/icon.png" height="120" align="center" alt="header" />
  </a>
  
  <br/>

# Fern Docs Starter

Create beautiful documentation in under 5 minutes. Here's [an example!](https://your-organization.docs.buildwithfern.com)

[![Discord](https://img.shields.io/badge/Join%20Our%20Community-black?logo=discord)](https://discord.com/invite/JkkXumPzcG)

</div>

---

## Customer Showcase

Your docs can look this good:

- [Flatfile's API Reference](https://reference.flatfile.com/api-reference/events/create-an-event)
- [Sugeragent's Docs](https://docs.superagent.sh/)
- [Credal's Docs](https://docs.credal.ai/)

---

## Let's Get Started

### Step 1: Use This Template

1. Click on the "Use this template" button.
2. Create a new repository. Name it anything you like, `docs` is a common naming choice.

### Step 2: Open in Your Preferred IDE

Clone your newly created repository and open it in your favorite integrated development environment (IDE) or code editor.

### Step 3: Customize Organization Name

In the fern.config.json file, replace the placeholder organization name with your actual organization name. For example:

```json
{
    "organization": "YourOrganization",
    "version": "0.15.18"
}
```

Also, in the docs.yml file, update the docs URL to match your organization's naming convention. For example:

```yml
instances:
  - url: your-organization.docs.buildwithfern.com
```

### Step 4: Generate Your Documentation

1. Install the Fern CLI by running:

```bash
npm install -g fern-api
```

1. Generate your documentation with the following command:

```bash
fern generate --docs
```

You will be prompted to log in and connect your GitHub account.

Once the documentation is generated, you will receive a URL where your documentation is published. For example:

```shell
┌─
│ ✓  your-organization.docs.buildwithfern.com
└─
```

### Step 5: Choose an API definition format

If you're using a [Fern Definition](https://docs.buildwithfern.com/api-definition/fern-definition/overview), you can edit the files within the [`definition`](/fern/definition/) folder.

If you're using an [OpenAPI Specification](https://docs.buildwithfern.com/api-definition/openapi/extensions), then run the command: `fern generate`. You'll see a new folder created called `openapi` that contains your spec. You can edit this spec to make it your own OR copy and paste a spec you already have. Then, delete the `definition` folder.

### Step 6: Customize Your Documentation

Next, modify the markdown pages located in the [pages](fern/docs/pages/) directory. You can further tailor your documentation to match your brand by adjusting settings in the [docs.yml](fern/docs.yml) file.

Fern has a built-in component library for you to use. [Explore the components.](https://docs.buildwithfern.com/generate-docs/component-library/)

### Step 6: Set Up a Custom Domain

If you wish to use a custom domain like `docs.your-organization.com` or a subdirectory like `your-organization.com/docs`, you can subscribe to the [Starter plan](https://buildwithfern.com/pricing). Once subscribed, update [docs.yml](fern/docs.yml) with the custom domain configuration:

``` yaml
 - url: your-organization.docs.buildwithfern.com
   custom-domain: docs.your-organization.com
```

### Step 7: Explore Advanced Features

For advanced documentation features and options, visit the [Fern Docs](https://docs.buildwithfern.com/generate-docs).

**Advanced features** include:

- Versioning
- Changelog
- Multiple APIs
- Custom background
- Bring your own fonts

Good luck creating beautiful and functional documentation! 🌿
