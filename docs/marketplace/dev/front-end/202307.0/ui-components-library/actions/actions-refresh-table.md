---
title: Actions Refresh Table
description: This document provides details about the Actions Refresh Table service in the Components Library.
template: concept-topic-template
related:
  - title: Actions
    link: docs/marketplace/dev/front-end/page.version/ui-components-library/actions/index.html
  - title: Actions Close Drawer
    link: docs/marketplace/dev/front-end/page.version/ui-components-library/actions/actions-close-drawer.html
  - title: Actions Drawer
    link: docs/marketplace/dev/front-end/page.version/ui-components-library/actions/actions-drawer.html
  - title: Actions HTTP
    link: docs/marketplace/dev/front-end/page.version/ui-components-library/actions/actions-http.html
  - title: Actions Notification
    link: docs/marketplace/dev/front-end/page.version/ui-components-library/actions/actions-notification.html
  - title: Actions Redirect
    link: docs/marketplace/dev/front-end/page.version/ui-components-library/actions/actions-redirect.html
  - title: Actions Refresh Drawer
    link: docs/marketplace/dev/front-end/page.version/ui-components-library/actions/actions-refresh-drawer.html
  - title: Actions Refresh Parent Table
    link: docs/marketplace/dev/front-end/page.version/ui-components-library/actions/actions-refresh-parent-table.html
---

This document explains the Actions Refresh Table service in the Components Library.

## Overview

Actions Refresh Table is an Angular Service that refreshes data of the table in the current context.

Check out an example usage of the Actions Refresh Table.

Service configuration:

- `type`—an action type.  
- `tableId`—an `id` of the table that will be refreshed.  

```html
<spy-button-action
    [action]="{
        type: 'refresh-table',
        tableId: 'table-id',
    }"
>
</spy-button-action>
```

## Service registration

Register the service:

```ts
declare module '@spryker/actions' {
    interface ActionsRegistry {
        'refresh-table': RefreshTableActionHandlerService;
    }
}

@NgModule({
    imports: [
        ActionsModule.withActions({
            'refresh-table': RefreshTableActionHandlerService,
        }),
    ],
})
export class RootModule {}
```

## Interfaces

Below you can find interfaces for Actions Refresh Table:

```ts
export interface RefreshTableActionConfig extends ActionConfig {
    tableId?: string;
}
```
