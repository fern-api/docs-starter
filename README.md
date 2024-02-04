<br/>
<div align="center">
  <a href="https://www.buildwithfern.com/?utm_source=github&utm_medium=readme&utm_campaign=docs-starter&utm_content=logo">
    <img src="/fern/docs/assets/logo_light_mode.png" height="50" align="center" alt="header" />
  </a>
  
  <br/>

# Docs Starter

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

## Let's get started

### Step 1: Use this template

1. Click on the "Use this template" button. You must be logged into GitHub.
2. Create a new repository. Name it anything you like; `docs` is a common naming choice.

### Step 2: Clone and open in your preferred code editor

Clone your newly created repository and open it in your favorite integrated development environment (IDE) or code editor.

The files and folders discussed in the following steps will be inside a `fern` folder in your repository.

### Step 3: Customize organization name

In the `fern.config.json` file, replace the placeholder organization name with your actual organization name. For example:

```json
{
    "organization": "YourOrganization",
    "version": "0.16.25"
}
```

In the `docs.yml` file, update the docs URL to match your organization's naming convention. For example:

```yml
instances:
  - url: your-organization.docs.buildwithfern.com
```


### Step 4: Install the Fern CLI

Install the Fern CLI globally by running:

```bash
npm install -g fern-api
```
As this is a global command, you can run it from any location. The CLI commands in the following steps must be run from within your repository.

### Step 5 (Optional): Use an OpenAPI Specification

If you will be using [Fern Definitions](https://docs.buildwithfern.com/api-definition/fern-definition/overview) to describe your API, skip to [Step 6](#step-6-generate-your-documentation).

If you will be using the [OpenAPI Specification](https://chat.openai.com/share/47bcc007-17d8-483a-ab5a-91c10c4a73e1) (OAS), follow these steps:
1. Delete the `definition` folder.
2. Run:

```bash
fern init --openapi URL_OR_PATH_TO_YOUR_OPENAPI_SPEC
```

Examples:

```fern init --openapi https://petstore3.swagger.io/api/v3/openapi.json```

```fern init --openapi ../apis/openapi.yml```

You can use a URL to an OAS file online, or you can use a local path. The file must be formatted as JSON or YAML. 

Confirm that you see a new folder named `openapi` and that it contains the OAS file you specified, in YAML format.

### Step 6: Generate your documentation

Generate and publish your documentation with the following command:

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
### Step 7: Customize your documentation

To update your API definitions:
- For [Fern Definitions](https://docs.buildwithfern.com/api-definition/fern-definition/overview), update the files in the `definition` folder.
- For OpenAPI Specification, update the file in the `openapi` folder. YAML and JSON file formats are supported.

Next, modify the markdown pages located in the `docs/pages` folder, such as the Welcome page.

Further tailor your documentation to match your brand by adjusting settings in the `docs.yml` file. 

To re-publish the updates to your documentation, run `fern generate --docs` again.

To preview updates to your documentation before publishing changes, run `fern generate --docs --preview`.

Fern has a built-in component library for you to use. [Explore the components.](https://docs.buildwithfern.com/generate-docs/component-library/)

### Step 8: Set up a custom domain

If you wish to use a custom subdomain like `https://docs.your-organization.com` or a subpath like `https://your-organization.com/docs`, you can subscribe to the [Starter plan](https://buildwithfern.com/pricing). Once subscribed, update `docs.yml` with the custom domain configuration:

``` yaml
 - url: your-organization.docs.buildwithfern.com
   custom-domain: docs.your-organization.com
```

### Step 9: Explore advanced features

For advanced documentation features and options, view the full [configuration docs](https://docs.buildwithfern.com/generate-docs/overview/configuration).

Good luck creating beautiful and functional documentation! 🌿
