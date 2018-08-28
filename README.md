# CanonicalAngularcliApp

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 6.1.0-rc.0.

and then modified by hand to run under Bazel.

Recommended to create the `dist` folder with `ln -s $(bazel info bazel-bin) dist`

## Development server

Instead of `ng serve`, run `ibazel run src:devserver`

Navigate to `http://localhost:4200/`. The app will automatically reload if you change any of the source files.

## Code scaffolding

Run `ng generate component component-name` to generate a new component. You can also use `ng generate directive|pipe|service|class|guard|interface|enum|module`.

## Build

Run `bazel build src:bundle` to build the project. The build artifacts will be stored in the `dist/` directory. All builds are production builds.

## Running unit tests

Run `bazel test src/...` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Running end-to-end tests

Run `bazel test e2e` to execute the end-to-end tests via [Protractor](http://www.protractortest.org/).

## Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI README](https://github.com/angular/angular-cli/blob/master/README.md).
