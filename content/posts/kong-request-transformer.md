+++
title = "Kong Request Transformer"
author = ["Derek"]
date = 2025-06-30
draft = false
+++

Usecase: A new service had to return json responses in different key case formats. Some endpoints were returning responses in `kebab-case` while others were returning in the more common `camelCase` format.

We went with a solution where we defaulted to `camelCase` as the default JSON marshaling format in the response. For the `kebab-case` endpoints the idea was to force a `Content-Type` header that would signal the alternate casing. This was logic that was added on our Kong request gateway/load balancer. The service would return the response format accordingly based on that header.

This was what I configured initially:

```nil
Add - For adding the `Content-Type` header when the it is not present in the request
```

When testing on integration I realised the above was not enough to handle requests when the `Content-Type` was set. I realised that I also needed the `Replace` configuration, to cover the case when the caller has already specified the header and we want to overwrite that.

```nil
Replace - For replacing the `Content-Type` header if it is present in the request
```

****TIL****: I needed both \`add\` and \`replace\` specified in the Kong ACL to force a specific \`Content-Type\`, regardless of whether the header was specified by the caller or not.

Ref: [Request Transformer Plugin - Kong Docs](https://developer.konghq.com/plugins/request-transformer)
