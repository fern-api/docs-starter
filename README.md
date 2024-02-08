<br/>
<div align="center">
  <a href="https://www.buildwithfern.com/?utm_source=github&utm_medium=readme&utm_campaign=docs-starter-openapi&utm_content=logo">
    <img src="/fern/docs/assets/logo_light_mode.png" height="50" align="center" alt="header" />
  </a>
  
  <br/>

# Docs Starter

Create beautiful documentation in under 5 minutes using an OpenAPI/Swagger specification. Here's [an example!](https://petstore-openapi.docs.buildwithfern.com)

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

### About OpenAPI/Swagger

The OpenAPI specification is a format for describing REST APIs. The specification consists of a single JSON or YAML file. OpenAPI was previously known as Swagger. Fern supports both OpenAPI (3.x) and Swagger (2.x). We'll refer to the specification as OpenAPI throughout this guide.

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
    "organization": "Petstore",
    "version": "0.17.2"
}
```

In the `docs.yml` file, update the docs URL to match your organization's naming convention. For example:

```yml
instances:
  - url: petstore-openapi.docs.buildwithfern.com
```

### Step 4: Install the Fern CLI

Install the Fern CLI globally by running:

```bash
npm install -g fern-api
```

As this is a global command, you can run it from any location. The CLI commands in the following steps must be run from within your repository.

### Step 5: (Optional) Use your OpenAPI specification

If you'd like to use the an example OpenAPI specificaton file, run:

```bash
fern init --openapi https://petstore3.swagger.io/api/v3/openapi.json
```

If you'd like to use your own OpenAPI specification file, run:

```bash
fern init --openapi URL_OR_PATH_TO_YOUR_OPENAPI_SPEC
```

You can use a URL to an OAS file online, or you can use a local path. The file must be formatted as JSON or YAML. 

Examples:

```fern init --openapi https://petstore3.swagger.io/api/v3/openapi.json```

```fern init --openapi ../apis/openapi.yml```

Confirm that you see a new folder named `openapi` and that it contains the OAS file you specified, in YAML format.

*Note: Don't have an OpenAPI spec? Use Fern's simpler format to define your API.* [*Learn more*](https://github.com/fern-api/docs-starter-fern-definition)

### Step 6: Check that your OpenAPI specification is valid

Run the following command to check that your OpenAPI specification is valid:

```bash
fern check
```

If you see errors, resolve them in your OpenAPI specification file. If you need help, reach out in [Discord](https://discord.com/invite/JkkXumPzcG) or [via email](mailto:support@buildwithfern.com). We're here to help!

### Step 7: Generate your documentation

Generate and publish your documentation with the following command:

```bash
fern generate --docs
```

You will be prompted to log in and connect your GitHub account.

Once the documentation is generated, you will receive a URL where your documentation is published. For example:

```shell
┌─
│ ✓  petstore-openapi.docs.buildwithfern.com
└─
```

### Step 8: Customize your documentation

Next, modify the markdown pages located in the `docs/pages` folder, such as the Welcome page.

Further tailor your documentation to match your brand by adjusting settings in the `docs.yml` file. 

To re-publish the updates to your documentation, run `fern generate --docs` again.

To preview updates to your documentation before publishing changes, run `fern generate --docs --preview`.

Fern has a built-in component library for you to use. [Explore the components.](https://docs.buildwithfern.com/generate-docs/component-library/)

### Step 9: Set up a custom domain

If you wish to use a custom subdomain like `https://docs.YOUR_ORGANIZATION.com` or a subpath like `https://YOUR_ORGANIZATION.com/docs`, you can subscribe to the [Starter plan](https://buildwithfern.com/pricing). Once subscribed, update `docs.yml` with the custom domain configuration:

``` yaml
 - url: petstore-openapi.docs.buildwithfern.com
   custom-domain: docs.petstore-openapi.com
```

### Step 10: Explore advanced features

For advanced documentation features and options, view the full [configuration docs](https://docs.buildwithfern.com/generate-docs/overview/configuration).

Good luck creating beautiful and functional documentation! 🌿
