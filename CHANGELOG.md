# Changelog

All notable changes to the AWS Amplify for Godot Engine Plugin will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]
### Added
- Upcoming features and improvements

## [0.3.3] - 2025-05-26
### Fixed
- Authentication flow in auth.gd by ensuring tokens are cleared before emitting signals
- Improved auth_form.gd with better initialization and error handling:
  - Added null check for sign_up visibility
  - Added auto-detection of aws_amplify singleton availability
  - Added automatic UI state handling based on sign-in status
  - Fixed token expiration time display using proper API
### Changed
- Updated scene references with UIDs for better compatibility
- Added LICENSE.md and README.md files to the plugin directory

## [0.3.2] - 2025-05-19
### Added
- Plugin icon for better visibility in Godot's plugin manager
### Changed
- Improved documentation and examples
### Fixed
- Minor bug fixes and performance improvements

## [0.3.1] - 2025-05-19
### Added
- Authentication module with comprehensive user management
  - Sign-up and sign-in flows
  - Password reset functionality
  - User attribute management
- Data module with GraphQL operations
  - Query support
  - Mutation support
  - Subscription capabilities
- Client module for AWS resource interaction
  - Raw HTTP requests
  - JSON-formatted requests
  - Authentication header handling
- UI Components
  - Ready-to-use authentication forms
  - Customizable form layouts
- Comprehensive documentation and examples

### Security
- Secure token management
- Protected user attribute handling
- Authenticated HTTP requests

## How to Upgrade
Please refer to our [documentation](https://docs.sligh.games/#!/en/amplify-godot) for detailed upgrade instructions between versions.

[Unreleased]: https://github.com/sligh-games/amplify-godot-engine-plugin/compare/v0.3.3...HEAD
[0.3.3]: https://github.com/sligh-games/amplify-godot-engine-plugin/compare/v0.3.2...v0.3.3
[0.3.2]: https://github.com/sligh-games/amplify-godot-engine-plugin/compare/v0.3.1...v0.3.2
[0.3.1]: https://github.com/sligh-games/amplify-godot-engine-plugin/releases/tag/v0.3.1
