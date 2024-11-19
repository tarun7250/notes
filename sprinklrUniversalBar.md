# UniversalBar



## universalBar layout






## Actionbar

### UniversalSearchButton
### LaunchPadButton
### QuickCreateWrapper

### NotificationButton
# NotificationButton
- `NotificationButton.tsx` 
```ts 
trigger({
      id: 'OPEN_NOTIFICATIONS_PANE',
      templateId: 'OPEN_NOTIFICATIONS_PANE',
 });
```

- `useButton.ts`
```ts
const onAction = ({ type, payload }) => {
    if (type === 'SET_STATUS') setStatus(payload.status);
}

const trigger = (action, target, payload) => {
    trigger({ action, target, payload }, onAction);
    actionIdRef.current = action.id;
}
```
- `ButtonsActionsProvider.tsx` - handler has trigger, activebuttionactions is the action
```ts
  const [activeButtonActions, handlers] = useButtonActionsState(buttonActions, parentHandlers);
```

- `useButtonActionsState` 
```ts
const trigger = (actionDetails, onAction ) => {
      const actionId = actionDetails.action.id;
      if (actionTypeToComponent[actionDetails.action.templateId]) {
        setActions(prevActions => new Map(prevActions).set(actionId, { onAction, ...actionDetails }));
        onAction({ type: 'SET_STATUS', payload: { status: 'loading', actionId } });
      } else if (!parentHandlers) {
        log.error(`Not able to find any button action with templateId: ${actionDetails.action.templateId}`);
      } else {
        parentHandlers?.trigger(actionDetails, onAction);
      }
}
```
- `ButtonActionsProvide.tsx`
```js


<Root actionTypeToComponent={buttonActions} actionHandlers={handlers} actions={activeButtonActions} {...rootProps/}>//activeButtonActions is action from setAction


const [Root, rootProps] = useOverrides(overrides?.Root, DefaultRoot);// spaceweb component

```
trigger contained in handler 



### AvatarButton


# study overrides
https://spaceweb.netlify.app/guides/understanding-overrides

notification.eventType


vs adaptermap

DASHBOARD_SHARED


- `NotificationListContainer.tsx` - 
```js
<NotificationList state={notificationState} onAction={onAction} getNotification={getNotification} />
```

- `virality-apps > templates > Notifications > Notifications.tsx` calling `NotificationList.tsx`
- `TemplatePageContainer.tsx (templateId: NOTIFICATIONS) > Suspense > Wrapped >  Notifications`
-  


{
  "variant": "CONTEXTUAL_PANE",
  "templateId": "NOTIFICATIONS",
  "activeView": {
    "templateId": "NOTIFICATIONS"
  },
  "onAction": "() => {}",
  "canGo": "canGo() {}",
  "viewParams": {
    "templateId": "NOTIFICATIONS"
  },
  "overrides": {}
}

variant: PageVariant;
  templateId: TemplateId;
  activeView: TemplateViewParams;
  onAction: OnAction<T>;
  canGo: (n: number) => boolean;
  viewParams: Omit<TemplateViewParams, 'queryParams'> & { routeState?: Spr.StringAnyMap } & Spr.StringAnyMap;
  overrides?: Spr.StringAnyMap;
  children?: React.ReactNode;


# in profile -  WithTabActions
- `NotificationButtonAction` - `openThirdPane(thirdPanePath);`
- `useThirdPane` - `ViralityViewContext.useContainer();` -> `open` - `openThirdPane`
- `useViralityViewState` - 
```js
  const open = useLatestCallback<ViralityViewState['open']>((_routeToSet, state?: Spr.StringAnyMap) => {
    const { route: prevRoute, state: prevState } = localStorageState ?? EMPTY_OBJECT_READONLY;
    const isRouteSetInLocalStorage = !!prevRoute;

    if (isRouteSetInLocalStorage && _routeToSet === prevRoute && _isEqual(state, prevState)) {
      const { routingParams } = getViralityParamsFromRoute(_routeToSet);
      publish(SYSTEM_EVENTS.VIRALITY_SWITCH_VIEW, {
        viewStateParams: state,
        ...routingParams,
      });
    } else {
      onAction({
        type: ACTIONS.OPEN_VIRALITY_PANE,
        payload: { route: _routeToSet, state },
      });
    }
  });
```


# entry point
- `AppTitle` -> NextDocumentTitle as DocumentTitle
- `SpaceApp.tsx` -> AppTitle
-  `NextDocumentTitle.tsx` -> `Head` , `props` isme virality 
```js
{
    "isOn": true,
    "route": "/template/NOTIFICATIONS"
}
```
- `props.children` -> `withTabActions.tsx` having same virality kv in props
- `WrappedComponents`
- `withPaidModule`, `withUserConfig`
- `withStyles.js` -> `WrappedComponent` -> props virality
- `withTabState.js` -> props virality
- 

/**
 * Author: Sahil
 * Created on: 9/4/19
 * Description: Common App component for old and new composer
 */
 - `App.js`
 - `withVirality.tsx`
 <!-- - `/src/components/quickViews/connectQuickView/components/quickView/index.tsx` return null
 - `BgUploadProgressBox.tsx` return null -->

# on first load 
- `ClassicApp.tsx` -> `<SpaceAppViralityContainer />`


# after
- `SpaceAppViralityContainer.tsx` - 
```js
//on later clicks only isOn and path will be changing
return isOn && path ? (
    <Suspense fallback={null}>
      <ViralityShellContainer
)
```
- `ViralityShellContainer.tsx` - `later chunk ViralityShellContainer`
- `ViralityShell.tsx`
 - `inside ViralityAppContainer` `./src/virality-app/ViralityApp.tsx` - `webpackChunkName: "virality-app"` history -> location -> 
 - `TemplatePageRoute.tsx`
 - `TemplatePageContainer.tsx` -> `LazyPage` by `getTemplatePage(templateId)` -> templateId: "NOTIFICATIONS", variant: "CONTEXTUAL_PLANE"
 - `./src/virality-app/factories/pages/templates/standard.ts` -> `/* webpackChunkName: "notifications-template-page" */ 'virality-app/templates/notifications'`

 - `Notifications.tsx` - `/src/virality-app/templates/notifications/Notifications.tsx`
 .... NotificationList .....



 ## mischellaneous
 - `Errorboundary.tsx`
 - `SplitView.tsx` -> virality
 - `ClientOnly.tsx` -> only children render

 