# XcodeServer API Docs

> Unofficial documentation of the Xcode Server API (Xcode 7 edition).

**For the best browsing experience, please visit the interactive [documentation view at Apiary](http://docs.xcodeserverapidocs.apiary.io).**

We're using the [API Blueprint](https://apiblueprint.org) format, so feel free to contribute to the [apiary.apib](apiary.apib) file. There is also a snapshot of the interactive documentation in [docs.html](docs.html).

:mortar_board: Getting Started With Xcode Server 
---------------------------------
To find out how to set up Xcode Server on your Mac in minutes (and more), check out my [series of tutorials](http://honzadvorsky.com/pages/xcode_server_tutorials/).

# :thought_balloon: Purpose
Many of us like the [Xcode Server](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/xcode_guide-continuous_integration/) continuous integration tool. [Recently](https://developer.apple.com/videos/wwdc/2015/?id=410) it introduced an API which allows you to integrate it in your workflow. This API is however not yet fully documented, which this project attempts to fix.

This knowledge is used in [XcodeServerSDK](https://github.com/czechboy0/XcodeServerSDK), an unofficial SDK for talking to the Xcode Server API written in Swift, where you can get a good understanding of how to call many of the following APIs. This enables tools like [Buildasaur](https://github.com/czechboy0/Buildasaur), which allow for Xcode Server to be an even more powerful tool.

# :warning: Warning
Since there is no official documentation yet, calling APIs with bad parameters might brick your Xcode Server. Note that many of the API endpoints are used *internally* by Xcode Server, so it might not be smart to try everything. I will gradually document the tried and useful endpoints and warn against the more tricky ones. However, *I am in no way liable for what you do with this information*. I recommend to not experiment on your production Xcode Server and instead run a development Xcode Server on your development machine. There you can always reset everything with `sudo xcrun xcscontrol --reset`, which **deletes all** Xcode Server data including your setup bots and integration assets.

If you want to know more about reverse engineering how Xcode Server works under the hood, check out [my article](http://honzadvorsky.com/blog/2015/5/4/under-the-hood-of-xcode-server).

# :rocket: API Documentation

Endpoints with :white_check_mark: are fully documented in our [interactive documentation](http://docs.xcodeserverapidocs.apiary.io). Click on the section header (e.g. `Bots`) to jump to the documentation. Below is a list of API endpoints we're aiming to document.

All the following API endpoints are **JSON based**. 

For more restricted actions like creating a bot, you need to use [Basic authentication](https://en.wikipedia.org/wiki/Basic_access_authentication). Such request has to contain a header like this

```
Authorization: Basic aGVsbG93b3JsZDpzZWNyZXRwYXNzd29yZA==
```
where `aGVsbG93b3JsZDpzZWNyZXRwYXNzd29yZA==` is just `username` and `password`, concatenated by `:` and [base64](https://en.wikipedia.org/wiki/Base64) encoded.

## Assets

- `GET /integrations/:id/assets`
- `GET /integrations/:id/install_product`
- `GET /integrations/:id/:token/install_manifest.plist`
- `GET /assets/token/:token/*`
- `GET /assets/*`
- `GET /profiles/ota.mobileconfig`
- `GET /integrations/:id/files`
- `POST /integrations/:id/files`
- `PUT /files/:id/upload`

## Authentication ([use cases](https://github.com/czechboy0/XcodeServerSDK/blob/swift-2/XcodeServerSDK/API%20Routes/XcodeServer%2BAuth.swift))

- `POST /auth/login`
- `POST /auth/force_login`
- `POST /auth/logout`
- `GET /auth/islogged`
- `GET /auth/isBotCreator`

## [Bots](http://docs.xcodeserverapidocs.apiary.io/#reference/bots) ([use cases](https://github.com/czechboy0/XcodeServerSDK/blob/swift-2/XcodeServerSDK/API%20Routes/XcodeServer%2BBot.swift))

- :white_check_mark: `POST /bots`
- :white_check_mark: `GET /bots`
- :white_check_mark: `GET /bots/:id`
- `PATCH /bots/:id`
- :white_check_mark: `DELETE /bots/:id/:rev`
- :white_check_mark: `DELETE /bots`
- :white_check_mark: `GET /bots/:id/stats`

## Code Coverage

- `POST /code_coverage/bulk_import`
- `GET /code_coverage/integration/:id`
- `POST /code_coverage/integration/keypath`

## Devices ([use cases](https://github.com/czechboy0/XcodeServerSDK/blob/swift-2/XcodeServerSDK/API%20Routes/XcodeServer%2BDevice.swift))

- `POST /devices`
- `GET /devices`
- `GET /devices/server`
- `GET /devices/:id`
- `PATCH /devices/:id`
- `DELETE /devices/:id/:rev`
- `DELETE /devices`

## [Integrations](http://docs.xcodeserverapidocs.apiary.io/#reference/integrations) ([use cases](https://github.com/czechboy0/XcodeServerSDK/blob/swift-2/XcodeServerSDK/API%20Routes/XcodeServer%2BIntegration.swift))

- :white_check_mark: `POST /bots/:id/integrations`
- :white_check_mark: `GET /bots/:id/integrations/count`
- :white_check_mark: `GET /bots/:id/integrations/:filter?`
- `GET /integrations`
- `GET /integrations/orphaned`
- `GET /integrations/running`
- `GET /integrations/:id`
- `PATCH /integrations/:id`
- `DELETE /integrations`
- `POST /integrations/bulk_import_tests`
- `GET /integrations/:id/test/:keyPath/:deviceIdentifier?`
- `POST /integrations/:id/test/batch/:deviceIdentifier?`
- `POST /integrations/:id/commits`
- `GET /integrations/:id/commits`
- `POST /integrations/:id/cancel`
- `POST /integrations/:id/request`
- `POST /integrations/:id/tags`
- `DELETE /integrations/:id/tags`
- `DELETE /integrations/:id/:rev`
- `GET /integrations/:id/tests_for_device/:did`
- `GET /integrations/filter/tag/:tag/:bots?`
- `GET /integrations/filter/:filter/:bots?`
- `POST /integrations/bulk-import-integrations`

## Issues

- `GET /integrations/:id/issues`
- `POST /integrations/:id/issues`
- `POST /integrations/:id/bulk_issues`
- `POST /integrations/:id/issues/:issueID/silence`
- `POST /integrations/:id/issues/:issueID/unsilence`
- `POST /integrations/:id/issues/:issueID/associations`
- `DELETE /integrations/:id/issues/:issueID/associations`

## Misc

- `DELETE /unittests`
- `GET /unittests/cleanup`
- `GET /ping`
- `GET /hostname`
- `GET /maintenance-tasks`

## Notification

- `POST /integrations/:id/notifications`
    
## Platform ([use cases](https://github.com/czechboy0/XcodeServerSDK/blob/swift-2/XcodeServerSDK/API%20Routes/XcodeServer%2BPlatform.swift))

- `POST /platforms`
- `GET /platforms`

## Repositories ([use cases](https://github.com/czechboy0/XcodeServerSDK/blob/swift-2/XcodeServerSDK/API%20Routes/XcodeServer%2BRepository.swift))

- `GET /repositories`
- `POST /repositories`

## Source Control Management ([use cases](https://github.com/czechboy0/XcodeServerSDK/blob/swift-2/XcodeServerSDK/API%20Routes/XcodeServer%2BSCM.swift))

- `POST /bots/preflight` (depricated)
- `POST /scm/preflight`
- `POST /scm/branches`
- `POST /bots/:id/reflight`
- `POST /bots/:id/branches`
- `GET /bots/:id/blueprint`
- `GET /integrations/:id/blueprint`

## Settings

- `GET /settings`
- `GET /settings/list`
- `PATCH /settings/:id`
- `DELETE /settings/:id/:rev`
- `DELETE /settings`
- `POST /settings/service/enable`
- `POST /settings/service/disable`

## Users

- `GET /users/:name/canCreateRepositories`
- `GET /users/:name/canViewBots`
- `GET /users/:name/canCreateBots`
- `GET /users/canAnyoneCreateRepositories`
- `GET /users/canAnyoneViewBots`
- `GET /users/canAnyoneCreateBots`

## Versions

- `POST /versions`
- `GET /versions`
- `GET /versions/list`
- `PATCH /versions/:id`
- `DELETE /versions/:id/:rev`
- `DELETE /versions`

# :pencil2: Contributing
Yes! Great! Create a Pull Request :+1:

# :v: License
MIT

# :alien: Author
Honza Dvorsky
[honzadvorsky.com](http://honzadvorsky.com)
[@czechboy0](https://twitter.com/czechboy0)


