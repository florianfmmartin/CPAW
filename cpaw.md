# CPAW implementation

## Value

The values in a packge can either be a keyword, an integer or a nil.

```janet
(defn cpaw-value? [value]
  (or (keyword? value) (int? value) (nil? value)))
```

## Resource creation

Here, we'll define how to create the resources.

```janet
(defn pkg [name &opt obj rel sub]
  (assert
    (and (keyword? name)
         (cpaw-value? obj)
         (cpaw-value? rel)
         (cpaw-value? sub)))
  [:pkg name obj rel sub])

(defn container [name]
  (assert (keyword? name))
  @{:internal @[]
    :push (fn [self v] (array/push (self :internal) v))})
```

## Core

```core
#!/bin/sh
janet {{NOTEBOOK}}
```

