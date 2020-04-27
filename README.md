# Incremental compilation bug

https://youtrack.jetbrains.com/issue/KT-38570

## Steps

* Run `./gradlew assemble`.
  * In `integration-test/build/sample-dir` you'll find the generated code.
* Change line 71 in `SquareComponentRegistrar` from `val hello${counter++} = "world"` to `val hello${counter++} = "something else"`.
* Run `./gradlew assemble` again.
  * Look at the generated source. Nothing has changed.

Repeat the steps, but put `kotlin.incremental=false` into your `gradle.properties`. You'll see that the generated code will change.