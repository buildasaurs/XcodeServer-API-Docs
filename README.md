# XcodeServer API Docs

> Unofficial documentation of the Xcode Server API (Xcode 7 edition).

**This is Work In Progress, more documentation is being added over time**

# :thought_balloon: Purpose
Many of us like the [Xcode Server](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/xcode_guide-continuous_integration/) continuous integration tool. [Recently](https://developer.apple.com/videos/wwdc/2015/?id=410) it introduced an API which allows you to integrate it in your workflow. This API is however not yet fully documented, which this project attempts to fix.

This knowledge is used in [XcodeServerSDK](https://github.com/czechboy0/XcodeServerSDK), an unofficial SDK for talking to the Xcode Server API written in Swift. This enables tools like [Buildasaur](https://github.com/czechboy0/Buildasaur), which allow for Xcode Server to be an even more powerful tool.

# :warning: Warning
Since there is no official documentation yet, calling APIs with bad parameters might brick your Xcode Server. Note that many of the API endpoints are used *internally* by Xcode Server, so it might not be smart to try everything. I will gradually document the tried and useful endpoints and warn against the more tricky ones. However, *I am in no way liable for what you do with this information*. I recommend to not experiment on your production Xcode Server and instead run a development Xcode Server on your development machine. There you can always reset everything with `sudo xcrun xcscontrol --reset`, which **deletes all** Xcode Server data including your setup bots and integration assets.

If you want to know more about reverse engineering how Xcode Server works under the hood, check out [my article](https://honzadvorsky.com/blog/2015/5/4/under-the-hood-of-xcode-server).

# :rocket: API Documentation

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

## Authentication

- `POST /auth/login`
- `POST /auth/force_login`
- `POST /auth/logout`
- `GET /auth/islogged`
- `GET /auth/isBotCreator`

## Bots

- `POST /bots`
- `GET /bots`
- `GET /bots/:id`
- `PATCH /bots/:id`
- `DELETE /bots/:id/:rev`
- `DELETE /bots`
- `GET /bots/:id/stats`

## Code Coverage

- `POST /code_coverage/bulk_import`
- `GET /code_coverage/integration/:id`
- `POST /code_coverage/integration/keypath`

## Devices

- `POST /devices`
- `GET /devices`
- `GET /devices/server`
- `GET /devices/:id`
- `PATCH /devices/:id`
- `DELETE /devices/:id/:rev`
- `DELETE /devices`

## Integrations

- `POST /bots/:id/integrations`
- `GET /bots/:id/integrations/count`
- `GET /bots/:id/integrations/:filter?`
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
    
## Platform

- `POST /platforms`
- `GET /platforms`

## Repositories

- `GET /repositories`
- `POST /repositories`

## Source Control Management

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

# :pencil2: Contributing
Yes! Great! Create a Pull Request :+1:

# :v: License
MIT

# :alien: Author
Honza Dvorsky
[honzadvorsky.com](http://honzadvorsky.com)
[@czechboy0](https://twitter.com/czechboy0)


