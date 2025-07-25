---
title: declarativeNetRequest.updateDynamicRules
slug: Mozilla/Add-ons/WebExtensions/API/declarativeNetRequest/updateDynamicRules
page-type: webextension-api-function
browser-compat: webextensions.api.declarativeNetRequest.updateDynamicRules
sidebar: addonsidebar
---

Modifies the set of dynamic rules for the extension. The rules with IDs listed in `options.removeRuleIds` are first removed, and then the rules given in `options.addRules` are added. Note that:

- This update happens as an atomic operation: either all specified rules are added and removed, or an error is returned.
- These rules are persisted across browser sessions and across extension updates.
- Static rules specified as part of the extension package can not be removed using this function.
- The number of dynamic rules that can be added is limited:
  - In Safari and up to Chrome 119, to the value of {{WebExtAPIRef("declarativeNetRequest.MAX_NUMBER_OF_DYNAMIC_AND_SESSION_RULES","MAX_NUMBER_OF_DYNAMIC_AND_SESSION_RULES")}} for the combined total of dynamic and session-scoped rules.
  - Up to Firefox 127 to the value of {{WebExtAPIRef("declarativeNetRequest.MAX_NUMBER_OF_DYNAMIC_AND_SESSION_RULES","MAX_NUMBER_OF_DYNAMIC_AND_SESSION_RULES")}}.
  - From Chrome 120 and Firefox 128, to the value of {{WebExtAPIRef("declarativeNetRequest.MAX_NUMBER_OF_DYNAMIC_RULES","MAX_NUMBER_OF_DYNAMIC_RULES")}}.

> [!NOTE]
> In Firefox 132 and earlier, dynamic rules are sometimes not applied after a browser restart, and calls to this API are rejected with an error ([Firefox bug 1921353](https://bugzil.la/1921353)). A workaround is to specify an enabled static ruleset in the [`declarative_net_request`](/en-US/docs/Mozilla/Add-ons/WebExtensions/manifest.json/declarative_net_request) manifest key. The ruleset file can be an empty list.

## Syntax

```js-nolint
let rulesUpdated = browser.declarativeNetRequest.updateDynamicRules(
    options                // object
);
```

### Parameters

- `options`
  - : An object containing details of the rules to add or delete from the dynamic rules.
    - `addRules` {{optional_inline}}
      - : An array of {{WebExtAPIRef("declarativeNetRequest.Rule")}}. Details of the rules to add.
    - `removeRuleIds` {{optional_inline}}
      - : An array of `number`. IDs of the rules to remove. Any invalid IDs are ignored.

### Return value

A [`Promise`](/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) If the request was successful, the promise is fulfilled with no arguments. If the request fails, the promise is rejected with an error message.

## Examples

{{WebExtExamples}}

## Browser compatibility

{{Compat}}

<!--
// Copyright 2015 The Chromium Authors. All rights reserved.
//
// Redistribution and use in source and binary forms, with or without
// modification, are permitted provided that the following conditions are
// met:
//
//    * Redistributions of source code must retain the above copyright
// notice, this list of conditions and the following disclaimer.
//    * Redistributions in binary form must reproduce the above
// copyright notice, this list of conditions and the following disclaimer
// in the documentation and/or other materials provided with the
// distribution.
//    * Neither the name of Google Inc. nor the names of its
// contributors may be used to endorse or promote products derived from
// this software without specific prior written permission.
//
// THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
// "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
// LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR
// A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT
// OWNER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
// SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT
// LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE,
// DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY
// THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
// (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
// OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
-->
