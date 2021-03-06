# angular-busy2 [Live Demo](https://tiberiuzuld.github.io/angular-busy)

[![npm version](https://badge.fury.io/js/angular-busy2.svg)](https://badge.fury.io/js/angular-busy2)
[![dependencies Status](https://david-dm.org/tiberiuzuld/angular-busy2/status.svg)](https://david-dm.org/tiberiuzuld/angular-busy2)
[![devDependencies Status](https://david-dm.org/tiberiuzuld/angular-busy2/dev-status.svg)](https://david-dm.org/tiberiuzuld/angular-busy2?type=dev)
[![downloads](https://img.shields.io/npm/dm/angular-busy2.svg)](https://www.npmjs.com/package/angular-busy2)
[![Donate](https://img.shields.io/badge/Donate-PayPal-green.svg)](https://www.paypal.me/tiberiuzuld)

> Show busy/loading indicators on Observable, Subscription, Promise, Boolean, Number

### Note Requires Angular5 for [AngularJS 1 branch 1.x](https://github.com/tiberiuzuld/angular-busy/tree/1.x)
## Getting Started

Install with npm.

```bash
npm install angular-busy2 --save
```

Add `CgBusyModule` as a module dependency for your module.

```typescript
import {CgBusyModule} from 'angular-busy2';
@NgModule({
 imports: [
   CgBusyModule
 ]
});
```

## Options

The `[cgBusy]` directive expects any Observable, Subscription, Promise, Boolean, Number and optional `[cgBusyConfig]` configuration object.

In other words.  You may do this:

```html
<div [cgBusy]="promise"></div>
```

or this:

```html
<div [cgBusy]="promise"
[cgBusyConfig]="{templateRef: customTemplate, message:message, backdrop:backdrop, delay:delay, minDuration:minDuration}"></div>
```

* `promise` - Required. The promise/Observables (or array of promises/Observables) that will cause the busy indicator to show. Also supports boolean and numbers (truthy values will show loading...)
* `message` - Optional.  Defaults to 'Please Wait...'.  The message to show in the indicator.  This value may be updated while the promise is active.  The indicator will reflect the updated values as they're changed.
* `backdrop` - Optional. Boolean, default is true. If true a faded backdrop will be shown behind the progress indicator.
* `templateRef` - Optional.  If provided, the given template will be shown in place of the default progress indicator template.
* `delay` - Optional.  The amount of time to wait until showing the indicator.  Defaults to 0.  Specified in milliseconds.
* `minDuration` - Optional.  The amount of time to keep the indicator showing even if the promise was resolved quicker.  Defaults to 0.  Specified in milliseconds.
* `wrapperClass` - Optional.  The name(s) of the CSS classes to be applied to the wrapper element of the busy sign/animation.  Defaults to `undefined`.  Typically only useful if you wish to apply different positioning to the animation.

## Overriding Defaults

The default values for `message`, `backdrop`, `templateRef`, `delay`, and `minDuration` may all be overridden by overriding the `CgBusyDefaults`, like so:

```typescript
import {CgBusyDefaults} from 'angular-busy2';
  
  @ViewChild('customTemplate')
  private customTemplateTpl: TemplateRef<any>;

  constructor(private busyDefaults: CgBusyDefaults) {
    this.busyDefaults.delay = 5000;
  }

  ngOnInit() {
    this.busyDefaults.templateRef = this.customTemplateTpl;
  }
```

```html
<ng-template #customTemplate let-options="options">
  <div class="custom-template">
    <div class="custom-message" [innerHtml]="options.message"></div>
  </div>
</ng-template>
```

Only the values you'd like overridden need to be specified.

> Fork from original angular-busy (cgBusy) https://github.com/cgross/angular-busy  
