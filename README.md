# Purescript React Testing Library

PureScript wrappers for [react-testing-library](https://github.com/testing-library/react-testing-library).

# Changelog

## `4.0.0`

Switched from `jsdom-global` to `global-jsdom`

## First install the node packages

```
npm install --save-dev @testing-library/react @testing-library/user-event jsdom global-jsdom
```

## Example

```purescript
module Test.Component.CounterSpec where

import Prelude
import Effect.Aff (Aff)
import Effect.Class (liftEffect)
import React.Basic (ReactComponent)
import React.TestingLibrary (cleanup, fireEventClick, renderComponent)
import Test.Component.Counter (mkCounter)
import Test.Spec (Spec, after_, before, describe, it)
import Test.Spec.Assertions.DOM (textContentShouldEqual)

spec ∷ Spec Unit
spec =
  after_ cleanup
    $ before setup
    $ describe
        "A simple counter" do
        it
          "renders without errors" \counter -> do
          { findByLabelText } <- renderComponent counter {}
          elem <- findByLabelText "A simple counter"
          elem `textContentShouldEqual` "Increment: 0"
        it
          "increments when clicked" \counter -> do
          { findByLabelText } <- renderComponent counter {}
          elem <- findByLabelText "A simple counter"
          elem `textContentShouldEqual` "Increment: 0"
          fireEventClick elem
          elem `textContentShouldEqual` "Increment: 1"

setup ∷ Aff (ReactComponent {})
setup = mkCounter # liftEffect
```

## More examples

Check out the examples in the `test` folder.
