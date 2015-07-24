# XcodeServer-API-Docs
Unofficial documentation of the Xcode Server API (Xcode 7 edition).

**This is still Work In Progress**

# :thought_balloon: Purpose
Many of us like the Xcode Server continuous integration tool, which allows you to integrate it in your workflow with an API. This API is however not yet properly documented, which this project attempts to fix.

# :warning: Warning
Since there is no official documentation yet, calling APIs with bad parameters might brick your Xcode Server. I am in no way liable for what you do with this information. I recommend to not experiment at your production Xcode Server and instead run a development Xcode Server on your development machine. There you can always reset everything with `sudo xcrun xcscontrol --reset`.

If you want to know more about reverse engineering how Xcode Server works under the hood, check out [my article](https://honzadvorsky.com/blog/2015/5/4/under-the-hood-of-xcode-server).

# :rocket: API Documentation

## Bots

- `POST /bots`
- `GET /bots`
- `GET /bots/:id`
- `PATCH /bots/:id`
- `DELETE /bots/:id/:rev`
- `DELETE /bots`
- `GET /bots/:id/stats`

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

# :pencil2: Contributing
Yes! Great! Create a Pull Request :+1:

# :v: License
MIT

# :alien: Author
Honza Dvorsky
[honzadvorsky.com](http://honzadvorsky.com)
[@czechboy0](https://twitter.com/czechboy0)


