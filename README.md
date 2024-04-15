<br/>
<div align="center">
  <a href="https://www.buildwithfern.com/?utm_source=github&utm_medium=readme&utm_campaign=docs-starter-openapi&utm_content=logo">
    <img src="/fern/docs/assets/fern.png" height="50" align="center" alt="header" />
  </a>
  
  <br/>

# Docs Starter

Learn how to create beautiful documentation in under 5 minutes using an OpenAPI specification (formerly Swagger).
</div>

## Customer Showcase

Gett inspired by API documentation built with Fern: [Hume](https://dev.hume.ai) | [MultiOn](https://docs.multion.ai) | [Flagright](https://docs.flagright.com) | [Traceloop](https://fern.traceloop.com/docs) | [ElevenLabs](https://elevenlabs.docs.buildwithfern.com/docs/developers)

---

## Requirements

-   Node 18 or higher
-   A [GitHub](https://github.com) account
  
### Step 1: Use this template

1. Click on the **Use this template** button (found at the top right of this page). You must be logged into GitHub.
2. Choose the option to **create a new repository**. Name it `fern-docs`.

### Step 2: Clone and open the repo in your preferred code editor

Clone your newly created repository and open it in your favorite code editor (e.g., VS Code).

The files and folders discussed in the following steps will be inside the `fern/` folder in your repository.

### Step 3: Customize organization name

Open the `fern.config.json` file, which looks like this:

```json
{
    "organization": "Petstore",
    "version": "0.17.8"
}
```
Replace `"Petstore"` with your own organization name within the quotes. Spaces are permitted. Leave the `version` number unchanged.

Open the `docs.yml` file and locate the `url`, which looks like this:

```yml
instances:
  - url: petstore-openapi.docs.buildwithfern.com
```

Replace `petstore-openapi` with your own organization's name. Use only alphanumeric characters, hyphens, and underscores. Do not use spaces, and leave the rest of the URL (`docs.buildwithfern.com`) unchanged.


### Step 4: Install the Fern CLI

Install the Fern CLI globally by running:

```bash
npm install -g fern-api
```

The CLI commands in the following steps must be run from within the root folder of your repository.

### Step 5: Generate your documentation

Run the following command:

```bash
fern generate --docs
```

You will be prompted to log in and connect your GitHub account.

Once the documentation is generated, you will receive the URL where your documentation is published. For example:

```shell
┌─
│ ✓  petstore-openapi.docs.buildwithfern.com
└─

# OR

┌─
│ ✓  MY_ORGANIZATION_NAME.docs.buildwithfern.com
└─
```

### Step 6: Customize your documentation

You must run `fern generate --docs` after any modifications to re-generate and publish your documentation site.

To preview updates to your documentation before publishing changes, run `fern generate --docs --preview`.

To use your own OpenAPI specification file or to update the existing one:
- Update or replace the OpenAPI specification file in the `openapi/` folder.
- *Note: Don't have an OpenAPI spec? Use Fern's simpler format to define your API.* [*Learn more*](https://github.com/fern-api/docs-starter-fern-definition).

To modify the other docs pages:
- Update the Markdown files located in the `docs/pages/` folder, such as `welcome.mdx`.

To modify site styles and navigation, or to add new pages:
- See [Writing Content](https://buildwithfern.com/learn/docs/content/write-markdown).

To learn about Fern's built-in component library you can use in Markdown:
- See the [Component Library](https://buildwithfern.com/learn/docs/components/).
  
### Step 7: Set up a custom domain

If you wish to use a custom subdomain like `https://docs.YOUR_ORGANIZATION.com` or a subpath like `https://YOUR_ORGANIZATION.com/docs`, you can subscribe to the [Starter plan](https://buildwithfern.com/pricing). Once subscribed, update `docs.yml` with the custom domain configuration:

``` yaml
 - url: petstore-openapi.docs.buildwithfern.com
   custom-domain: docs.petstore-openapi.com
```

### Step 8: Explore advanced features

For advanced documentation features and options, view the full [configuration docs](https://buildwithfern.com/learn/docs/config/overview).

Good luck creating beautiful and functional documentation! 🌿

---

## Support

Need help? [Set up a call](https://buildwithfern.com/contact) with an expert or email us at [support@buildwithfern.com](mailto:support@buildwithfern.com). 

## About OpenAPI (formerly Swagger)

The OpenAPI specification is a format for describing REST APIs. The specification consists of a single JSON or YAML file. OpenAPI was previously known as Swagger. Fern supports both OpenAPI (3.x) and Swagger (2.x). We refer to the specification as OpenAPI throughout our documentation.
