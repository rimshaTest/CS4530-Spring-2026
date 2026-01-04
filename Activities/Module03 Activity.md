---
layout: page
title: Messing With APIs
nav_exclude: true
---

If you go to [this URL](https://name-seeing-server.onrender.com/) your browser makes an HTTP GET request that will get a JSON response. That URL also accepts HTTP POST requests containing JSON data. The server at that URL also doesn’t correctly validate its input. Being able to [see the source code](https://github.com/neu-se/name-seeing-server/blob/main/server.ts) will make this app easy to attack.

This activity involves understanding the server by reading the woefully uncommented code and interacting with it with HTTP requests. One way to do this is with [Postman] XXX LINK. You’ll also try your hand at using [Zod](https://zod.dev/api?id=objects) to describe the desired shape of input in a way that — unlike TypeScript types — can actually check whether inputs have the right shape.

You’ll hand in your assignment as a single TypeScript file `handin.ts` as required by your instructor. The template is [here](https://github.com/neu-se/name-seeing-server/blob/main/handin.ts). If you go to <https://github.com/neu-se/name-seeing-server>, find the green "Use this template" button, and select "Open in a codespace," you can edit the `handin.ts` in your browser.
