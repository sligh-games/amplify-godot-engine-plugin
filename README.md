# AWS Amplify for Godot Engine - Plugin

[![GitHub release](https://img.shields.io/github/release/sligh-games/amplify-godot-engine-plugin)](https://github.com//sligh-games/amplify-godot-engine-plugin/releases)
[![Open Bugs](https://img.shields.io/github/issues/sligh-games/amplify-godot-engine-plugin/bug?color=d73a4a&label=bugs)](https://github.com/sligh-games/amplify-godot-engine-plugin/issues?q=is%3Aissue+is%3Aopen+label%3Abug)
[![Feature Requests](https://img.shields.io/github/issues/sligh-games/amplify-godot-engine-plugin/feature-request?color=ff9001&label=enhancement)](https://github.com/sligh-games/amplify-godot-engine-plugin/issues?q=is%3Aissue+label%3Aenhancement+is%3Aopen)
[![Closed Issues](https://img.shields.io/github/issues-closed/sligh-games/amplify-godot-engine-plugin?color=%2325CC00&label=issues%20closed)](https://github.com/sligh-games/amplify-godot-engine-plugin/issues?q=is%3Aissue+is%3Aclosed+)

A powerful Godot Engine plugin that seamlessly integrates AWS Amplify services into your game projects. This plugin enables game developers to leverage AWS cloud capabilities directly within the Godot environment, providing authentication, data storage, API access, and more with minimal configuration.

## Key Features

- **Easy Integration**: Simple installation process with minimal setup required
- **Authentication**: Complete user authentication flows with sign-up, sign-in, and account management
- **Data Management**: GraphQL-based data operations for game state persistence
- **API Access**: Simplified HTTP client for interacting with AWS resources
- **UI Components**: Ready-to-use authentication forms for rapid implementation
- **Amplify Compatibility**: Designed to work with AWS Amplify deployed resources

## Documentation

For comprehensive documentation, tutorials, and examples, visit our [official documentation](https://docs.sligh.games/#!/en/amplify-godot).

## Getting Started

Jump right into your Godot CI/CD pipeline with our comprehensive resources:
- **Quick Setup**: Follow our [quickstart guides](https://docs.sligh.games/#!/en/amplify-godot/get-started) for step-by-step implementation
- **Advanced Usage**: Explore [interactive labs](https://docs.sligh.games/#!/en/amplify-godot) for deeper integration scenarios

## Installation

### Plugin Versions

| Version | Godot Compatibility | Download | Changelog |
| --- | --- | --- | --- |
| 0.3.2 | 4.3+ | [Download](https://github.com/sligh-games/amplify-godot-engine-plugin/releases/download/v0.3.2/AWSAmplifyPlugin.zip) | [View](https://github.com/sligh-games/amplify-godot-engine-plugin/blob/main/CHANGELOG.md#032---2025-05-19) |
| 0.3.1 | 4.3+ | [Download](https://github.com/sligh-games/amplify-godot-engine-plugin/releases/download/v0.3.1/AWSAmplifyPlugin.zip) | [View](https://github.com/sligh-games/amplify-godot-engine-plugin/blob/main/CHANGELOG.md#031---2025-05-19) |

### Download the Plugin

1. Go to the [GitHub Release Section](https://github.com/sligh-games/amplify-godot-engine-plugin/releases)
2. Click on the latest release
3. Download the source code
4. Extract the plugin code
5. Copy the `addons/aws-amplify` folder to the root of your Godot project

### Enable the Plugin

1. Open Project → Project Settings → Plugins
2. Find "AWS Amplify" in the list and click the "Enable" checkbox
3. The plugin automatically loads the `aws_amplify` singleton when enabled

The AWS Amplify Plugin is now ready to be used in your project!

## Usage Examples

### Authentication

```gdscript
# Sign up a new user
aws_amplify.auth.sign_up("username", "password", {
    "email": "user@example.com",
    "name": "Player One"
})

# Sign in an existing user
aws_amplify.auth.sign_in("username", "password")

# Sign out
aws_amplify.auth.sign_out()
```

### Data Operations

```gdscript
# Query data
var operation = """
query ListItems {
    listItems {
        items {
            id
            name
            description
        }
    }
}
"""
aws_amplify.data.query(operation, "ListItems")

# Create data with mutation
var create_operation = """
mutation CreateItem($input: CreateItemInput!) {
    createItem(input: $input) {
        id
        name
        description
    }
}
"""
aws_amplify.data.mutation(create_operation, "CreateItem", {
    "input": {
        "name": "Magic Sword",
        "description": "A powerful weapon"
    }
})
```

### Using UI Components

```gdscript
# Add the auth form to your scene
var auth_form = load("res://addons/aws-amplify/runtime/ui/auth_form.tscn").instantiate()
add_child(auth_form)

# Configure the form
auth_form.set_form_type("sign_in") # Options: sign_in, sign_up, confirm_sign_up, etc.

# Connect to signals
auth_form.connect("sign_in_success", Callable(self, "_on_sign_in_success"))
auth_form.connect("sign_in_error", Callable(self, "_on_sign_in_error"))
```

## Architecture

The plugin is organized in the same way as the [amplify-js](https://github.com/aws-amplify/amplify-js) client. The base class `AWSAmplify` contains several modules, each implementing specific features. You can access each module from the base class directly with the global variable `aws_amplify`.

### Module Overview

#### Client Module

This module offers basic features to send HTTP requests to AWS resources.

```gdscript
# Send a GET request
aws_amplify.client.get_json("https://api.example.com/endpoint", [], {})

# Send a POST request with JSON body
aws_amplify.client.post_json("https://api.example.com/endpoint", [], {"key": "value"})
```

[View Client Module Source](https://github.com/sligh-games/amplify-godot-engine-plugin/blob/main/addons/aws-amplify/runtime/lib/client.gd)

#### Authentication Module

This module provides comprehensive authentication features.

```gdscript
# Get user attributes
var user_attributes = aws_amplify.auth.get_user_attributes()

# Update user attributes
aws_amplify.auth.update_user_attribute("custom:level", "10")
```

[View Authentication Module Source](https://github.com/sligh-games/amplify-godot-engine-plugin/blob/main/addons/aws-amplify/runtime/lib/auth.gd)

#### Data Module

This module offers GraphQL features for data operations.

```gdscript
# Subscribe to real-time updates
aws_amplify.data.subscription(subscription_operation, "OnCreateItem")
```

[View Data Module Source](https://github.com/sligh-games/amplify-godot-engine-plugin/blob/main/addons/aws-amplify/runtime/lib/data.gd)

## API Reference

### Client Module

#### HTTP Requests (Raw)

- `get_(endpoint: String, headers: Array, body: String)`
- `post(endpoint: String, headers: Array, body: String)`
- `put(endpoint: String, headers: Array, body: String)`
- `delete(endpoint: String, headers: Array, body: String)`
- `send(endpoint: String, headers: Array, method: HTTPClient.Method, body: String)`

#### HTTP Requests (JSON)

- `get_json(endpoint: String, headers: Array, json_body: Dictionary)`
- `post_json(endpoint: String, headers: Array, json_body: Dictionary)`
- `put_json(endpoint: String, headers: Array, json_body: Dictionary)`
- `delete_json(endpoint: String, headers: Array, body: Dictionary)`
- `send_json(endpoint: String, headers: Array, method: HTTPClient.Method, json_body: Dictionary)`

### Authentication Module

#### Sign-Up

- `sign_up(username, password, options: Dictionary = {})`
- `confirm_sign_up(username: String, confirmation_code: String, options: Dictionary = {})`
- `resend_sign_up_code(username, options: Dictionary = {})`

#### Sign-In

- `sign_in(username, password, options: Dictionary = {})`
- `reset_password(username, options: Dictionary = {})`
- `confirm_reset_password(username, new_password, confirmation_code, options: Dictionary = {})`
- `update_password(old_password, new_password, options: Dictionary = {})`

#### Sign-Out

- `sign_out(global: bool = false)`
- `refresh_token(refresh_token)`

#### User Attributes

- `update_user_attributes(user_attributes: Dictionary, options: Dictionary = {})`
- `update_user_attribute(user_attribute_name: String, user_attribute_value, options: Dictionary = {})`
- `confirm_user_attribute(attribute_name: String, confirmation_code: String, options: Dictionary = {})`
- `send_user_attribute_confirmation_code(attribute_name: String, confirmation_code: String, options: Dictionary = {})`
- `delete_user_attributes(user_attribute_names: Array[String])`

#### Cached Variables Manipulation

- `get_token(name)`
- `get_user_attribute(name: String, refresh_attributes = false)`
- `get_user_attributes(refresh_attributes = false)`
- `add_user_attributes(user_attributes: Dictionary)`
- `remove_user_attributes(keys: Array)`
- `refresh_user(refresh_token = false, refresh_user_attributes = false)`

#### Authenticated HTTP Requests

- Various authenticated HTTP request methods (same signature as Client module)

### Data Module

- `query(operation, operation_name = "MyQuery", authenticated: bool = true)`
- `mutation(operation, operation_name = "MyMutation", authenticated: bool = true)`
- `subscription(operation, operation_name = "MySubscription", authenticated: bool = true)`
- `send(operation, operation_name, method: GraphQLMethod, authenticated: bool = true)`

## UI Components

The plugin offers sign-up, sign-in, and sign-out forms to handle various user authentication flows.

[View Auth Form Source](https://github.com/sligh-games/amplify-godot-engine-plugin/blob/main/addons/aws-amplify/runtime/ui/auth_form.gd)

For examples of how to use these forms, check our [sample repository](https://github.com/sligh-games/amplify-godot-engine-sample/tree/feature/auth_sign_in).

## Community

Join our community to get help, share ideas, and collaborate:

[![join sligh games discord](https://img.shields.io/discord/1371568283307868190?logo=discord&label=Sligh%20Games)](https://discord.gg/qN2q77zNDa)
[![join aws amplify discord](https://img.shields.io/discord/308323056592486420?logo=discord&label=AWS%20Amplify)](https://discord.gg/amplify)
[![join godot engine discord](https://img.shields.io/discord/1235157165589794909?logo=discord&label=Godot%20Engine)](https://discord.gg/godotengine)

For technical questions and feature discussions, visit our [GitHub Discussions](https://github.com/orgs/sligh-games/discussions).

## Security

If you discover a potential security issue, please DO NOT create a public GitHub issue. Instead, send an email directly to [security@sligh.games](mailto:security@sligh.games). This helps us address security vulnerabilities promptly and responsibly.

## Issues

If you encounter any issues with the plugin, [report a bug](https://github.com/sligh-games/amplify-godot-engine-plugin/issues/new?assignees=&labels=&projects=&template=bug_report.md&title=). If you have ideas for new features, [create a feature request](https://github.com/sligh-games/amplify-godot-engine-plugin/issues/new?assignees=&labels=&projects=&template=feature_request.md&title=).

## Contributing

We welcome contributions from the community! See [CONTRIBUTING](CONTRIBUTING.md) for more information on how to get involved.

## License

This library is licensed under the MIT License. See the [LICENSE](LICENSE.md) file for details.

## Third Party Licenses

See [THIRD_PARTY_LICENSES](THIRD_PARTY_LICENSES.md) for information about third-party components used in this project.
