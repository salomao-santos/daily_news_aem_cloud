# AEM Cloud Service Project Generation using Archetype via Kiro IDE Prompt

## 📋 Objective

Generate a new AEM as a Cloud Service project using Adobe's official Maven Archetype, consulting documentation via MCP AEM Documentation.

---

## 🔧 Prerequisites
- JDK 21
- Maven installed (validate with `mvn --version`)
- MCP AEM Documentation configured and active
- Access to repository: https://github.com/adobe/aem-project-archetype

---

## 📝 Step 1: Collect Project Parameters

Before executing, request the following parameters from the user:

### Required Parameters

| Parameter | Description | Example | Default |
|-----------|-----------|---------|--------|
| `appTitle` | Application title (used for website title and component groups) | "My Site" | - |
| `appId` | Technical name (used for components, configs, content folders and client libraries) | "mysite" | - |
| `groupId` | Base Maven Group ID (must be a valid Java package name) | "com.mysite" | - |
| `artifactId` | Base Maven Artifact ID | "${appId}" | ${appId} |
| `version` | Project version | "1.0-SNAPSHOT" | 1.0-SNAPSHOT |

### AEM Configuration Parameters

| Parameter | Description | Possible Values | Default |
|-----------|-----------|-------------------|--------|
| `aemVersion` | Target AEM version | `cloud`, `6.5.8` | cloud |
| `sdkVersion` | SDK version (when aemVersion=cloud) | e.g.: `2020.02.2265.20200217T222518Z-200130` | latest |
| `archetypeVersion` | Archetype version | e.g.: `56` | 56 |

### Structure Parameters

| Parameter | Description | Possible Values | Default |
|-----------|-----------|-------------------|--------|
| `package` | Java Source Package | e.g.: "com.mysite" | ${groupId} |
| `language` | Language code (ISO 639-1) | e.g.: `en`, `deu`, `pt` | en |
| `country` | Country code (ISO 3166-1) | e.g.: `US`, `BR` | us |
| `singleCountry` | Single country content structure | `y`, `n` | y |

### Feature Parameters

| Parameter | Description | Possible Values | Default |
|-----------|-----------|-------------------|--------|
| `includeDispatcherConfig` | Include dispatcher configuration | `y`, `n` | y |
| `frontendModule` | Frontend module | `general`, `none` | general |
| `includeExamples` | Include example site (Component Library) | `y`, `n` | n |
| `includeErrorHandler` | Include custom 404 page | `y`, `n` | n |
| `datalayer` | Adobe Client Data Layer integration | `y`, `n` | y |
| `amp` | AMP support for templates | `y`, `n` | n |
| `enableDynamicMedia` | Enable Dynamic Media | `y`, `n` | n |
| `enableSSR` | Enable SSR for frontend project | `y`, `n` | n |
| `precompiledScripts` | Precompile server-side scripts | `y`, `n` | n |

### CIF (Commerce Integration Framework) Parameters

| Parameter | Description | Possible Values | Default |
|-----------|-----------|-------------------|--------|
| `includeCif` | Include CIF Core Components | `y`, `n` | n |
| `commerceEndpoint` | Commerce system GraphQL endpoint | e.g.: `https://hostname.com/graphql` | - |

### Forms Parameters

| Parameter | Description | Possible Values | Default |
|-----------|-----------|-------------------|--------|
| `includeFormscommunications` | Include Forms Core Components (Communications) | `y`, `n` | n |
| `includeFormsenrollment` | Include Forms Core Components (Enrollment) | `y`, `n` | n |
| `includeFormsheadless` | Include Forms headless artifacts | `y`, `n` | n |
| `sdkFormsVersion` | Forms SDK version (when includeFormscommunications=y or includeFormsenrollment=y) | e.g.: `2020.12.17.02` | latest |

---

## 🚀 Step 2: Consult Documentation via MCP

Use MCP AEM Documentation to get updated information:

### Available MCP Commands

1. **Search archetype documentation:**
   ```
   search_experience_league(query="aem project archetype", content_types=["Documentation"])
   ```

2. **Read specific documentation:**
   ```
   read_documentation(url="https://github.com/adobe/aem-project-archetype")
   ```

3. **List available services:**
   ```
   get_available_services()
   ```

---

## ⚙️ Step 3: Generate the Project

With the collected parameters, execute the Maven command:

### Base Command

```bash
mvn org.apache.maven.plugins:maven-archetype-plugin:3.3.1:generate \
  -D archetypeGroupId=com.adobe.aem \
  -D archetypeArtifactId=aem-project-archetype \
  -D archetypeVersion=56 \
  -D appTitle="My Site" \
  -D appId="mysite" \
  -D groupId="com.mysite" \
  -D artifactId="mysite" \
  -D version="1.0-SNAPSHOT" \
  -D aemVersion="cloud" \
  -D sdkVersion="latest" \
  -D includeDispatcherConfig="y" \
  -D frontendModule="general" \
  -D language="en" \
  -D country="us" \
  -D singleCountry="y" \
  -D includeExamples="n" \
  -D includeErrorHandler="n" \
  -D datalayer="y" \
  -D amp="n" \
  -D enableDynamicMedia="n" \
  -D enableSSR="n" \
  -D precompiledScripts="n" \
  -D includeCif="n" \
  -D includeFormscommunications="n" \
  -D includeFormsenrollment="n" \
  -D includeFormsheadless="n"
```

### Project Location

The project will be generated in the current directory where the Maven command is executed.

---

## ✅ Step 4: Validation

After generation, verify:

1. **Project structure created:**
   ```bash
   ls -la
   ```

2. **Maven Modules:**
   - `core` - Java code (OSGi bundles)
   - `ui.apps` - Components, templates, dialogs
   - `ui.content` - Initial content
   - `ui.config` - OSGi configurations
   - `ui.frontend` - Frontend code (if frontendModule != none)
   - `ui.tests` - Integration tests
   - `dispatcher` - Dispatcher configuration (if includeDispatcherConfig=y)

3. **Initial build:**
   ```bash
   cd <artifactId>
   mvn clean install
   ```

---

## 📚 References

- Official repository: https://github.com/adobe/aem-project-archetype
- Documentation: Use MCP to access the latest documentation
- Available versions: https://github.com/adobe/aem-project-archetype/releases

---

## 🔍 Important Notes

- Use `frontendModule=general` for regular sites or `none` if you don't need a frontend module
- If `aemVersion=cloud`, the `sdkVersion` parameter can be specified
- `precompiledScripts` requires `aemVersion=cloud`
- CIF requires the `commerceEndpoint` parameter when `includeCif=y`
- Forms SDK version is only used when Forms is enabled
