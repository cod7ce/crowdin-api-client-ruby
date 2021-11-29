[<p align='center'><img src='https://support.crowdin.com/assets/logos/crowdin-dark-symbol.png' data-canonical-src='https://support.crowdin.com/assets/logos/crowdin-dark-symbol.png' width='200' height='200' align='center'/></p>](https://crowdin.com)

# Crowdin Ruby client

The Crowdin Ruby client is a lightweight interface to the Crowdin API v2. It provides common services for making API requests.

Crowdin API is a full-featured RESTful API that helps you to integrate localization into your development process. The endpoints that we use allow you to easily make calls to retrieve information and to execute actions needed.

For more about Crowdin API v2 see the documentation:
- [Crowdin](https://support.crowdin.com/api/v2/)
- [Crowdin Enterprise](https://support.crowdin.com/enterprise/api/)

### Status

[![Gem](https://img.shields.io/gem/v/crowdin-api?logo=ruby&cacheSeconds=1800)](https://rubygems.org/gems/crowdin-api)
[![Gem](https://img.shields.io/gem/dt/crowdin-api?cacheSeconds=1800)](https://rubygems.org/gems/crowdin-api)
[![Gem](https://img.shields.io/gem/dtv/crowdin-api?cacheSeconds=1800)](https://rubygems.org/gems/crowdin-api)

[![Test and Lint](https://github.com/crowdin/crowdin-api-client-ruby/actions/workflows/test-and-lint.yml/badge.svg)](https://github.com/crowdin/crowdin-api-client-ruby/actions/workflows/test-and-lint.yml)
[![codecov](https://codecov.io/gh/crowdin/crowdin-api-client-ruby/branch/master/graph/badge.svg?token=OJsyJwQbFM)](https://codecov.io/gh/crowdin/crowdin-api-client-ruby)
[![GitHub issues](https://img.shields.io/github/issues/crowdin/crowdin-api-client-ruby?cacheSeconds=1800)](https://github.com/crowdin/crowdin-api-client-ruby/issues)
[![GitHub](https://img.shields.io/github/license/crowdin/crowdin-api-client-ruby?cacheSeconds=18000)](https://github.com/crowdin/crowdin-api-client-ruby/blob/main/LICENSE)

## Table of Contents
* [Installation](#installation)
* [Quick Start](#quick-start)
  * [Initialization](#initialization)
  * [How to call methods](#how-to-call-methods)
  * [Command-Line Client](#command-line-client)
* [Seeking Assistance](#seeking-assistance)
* [Contributing](#contributing)
* [License](#license)

## Installation

Add this line to your application's Gemfile:

```gemfile
gem 'crowdin-api', '~> 1.0.0'
```

And then execute:

```console
bundle install
```

Or install it yourself as:

```console
gem install crowdin-api
```

---

:bookmark_tabs: For versions *0.6.0* and lower see the [branch api/v1](https://github.com/crowdin/crowdin-api-client-ruby/tree/api/v1). Please note that these versions are no longer supported.

:exclamation: Migration from version *0.6.0* to *1.x.x* requires changes in your code.

---

## Quick start

### Initialization
```ruby
require 'crowdin-api'

# Create a new Crowdin Client object.
crowdin = Crowdin::Client.new do |config|
  config.api_token = 'YourApiToken'
end
# or you can create Enterprise instance by specify your organization_domain
crowdin = Crowdin::Client.new do |config|
  config.api_token = 'YourEnterpriseApiToken'
  config.organization_domain = 'YourOrganizationDomain'
end

# Also you can specify project_id to handle it in methods

# All Crowdin Client config options:
crowdin = Crowdin::Client.new do |config|
  config.api_token = 'YourApiToken' # [String] required
  config.organization_domain = 'YourOrganizationDomain' # [String] optional
  config.project_id = 'YourProjectId' # [Integer] nil by default
  config.enable_logger = true # [Boolean] false by default
end
```

To generate a new token in Crowdin, follow these steps:
- Go to *Account Settings* > *API* tab, *Personal Access Tokens* section, and click *New Token*.
- Specify *Token Name* and click *Create*.

To generate a new token in Crowdin Enterprise, follow these steps:
- Go to *Account Settings* > *Access tokens* tab and click *New token*.
- Specify *Token Name*, select *Scopes* and *Projects*, click *Create*.

### How to call methods

```ruby
# Create Project
project = crowdin.add_project(name: your_project_name, sourceLanguageId: your_language_id)

# Get list of Projects
projects = client.list_projects

# Get specified project
project = client.get_project(your_project_id)

# Get list of Projects with offset and limit
projects = client.list_projects(offset: 10, limit: 20)

# Add Storage
adding_storage_response = crowdin.add_storage(File.open('YourFilename.extension'))
# or you can specify only filename
adding_storage_response = crowdin.add_storage('YourFilename.extension')

# Download file
filename = crowdin.download_file(your_destination, your_file_id, your_project_id)
# your_destination - filename or full path to file
# project_id is optional, as it can be initialized with a Crowdin Client

# File revisions
file_revisions = crowdin.list_file_revisions(your_file_id, { limit: 10, project_id: your_project_id })
# project_id is optional, as it can be initialized with a Crowdin Client
```

### Command-Line Client

The Crowdin Ruby client support crowdin-console, where you can test endpoints easier

```console
bundle exec crowdin-console --enable-logger --api-token API_TOKEN --project-id PROJECT_ID
```

Or Crowdin Enterprise

```console
bundle exec crowdin-console --enable-logger --enterprise --api-token API_TOKEN --organization-domain YOUR_DOMAIN
```

When execute you'll have IRB console with configured *@crowdin* instance

```
> @crowdin.list_projects
```

## Seeking Assistance

If you find any problems or would like to suggest a feature, please read the [How can I contribute](/CONTRIBUTING.md#how-can-i-contribute) section in our contributing guidelines.

Need help working with Crowdin Ruby client or have any questions? [Contact](https://crowdin.com/contacts) Customer Success Service.

## Contributing

If you want to contribute please read the [Contributing](/CONTRIBUTING.md) guidelines.

## License

<pre>
The Crowdin Ruby Client is licensed under the MIT License.
See the LICENSE.md file distributed with this work for additional 
information regarding copyright ownership.

Except as contained in the LICENSE file, the name(s) of the above copyright
holders shall not be used in advertising or otherwise to promote the sale,
use or other dealings in this Software without prior written authorization.
</pre>
