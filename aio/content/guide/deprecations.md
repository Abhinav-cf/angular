# Deprecated APIs and features

Angular strives to balance innovation and stability.
Sometimes, APIs and features become obsolete and need to be removed or replaced so that Angular can stay current with new best practices, changing dependencies, or changes in the (web) platform itself.

To make these transitions as easy as possible, we deprecate APIs and features for a period of time before removing them. This gives you time to update your applications to the latest APIs and best practices.

This guide contains a summary of all Angular APIs and features that are currently deprecated.

<div class="alert is-helpful">

Features and APIs that were deprecated in v6 or earlier are candidates for removal in version 9 or any later major version. For information about Angular's deprecation and removal practices, see [Angular Release Practices](guide/releases#deprecation-practices "Angular Release Practices: Deprecation practices").

For step-by-step instructions on how to update to the latest Angular release, use the interactive update guide at [update.angular.io](https://update.angular.io).

</div>

## Index

To help you future-proof your projects, the following table lists all deprecated APIs and features, organized by the release in which they are candidates for removal. Each item is linked to the section later in this guide that describes the deprecation reason and replacement options.

<!--
deprecation -> removal cheat sheet
v4 - v7
v5 - v8
v6 - v9
v7 - v10
v8 - v11
v9 - v12
v10 - v13
v11 - v14
v12 - v15
v13 -> v16
-->

| Area                      | API or Feature                                                                                | May be removed in     |
|:---                       |:---                                                                                           |:---                   |
| `@angular/common`         | [`ReflectiveInjector`](#reflectiveinjector)                                                   | <!--v8--> v11         |
| `@angular/common`         | [`CurrencyPipe` - `DEFAULT_CURRENCY_CODE`](api/common/CurrencyPipe#currency-code-deprecation) | <!--v9--> v11         |
| `@angular/common/http`    | [`XhrFactory`](api/common/http/XhrFactory)                                                    | <!--v12--> v15        |
| `@angular/core`           | [`DefaultIterableDiffer`](#core)                                                              | <!--v7--> v11         |
| `@angular/core`           | [`ReflectiveKey`](#core)                                                                      | <!--v8--> v11         |
| `@angular/core`           | [`RenderComponentType`](#core)                                                                | <!--v7--> v11         |
| `@angular/core`           | [Factory-based signature of `ApplicationRef.bootstrap`](#core)                                | <!--v13--> v15        |
| `@angular/core`           | [`PlatformRef.bootstrapModuleFactory`](#core)                                                 | <!--v13--> v15        |
| `@angular/core`         | [`getModuleFactory`](#core)                                                                       | <!--v13--> v16        |
| `@angular/core`         | [`ModuleWithComponentFactories`](#core)                                                                       | <!--v13--> v16        |
| `@angular/core`         | [`Compiler`](#core)                                                                       | <!--v13--> v16        |
| `@angular/core`         | [`CompilerFactory`](#core)                                                                       | <!--v13--> v16        |
| `@angular/core`         | [`NgModuleFactory`](#core)                                                                       | <!--v13--> v16        |
| `@angular/platform-browser-dynamic`         | [`JitCompilerFactory`](#platform-browser-dynamic)                                                                       | <!--v13--> v16        |
| `@angular/forms`          | [`ngModel` with reactive forms](#ngmodel-reactive)                                            | <!--v6--> v11         |
| `@angular/upgrade`        | [`@angular/upgrade`](#upgrade)                                                                | <!--v8--> v11         |
| `@angular/upgrade`        | [`getAngularLib`](#upgrade-static)                                                            | <!--v8--> v11         |
| `@angular/upgrade`        | [`setAngularLib`](#upgrade-static)                                                            | <!--v8--> v11         |
| template syntax           | [`<template>`](#template-tag)                                                                 | <!--v7--> v11         |
| polyfills                 | [reflect-metadata](#reflect-metadata)                                                         | <!--v8--> v11         |
| npm package format        | [`esm5` and `fesm5` entry-points in @angular/* npm packages](guide/deprecations#esm5-fesm5)   | <!-- v9 --> v11       |
| `@angular/compiler-cli`   | [Input setter coercion](#input-setter-coercion)                                               | <!--v13--> v15        |
| `@angular/compiler-cli` | [`fullTemplateTypeCheck`](#full-template-type-check)                                          | <!--v13--> v15        |
| `@angular/core`           | [`defineInjectable`](#core)                                                                   | <!--v8--> v11         |
| `@angular/core`           | [`entryComponents`](api/core/NgModule#entryComponents)                                        | <!--v9--> v11         |
| `@angular/core`           | [`ANALYZE_FOR_ENTRY_COMPONENTS`](api/core/ANALYZE_FOR_ENTRY_COMPONENTS)                       | <!--v9--> v11         |
| `@angular/core`           | [Factory-based signature of `ViewContainerRef.createComponent`](api/core/ViewContainerRef#createComponent) | <!--v13--> v15         |
| `@angular/core/testing`   | [`TestBed.get`](#testing)                                                                     | <!--v9--> v12         |
| `@angular/core/testing`   | [`async`](#testing)                                                                           | <!--v9--> v12         |
| `@angular/core/testing`   | [`aotSummaries` argument in `TestBed.initTestEnvironment`](#testing)                          | <!--v13--> v14        |
| `@angular/core/testing`   | [`aotSummaries` field of the `TestModuleMetadata` type](#testing)                             | <!--v13--> v14        |
| `@angular/forms`          | [`FormBuilder.group` legacy options parameter](api/forms/FormBuilder#group)                   | <!--v11--> v14        |
| `@angular/platform-server`| [`renderModuleFactory`](#platform-server)                                                     | <!--v13--> v15        |
| `@angular/service-worker` | [`SwUpdate#activated`](api/service-worker/SwUpdate#activated)                                 | <!--v13--> v16        |
| `@angular/service-worker` | [`SwUpdate#available`](api/service-worker/SwUpdate#available)                                 | <!--v13--> v16        |
| template syntax           | [`/deep/`, `>>>`, and `::ng-deep`](#deep-component-style-selector)                            | <!--v7--> unspecified |
| template syntax         | [`bind-`, `on-`, `bindon-`, and `ref-`](#bind-syntax)                            | <!--v13--> v15 |

For information about Angular CDK and Angular Material deprecations, see the [changelog](https://github.com/angular/components/blob/master/CHANGELOG.md).

## Deprecated APIs

This section contains a complete list all of the currently-deprecated APIs, with details to help you plan your migration to a replacement.

<div class="alert is-helpful">

**TIP**: In the [API reference section](api) of this site, deprecated APIs are indicated by ~~strikethrough.~~ You can filter the API list by [**Status: deprecated**](api?status=deprecated).

</div>

{@a common}

### @angular/common

| API                                                                                           | Replacement                                         | Deprecation announced | Notes                                                                                                     |
| :---                                                                                          |:---                                                 |:---                   |:---                                                                                                       |
| [`CurrencyPipe` - `DEFAULT_CURRENCY_CODE`](api/common/CurrencyPipe#currency-code-deprecation) | `{provide: DEFAULT_CURRENCY_CODE, useValue: 'USD'}` | v9                    | From v11 the default code will be extracted from the locale data given by `LOCALE_ID`, rather than `USD`. |

{@a common-http}

### @angular/common/http

| API                                        | Replacement                       | Deprecation announced | Notes                                                                        |
|:---                                        |:---                               |:---                   |:---                                                                          |
| [`XhrFactory`](api/common/http/XhrFactory) | `XhrFactory` in `@angular/common` | v12                   | The `XhrFactory` has moved from `@angular/common/http` to `@angular/common`. |

{@a core}

### @angular/core

| API                                                                                | Replacement                                                                        | Deprecation announced | Notes                                                                                                                                                                                                                                    |
|:---                                                                                |:---                                                                                |:---                   |:---                                                                                                                                                                                                                                      |
| [`DefaultIterableDiffer`](api/core/DefaultIterableDiffer)                          | n/a                                                                                | v4                    | Not part of public API.                                                                                                                                                                                                                  |
| [`ReflectiveInjector`](api/core/ReflectiveInjector)                                | `{@link Injector#create Injector.create()}`                                        | v5                    | See [`ReflectiveInjector`](#reflectiveinjector)                                                                                                                                                                                          |
| [`ReflectiveKey`](api/core/ReflectiveKey)                                          | none                                                                               | v5                    | none                                                                                                                                                                                                                                     |
| [`defineInjectable`](api/core/defineInjectable)                                    | `ɵɵdefineInjectable`                                                               | v8                    | Used only in generated code. No source code should depend on this API.                                                                                                                                                                   |
| [`entryComponents`](api/core/NgModule#entryComponents)                             | none                                                                               | v9                    | See [`entryComponents`](#entryComponents)                                                                                                                                                                                                |
| [`ANALYZE_FOR_ENTRY_COMPONENTS`](api/core/ANALYZE_FOR_ENTRY_COMPONENTS)            | none                                                                               | v9                    | See [`ANALYZE_FOR_ENTRY_COMPONENTS`](#entryComponents)                                                                                                                                                                                   |
| [`async`](api/core/testing/async)                                                  | [`waitForAsync`](api/core/testing/waitForAsync)                                    | v11                   | The [`async`](api/core/testing/async) function from `@angular/core/testing` has been renamed to `waitForAsync` in order to avoid confusion with the native JavaScript <code class="no-auto-link">async</code> syntax. The existing function is deprecated and will be removed in a future version. |
| [`getModuleFactory`](api/core/getModuleFactory)                                            | [`getNgModuleById`](api/core/getNgModuleById)                                                                               | v13                   | Ivy allows working with NgModule classes directly, without retrieving corresponding factories.                                                                                                                                                                                             |
| `ViewChildren.emitDistinctChangesOnly` / `ContentChildren.emitDistinctChangesOnly` | none (was part of [issue #40091](https://github.com/angular/angular/issues/40091)) |                       | This is a temporary flag introduced as part of bugfix of [issue #40091](https://github.com/angular/angular/issues/40091) and will be removed.                                                                                            |
| Factory-based signature of [`ApplicationRef.bootstrap`](api/core/ApplicationRef#bootstrap)                          | Type-based signature of [`ApplicationRef.bootstrap`](api/core/ApplicationRef#bootstrap)                                                                                 | v13                    | With Ivy, there is no need to resolve Component factory and Component Type can be provided directly.                                                                                                                                                                                                                  |
| [`PlatformRef.bootstrapModuleFactory`](api/core/PlatformRef#bootstrapModuleFactory)                          | [`PlatformRef.bootstrapModule`](api/core/PlatformRef#bootstrapModule)                                                                                 | v13                    | With Ivy, there is no need to resolve NgModule factory and NgModule Type can be provided directly.                                                                                                                                                                                                                  |
| [`ModuleWithComponentFactories`](api/core/ModuleWithComponentFactories)                          | none                                                                                 | v13                    | Ivy JIT mode doesn't require accessing this symbol. See [JIT API changes due to ViewEngine deprecation](#jit-api-changes) for additional context.                                                                                                                                                                                                                  |
| [`Compiler`](api/core/Compiler)                          | none                                                                                 | v13                    | Ivy JIT mode doesn't require accessing this symbol. See [JIT API changes due to ViewEngine deprecation](#jit-api-changes) for additional context.                                                                                                                                                                                                                  |
| [`CompilerFactory`](api/core/CompilerFactory)                          | none                                                                                 | v13                    | Ivy JIT mode doesn't require accessing this symbol. See [JIT API changes due to ViewEngine deprecation](#jit-api-changes) for additional context.                                                                                                                                                                                                                  |
| [`NgModuleFactory`](api/core/NgModuleFactory)                          | Use non-factory based framework APIs like [PlatformRef.bootstrapModule](api/core/PlatformRef#bootstrapModule) and [createNgModuleRef](api/core/createNgModuleRef)                                                                                 | v13                    | Ivy JIT mode doesn't require accessing this symbol. See [JIT API changes due to ViewEngine deprecation](#jit-api-changes) for additional context.                                                                                                                                                                                                                 |
| [Factory-based signature of `ViewContainerRef.createComponent`](api/core/ViewContainerRef#createComponent)                                                  | [Type-based signature of `ViewContainerRef.createComponent`](api/core/ViewContainerRef#createComponent)                                    | v13                   | Angular no longer requires component factories to dynamically create components. Use different signature of the `createComponent` method, which allows passing Component class directly. |

{@a testing}

### @angular/core/testing

| API                                           | Replacement                                         | Deprecation announced | Notes                                         |
|:---                                           |:---                                                 |:---                   |:---                                           |
| [`TestBed.get`](api/core/testing/TestBed#get) | [`TestBed.inject`](api/core/testing/TestBed#inject) | v9                    | Same behavior, but type safe.                 |
| [`async`](api/core/testing/async)             | [`waitForAsync`](api/core/testing/waitForAsync)     | v10                   | Same behavior, but rename to avoid confusion. |
| [`aotSummaries` argument in `TestBed.initTestEnvironment`](api/core/testing/TestBed#inittestenvironment)             | No replacement needed     | v13                   | Summary files are unused in Ivy. |
| [`aotSummaries` field of the `TestModuleMetadata` type](api/core/testing/TestModuleMetadata)             | No replacement needed     | v13                   | Summary files are unused in Ivy. |

{@a platform-browser-dynamic}

### @angular/platform-browser-dynamic

| API                                           | Replacement                                         | Deprecation announced | Notes                                         |
|:---                                           |:---                                                 |:---                   |:---                                           |
| [`JitCompilerFactory`](api/platform-browser-dynamic/JitCompilerFactory) | none | v13                    | This symbol is no longer necessary. See [JIT API changes due to ViewEngine deprecation](#jit-api-changes) for additional context. |


{@a platform-server}

### @angular/platform-server

| API                             | Replacement                                     | Deprecation announced | Notes                                          |
|:---                             |:---                                             |:---                   |:---                                            |
| [`renderModuleFactory`](api/platform-server/renderModuleFactory) | [`renderModule`](api/platform-server/renderModule) | v13                    | This symbol is no longer necessary. See [JIT API changes due to ViewEngine deprecation](#jit-api-changes) for additional context. |


{@a forms}

### @angular/forms

| API                                                                         | Replacement                                                                  | Deprecation announced | Notes |
|:---                                                                         |:---                                                                          |:---                   |:---   |
| [`ngModel` with reactive forms](#ngmodel-reactive)                          | [`FormControlDirective`](api/forms/FormControlDirective)                     | v6                    | none  |
| [`FormBuilder.group` legacy options parameter](api/forms/FormBuilder#group) | [`AbstractControlOptions` parameter value](api/forms/AbstractControlOptions) | v11                   | none  |

{@a service-worker}

### @angular/service-worker

| API                                                           | Replacement                                                                            | Deprecation announced    | Notes
|:---                                                           |:---                                                                                    |:---                      |:---
| [`SwUpdate#activated`](api/service-worker/SwUpdate#activated) | [`SwUpdate#activateUpdate()` return value](api/service-worker/SwUpdate#activateUpdate) | v13                      | The return value of `SwUpdate#activateUpdate()` indicates whether an update was successfully activated. |
| [`SwUpdate#available`](api/service-worker/SwUpdate#available) | [`SwUpdate#versionUpdates`](api/service-worker/SwUpdate#versionUpdates)                | v13                      | The behavior of `SwUpdate#available` can be rebuilt by filtering for `VersionReadyEvent` events on [`SwUpdate#versionUpdates`](api/service-worker/SwUpdate#versionUpdates) |

{@a upgrade}

### @angular/upgrade

| API                             | Replacement                                     | Deprecation announced | Notes                                          |
|:---                             |:---                                             |:---                   |:---                                            |
| [All entry points](api/upgrade) | [`@angular/upgrade/static`](api/upgrade/static) | v5                    | See [Upgrading from AngularJS](guide/upgrade). |

{@a upgrade-static}

### @angular/upgrade/static

| API                                                 | Replacement                                                   | Deprecation announced | Notes                                          |
|:---                                                 |:---                                                           |:---                   |:---                                            |
| [`getAngularLib`](api/upgrade/static/getAngularLib) | [`getAngularJSGlobal`](api/upgrade/static/getAngularJSGlobal) | v5                    | See [Upgrading from AngularJS](guide/upgrade). |
| [`setAngularLib`](api/upgrade/static/setAngularLib) | [`setAngularJSGlobal`](api/upgrade/static/setAngularJSGlobal) | v5                    | See [Upgrading from AngularJS](guide/upgrade). |

{@a deprecated-features}

## Deprecated features

This section lists all of the currently-deprecated features, which includes template syntax, configuration options, and any other deprecations not listed in the [Deprecated APIs](#deprecated-apis) section above. It also includes deprecated API usage scenarios or API combinations, to augment the information above.

{@a bazelbuilder}

### Bazel builder and schematics

Bazel builder and schematics were introduced in Angular Labs to let users try out Bazel without having to manage Bazel version and BUILD files.
This feature has been deprecated. For more information, please refer to the [migration doc](https://github.com/angular/angular/blob/master/packages/bazel/docs/BAZEL_SCHEMATICS.md).

{@a wtf}

### Web Tracing Framework integration

Angular previously supported an integration with the [Web Tracing Framework (WTF)](https://google.github.io/tracing-framework) for performance testing of Angular applications. This integration has not been maintained and is now defunct. As a result, the integration was deprecated in Angular version 8, and due to no evidence of any existing usage, removed in version 9.

{@a deep-component-style-selector}

### `/deep/`, `>>>`, and `::ng-deep` component style selectors

The shadow-dom-piercing descendant combinator is deprecated and support is being [removed from major browsers and tools](https://developers.google.com/web/updates/2017/10/remove-shadow-piercing). As such, in v4 we deprecated support in Angular for all three of `/deep/`, `>>>`, and `::ng-deep`. Until removal, `::ng-deep` is preferred for broader compatibility with the tools.

For more information, see [/deep/, >>>, and ::ng-deep](guide/component-styles#deprecated-deep--and-ng-deep "Component Styles guide, Deprecated deep and ngdeep") in the Component Styles guide.

{@a bind-syntax}

### `bind-`, `on-`, `bindon-`, and `ref-` prefixes

The template prefixes `bind-`, `on-`, `bindon-`, and `ref-` have been deprecated in v13. Templates
should use the more widely documented syntaxes for binding and references:

* `[input]="value"` instead of `bind-input="value"`
* `[@trigger]="value"` instead of	`bind-animate-trigger="value"`
* `(click)="onClick()"` instead of `on-click="onClick()"`
* `[(ngModel)]="value"` instead of `bindon-ngModel="value"`
* `#templateRef` instead of `ref-templateRef`

{@a template-tag}

### `<template>` tag

The `<template>` tag was deprecated in v4 to avoid colliding with the DOM's element of the same name (such as when using web components). Use `<ng-template>` instead. For more information, see the [Ahead-of-Time Compilation](guide/aot-compiler) guide.

{@a ngmodel-reactive}

### ngModel with reactive forms

Support for using the `ngModel` input property and `ngModelChange` event with reactive form directives has been deprecated in Angular v6 and will be removed in a future version of Angular.

Now deprecated:

<code-example language="html">

&lt;input [formControl]="control" [(ngModel)]="value"&gt;

</code-example>

<code-example language="typescript">

this.value = 'some value';

</code-example>

This support was deprecated for several reasons. First, developers found this pattern confusing. It seems like the actual `ngModel` directive is being used, but in fact it's an input/output property named `ngModel` on the reactive form directive that approximates some, but not all, of the directive's behavior.
It allows getting and setting a value and intercepting value events, but some of `ngModel`'s other features, such as delaying updates with`ngModelOptions` or exporting the directive, don't work.

In addition, this pattern mixes template-driven and reactive forms strategies, which prevents taking advantage of the full benefits of either strategy.
Setting the value in the template violates the template-agnostic principles behind reactive forms, whereas adding a `FormControl`/`FormGroup` layer in the class removes the convenience of defining forms in the template.

To update your code before support is removed, you'll want to decide whether to stick with reactive form directives (and get/set values using reactive forms patterns) or switch to template-driven directives.

**After** (choice 1 - use reactive forms):

<code-example language="html">

&lt;input [formControl]="control"&gt;

</code-example>

<code-example language="typescript">

this.control.setValue('some value');

</code-example>

**After** (choice 2 - use template-driven forms):

<code-example language="html">

&lt;input [(ngModel)]="value"&gt;

</code-example>

<code-example language="typescript">

this.value = 'some value';

</code-example>

By default, when you use this pattern, you will see a deprecation warning once in dev mode. You can choose to silence this warning by configuring `ReactiveFormsModule` at import time:

<code-example language="typescript">

imports: [
  ReactiveFormsModule.withConfig({warnOnNgModelWithFormControl: 'never'});
]

</code-example>

Alternatively, you can choose to surface a separate warning for each instance of this pattern with a configuration value of `"always"`. This may help to track down where in the code the pattern is being used as the code is being updated.

{@a reflectiveinjector}

### ReflectiveInjector

In v5, Angular replaced the `ReflectiveInjector` with the `StaticInjector`. The injector no longer requires the Reflect polyfill, reducing application size for most developers.

**Before**:

<code-example language="typescript">

ReflectiveInjector.resolveAndCreate(providers);

</code-example>

**After**:

<code-example language="typescript">

Injector.create({providers});

</code-example>

{@a loadChildren}

### loadChildren string syntax

When Angular first introduced lazy routes, there wasn't browser support for dynamically loading additional JavaScript. Angular created our own scheme using the syntax `loadChildren: './lazy/lazy.module#LazyModule'` and built tooling to support it. Now that ECMAScript dynamic import is supported in many browsers, Angular is moving toward this new syntax.

In version 8, the string syntax for the [`loadChildren`](api/router/LoadChildren) route specification was deprecated, in favor of new syntax that uses `import()` syntax.

**Before**:

<code-example language="typescript">

const routes: Routes = [{
  path: 'lazy',
  // The following string syntax for loadChildren is deprecated
  loadChildren: './lazy/lazy.module#LazyModule'
}];

</code-example>

**After**:

<code-example language="typescript">

const routes: Routes = [{
  path: 'lazy',
  // The new import() syntax
  loadChildren: () => import('./lazy/lazy.module').then(m => m.LazyModule)
}];

</code-example>

<div class="alert is-helpful">

**Version 8 update**: When you update to version 8, the [`ng update`](cli/update) command performs the transformation automatically. Prior to version 7, the `import()` syntax only works in JIT mode (with view engine).

</div>

<div class="alert is-helpful">

**Declaration syntax**: It's important to follow the route declaration syntax `loadChildren: () => import('...').then(m => m.ModuleName)` to allow `ngc` to discover the lazy-loaded module and the associated `NgModule`. You can find the complete list of allowed syntax constructs [here](https://github.com/angular/angular-cli/blob/a491b09800b493fe01301387fa9a025f7c7d4808/packages/ngtools/webpack/src/transformers/import_factory.ts#L104-L113). These restrictions will be relaxed with the release of Ivy since it'll no longer use `NgFactories`.

</div>


{@a reflect-metadata}

### Dependency on a reflect-metadata polyfill in JIT mode

Angular applications, and specifically applications that relied on the JIT compiler, used to require a polyfill for the [reflect-metadata](https://github.com/rbuckton/reflect-metadata) APIs.

The need for this polyfill was removed in Angular version 8.0 ([see #14473](https://github.com/angular/angular-cli/pull/14473)), rendering the presence of the poylfill in most Angular applications unnecessary. Because the polyfill can be depended on by 3rd-party libraries, instead of removing it from all Angular projects, we are deprecating the requirement for this polyfill as of version 8.0. This should give library authors and application developers sufficient time to evaluate if they need the polyfill, and perform any refactoring necessary to remove the dependency on it.

In a typical Angular project, the polyfill is not used in production builds, so removing it should not impact production applications. The goal behind this removal is overall simplification of the build setup and decrease in the number of external dependencies.

{@a static-query-resolution}

### `@ViewChild()` / `@ContentChild()` static resolution as the default

See the [dedicated migration guide for static queries](guide/static-query-migration).

{@a contentchild-input-together}

### `@ContentChild()` / `@Input()` used together

The following pattern is deprecated:

<code-example language="typescript">

@Input() @ContentChild(TemplateRef) tpl !: TemplateRef&lt;any&gt;;

</code-example>

Rather than using this pattern, separate the two decorators into their own
properties and add fallback logic as in the following example:

<code-example language="typescript">

@Input() tpl !: TemplateRef&lt;any&gt;;
@ContentChild(TemplateRef) inlineTemplate !: TemplateRef&lt;any&gt;;

</code-example>

{@a cant-assign-template-vars}

### Cannot assign to template variables

In the following example, the two-way binding means that `optionName`
should be written when the `valueChange` event fires.

<code-example language="html">

&lt;option *ngFor="let optionName of options" [(value)]="optionName"&gt;&lt;/option&gt;

</code-example>

However, in practice, Angular ignores two-way bindings to template variables. Starting in version 8, attempting to write to template variables is deprecated. In a future version, we will throw to indicate that the write is not supported.

<code-example language="html">

&lt;option *ngFor="let optionName of options" [value]="optionName"&gt;&lt;/option&gt;

</code-example>

{@a binding-to-innertext}

### Binding to `innerText` in `platform-server`

[Domino](https://github.com/fgnass/domino), which is used in server-side rendering, doesn't support `innerText`, so in platform-server's "domino adapter", there was special code to fall back to `textContent` if you tried to bind to `innerText`.

These two properties have subtle differences, so switching to `textContent` under the hood can be surprising to users. For this reason, we are deprecating this behavior. Going forward, users should explicitly bind to `textContent` when using Domino.

{@a wtf-apis}

### `wtfStartTimeRange` and all `wtf*` APIs

All of the `wtf*` APIs are deprecated and will be removed in a future version.

{@a entryComponents}

### `entryComponents` and `ANALYZE_FOR_ENTRY_COMPONENTS` no longer required

Previously, the `entryComponents` array in the `NgModule` definition was used to tell the compiler which components would be created and inserted dynamically.
With Ivy, this isn't a requirement anymore and the `entryComponents` array can be removed from existing module declarations.
The same applies to the `ANALYZE_FOR_ENTRY_COMPONENTS` injection token.

**NOTE**: You may still need to keep these if building a library that will be consumed by a View Engine application.

{@a moduleWithProviders}

### `ModuleWithProviders` type without a generic

Some Angular libraries, such as `@angular/router` and `@ngrx/store`, implement APIs that return a type called `ModuleWithProviders` (typically using a method named `forRoot()`).
This type represents an `NgModule` along with additional providers.
Angular version 9 deprecates use of `ModuleWithProviders` without an explicitly generic type, where the generic type refers to the type of the `NgModule`.
In a future version of Angular, the generic will no longer be optional.

If you're using the CLI, `ng update` should [migrate your code automatically](guide/migration-module-with-providers).
If you're not using the CLI, you can add any missing generic types to your application manually.
For example:

**Before**

<code-example language="typescript">

@NgModule({...})
export class MyModule {
  static forRoot(config: SomeConfig): ModuleWithProviders {
    return {
      ngModule: SomeModule,
      providers: [
        {provide: SomeConfig, useValue: config}
      ]
    };
  }
}

</code-example>

**After**:

<code-example language="typescript">

@NgModule({...})
export class MyModule {
  static forRoot(config: SomeConfig): ModuleWithProviders<SomeModule> {
    return {
      ngModule: SomeModule,
      providers: [
        {provide: SomeConfig, useValue: config }
      ]
    };
  }
}

</code-example>

<!--
### Internet Explorer 11

Angular support for Microsoft's Internet Explorer 11 (IE11) is deprecated and will be removed in Angular v13.
Ending IE11 support allows Angular to take advantage of web platform APIs present only in evergreen browsers, resulting in better APIs for developers and more capabilities for application users.
An additional motivation behind this removal is the drop in global usage of IE11 to just ~1% (as of March 2021).
For full rationale and discussion behind this deprecation, see [RFC: Internet Explorer 11 support deprecation and removal](https://github.com/angular/angular/issues/41840).

**Note**: IE11 will be supported in Angular v12 LTS releases through November 2022.
-->

{@a input-setter-coercion}
### Input setter coercion

Since the `strictTemplates` flag has been introduced in Angular the compiler has been able to type-check input bindings to the declared input type of the corresponding directive.
When a getter/setter pair is being used for the input it may be desirable to let the setter accept a broader set of types than what is returned by the getter, for example when the setter first converts the input value.
However, until TypeScript 4.3 a getter/setter pair was required to have identical types so this pattern could not be accurately declared.

To mitigate this limitation, it was made possible to declare [input setter coercion fields](guide/template-typecheck#input-setter-coercion) in directives that are used when type-checking input bindings.
However, since [TypeScript 4.3](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-4-3.html#separate-write-types-on-properties) the limitation has been removed; setters can now accept a wider type than what is returned by the getter.
This means that input coercion fields are no longer needed, as their effects can be achieved by widening the type of the setter.

For example, the following directive:

```typescript
@Component({...})
class SubmitButton {
  private _disabled: boolean;

  @Input()
  get disabled(): boolean {
    return this._disabled;
  }

  set disabled(value: boolean) {
    this._disabled = (value === '') || value;
  }

  static ngAcceptInputType_disabled: boolean|'';
}
```

can be refactored as follows:

```typescript
@Component({...})
class SubmitButton {
  private _disabled: boolean;

  @Input()
  get disabled(): boolean {
    return this._disabled;
  }

  set disabled(value: boolean|'') {
    this._disabled = (value === '') || value;
  }
}
```

{@a full-template-type-check}
### `fullTemplateTypeCheck`

When compiling your application using the AOT compiler, your templates are type-checked according to a certain strictness level.
Before Angular 9 there existed only two strictness levels of template type checking as determined by [the `fullTemplateTypeCheck` compiler option](guide/angular-compiler-options).
In version 9 the `strictTemplates` family of compiler options has been introduced as a more fine-grained approach to configuring how strict your templates are being type-checked.

The `fullTemplateTypeCheck` flag is being deprecated in favor of the new `strictTemplates` option and its related compiler options.
Projects that currently have `fullTemplateTypeCheck: true` configured can migrate to the following set of compiler options to achieve the same level of type-checking:

<code-example language="json" header="tsconfig.app.json">

{
  "angularCompilerOptions": {
    ...
    "strictTemplates": true,
    "strictInputTypes": false,
    "strictNullInputTypes": false,
    "strictAttributeTypes": false,
    "strictOutputEventTypes": false,
    "strictDomEventTypes": false,
    "strictDomLocalRefTypes": false,
    "strictSafeNavigationTypes": false,
    "strictContextGenerics": false,
    ...
  }
}

</code-example>

{@a jit-api-changes}

## JIT API changes due to ViewEngine deprecation

In ViewEngine, [JIT compilation](https://angular.io/guide/glossary#jit) required special providers (like `Compiler`, `CompilerFactory`, etc) to be injected in the app and corresponding methods to be invoked. With Ivy, JIT compilation takes place implicitly if the Component, NgModule, etc have not already been [AOT compiled](https://angular.io/guide/glossary#aot). Those special providers were made available in Ivy for backwards-compatibility with ViewEngine to make the transition to Ivy smoother. Since ViewEngine is deprecated and will soon be removed, those symbols are now deprecated as well.

Important note: this deprecation doesn't affect JIT mode in Ivy (JIT remains available with Ivy, however we are exploring a possibility of deprecating it in the future. See [RFC: Exploration of use-cases for Angular JIT compilation mode](https://github.com/angular/angular/issues/43133)).


{@a deprecated-cli-flags}

## Deprecated CLI APIs and Options

This section contains a complete list all of the currently deprecated CLI flags.

### @angular-devkit/build-angular

| API/Option                | May be removed in | Notes                                                                                                          |
| ------------------------- | ----------------- | -------------------------------------------------------------------------------------------------------------- |
| `extractCss`              | <!--v11--> v13    | No longer required to disable CSS extraction during development.                                               |
| `i18nFormat`              | <!--v9--> v12     | Format is now automatically detected.                                                                          |
| `i18nLocale`              | <!--v9--> v12     | New [localization option][AioGuideI18nCommonMergeDefineLocalesInTheBuildConfiguration] in version 9 and later. |
| `hmrWarning`              | <!--v11--> v13    | No longer has an effect.                                                                                       |
| `servePathDefaultWarning` | <!--v11--> v13    | No longer has an effect.                                                                                       |

### @schematics/angular

| API/Option                      | May be removed in | Notes                                                                           |
| ------------------------------- | ----------------- |-------------------------------------------------------------------------------- |
| `lintFix`                       | <!--v11--> v12    | Deprecated as part of TSLint deprecation.                                      |

{@a removed}

## Removed APIs

The following APIs have been removed starting with version 11.0.0*:

| Package          | API            | Replacement | Notes |
| ---------------- | -------------- | ----------- | ----- |
| `@angular/router` | `preserveQueryParams` | [`queryParamsHandling`](api/router/UrlCreationOptions#queryParamsHandling) | |

\* To see APIs removed in version 10, check out this guide on the [version 10 docs site](https://v10.angular.io/guide/deprecations#removed).

{@a esm5-fesm5}

### `esm5` and `fesm5` code formats in @angular/* npm packages

As of Angular v8, the CLI primarily consumes the `fesm2015` variant of the code distributed as part of `@angular/*` npm packages.
This renders the `esm5` and `fesm5` distributions obsolete and unnecessary, adding bloat to the package size and slowing down npm installations.

This removal has no impact on CLI users, unless they modified their build configuration to explicitly consume these code distributions.

Any application still relying on the `esm5` and `fesm5` as the input to its build system will need to ensure that the build pipeline is capable of accepting JavaScript code conforming to ECMAScript 2015 (ES2015) language specification.

Note that this change doesn't make existing libraries distributed in this format incompatible with the Angular CLI.
The CLI will fall back and consume libraries in less desirable formats if others are not available.
However, we do recommend that libraries ship their code in ES2015 format in order to make builds faster and build output smaller.

In practical terms, the `package.json` of all `@angular` packages has changed in the following way:

**Before**:

<code-example language="json" header="package.app.json">

{
  "name": "@angular/core",
  "version": "9.0.0",
  "main": "./bundles/core.umd.js",
  "module": "./fesm5/core.js",
  "es2015": "./fesm2015/core.js",
  "esm5": "./esm5/core.js",
  "esm2015": "./esm2015/core.js",
  "fesm5": "./fesm5/core.js",
  "fesm2015": "./fesm2015/core.js",
  ...
}

</code-example>

**After**:

<code-example language="json" header="package.app.json">

{
  "name": "@angular/core",
  "version": "10.0.0",
  "main": "./bundles/core.umd.js",
  "module": "./fesm2015/core.js",
  "es2015": "./fesm2015/core.js",
  "esm2015": "./esm2015/core.js",
  "fesm2015": "./fesm2015/core.js",
  ...
}

</code-example>

For more information about the npm package format, see the [Angular Package Format spec](https://goo.gl/jB3GVv).

{@a style-sanitization}

### Style Sanitization for `[style]` and `[style.prop]` bindings

Angular used to sanitize `[style]` and `[style.prop]` bindings to prevent malicious code from being inserted through `javascript:` expressions in CSS `url()` entries. However, most modern browsers no longer support the usage of these expressions, so sanitization was only maintained for the sake of IE 6 and 7. Given that Angular does not support either IE 6 or 7 and sanitization has a performance cost, we will no longer sanitize style bindings as of version 10 of Angular.

### `loadChildren` string syntax in `@angular/router`

It is no longer possible to use the `loadChildren` string syntax to configure lazy routes.
The string syntax has been replaced with dynamic import statements.
The `DeprecatedLoadChildren` type was removed from `@angular/router`.
Find more information about the replacement in the [`LoadChildrenCallback` documentation](api/router/LoadChildrenCallback).

The supporting classes `NgModuleFactoryLoader`, `SystemJsNgModuleLoader` and `SystemJsNgModuleLoaderConfig` classes were removed from `@angular/core`, as well as `SpyNgModuleFactoryLoader` from `@angular/router`.

### `WrappedValue`

The purpose of `WrappedValue` was to allow the same object instance to be treated as different for the purposes of change detection.
It was commonly used with the `async` pipe in the case where the `Observable` produces the same instance of the value.

Given that this use case is relatively rare and special handling impacted application performance, the `WrappedValue` API has been removed in Angular 13.

If you rely on the behavior that the same object instance should cause change detection, you have two options:

- Clone the resulting value so that it has a new identity.
- Explicitly call [`ChangeDetectorRef.detectChanges()`](api/core/ChangeDetectorRef#detectchanges) to force the update.

<!-- links -->

[AioGuideI18nCommonMergeDefineLocalesInTheBuildConfiguration]: guide/i18n-common-merge#define-locales-in-the-build-configuration "Define locales in the build configuration - Common Internationalization task #6: Merge translations into the application | Angular"

<!-- end links -->

@reviewed 2021-09-15
