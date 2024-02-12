<br/>
<div align="center">
  <a href="https://www.buildwithfern.com/?utm_source=github&utm_medium=readme&utm_campaign=docs-starter-openapi&utm_content=logo">
    <img src="/fern/docs/assets/fern.png" height="50" align="center" alt="header" />
  </a>
  
  <br/>

# Docs Starter

In this tutorial, you will learn how to create beautiful documentation in under 5 minutes using an OpenAPI/Swagger specification.
</div>

---

### Step 1: Use this template

1. Click on the "Use this template" button. You must be logged into GitHub.
2. Create a new repository. Name is something like `fern-docs`.

### Step 2: Clone and open in your preferred code editor

Clone your newly created repository and open it in your favorite code editor (e.g., VS Code).

The files and folders discussed in the following steps will be inside a `fern` folder in your repository.

### Step 3: Customize organization name

In the `fern.config.json` file, replace the placeholder organization name with your actual organization name. For example:

```diff
{
-   "organization": "Petstore",
+   "organization": "MY_ORGANIZATION_NAME",
    "version": "0.17.8"
}
```

In the `docs.yml` file, update the docs URL to match your organization's naming convention. For example:

```diff
instances:
-  - url: petstore-openapi.docs.buildwithfern.com
+  - url: MY_ORGANIZATION_NAME.docs.buildwithfern.com
```

### Step 4: Install the Fern CLI

Install the Fern CLI globally by running:

```bash
npm install -g fern-api
```

The CLI commands in the following steps must be run from within the root of your repository.

### Step 5: Check that your OpenAPI specification is valid

Run the following command to check that your OpenAPI specification is valid:

```bash
fern check
```

### Step 6: Generate your documentation

Run the following command:

```bash
fern generate --docs
```

You will be prompted to log in and connect your GitHub account.

Once the documentation is generated, you will receive a URL where your documentation is published. For example:

```shell
┌─
│ ✓  petstore-openapi.docs.buildwithfern.com
└─

# OR

┌─
│ ✓  MY_ORGANIZTION_NAME.docs.buildwithfern.com
└─
```

### Step 7: (Optional) Add your own OpenAPI specification file

If you'd like to use your own OpenAPI file, run:

```bash
fern init --openapi URL_TO_YOUR_OPENAPI

# OR

fern init --openapi PATH_TO_YOUR_OPENAPI
```

Examples:

```bash
fern init --openapi https://raw.githubusercontent.com/fern-api/docs-starter-openapi/main/fern/openapi/openapi.yaml

# OR

fern init --openapi ../apis/openapi.yml
```

Confirm that you see a folder named `openapi` which contains the OpenAPI file you specified, in YAML format.

*Note: Don't have an OpenAPI spec? Use Fern's simpler format to define your API.* [*Learn more*](https://github.com/fern-api/docs-starter-fern-definition)

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

---

### Support

Need help? Email us at (support@buildwithfern.com)[mailto:support@buildwithfern.com] or join our [Discord community](https://discord.com/invite/JkkXumPzcG).

### Customer Showcase

Your docs can look this good:

- [Flatfile's API Reference](https://reference.flatfile.com/api-reference/events/create-an-event)
- [Sugeragent's Docs](https://docs.superagent.sh/)
- [Credal's Docs](https://docs.credal.ai/)

### About OpenAPI (formerly Swagger)

The OpenAPI specification is a format for describing REST APIs. The specification consists of a single JSON or YAML file. OpenAPI was previously known as Swagger. Fern supports both OpenAPI (3.x) and Swagger (2.x). We'll refer to the specification as OpenAPI throughout this guide.