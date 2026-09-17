# Weekly Report 02

## Glauriel

---

## Tien

### 1. Template Method Pattern (Hook & Template)

- **Template method:** Defined in the superclass to set the workflow order and invoke hook(s).
* **Hook method:** Using self and let subclass define it.

---

### 2. `printOn:` vs `printString`

- **Implement `printOn: aStream`:** This is where you describe how your object looks. Use streams to avoid creating throwaway strings.
- **Call `printString`:** Use this when you actually need a `String` (like printing it with `Ctrl + P`). It will call `printOn:` behind the scenes.

```
Person >> printOn: aStream
    super printOn: aStream.
    aStream 
        nextPut: $(;
        nextPutAll: firstName;
        space;
        nextPutAll: lastName;
        nextPut: $)

```
- In addition, `Transcript show: ...; cr` for console/ log streaming. `cr` inserts a line break.

---

### 3. Initialization

Always call `super initialize` first when setting up your object's default state to avoid a warning:

```
MyClass >> initialize
    super initialize.
    items := OrderedCollection new.

```

---

### 4. `yourself` vs `self`

- `self` is the object itself inside a method.
- `yourself` is a helper message (`^ self`) used at the end of a cascade (`;`). It makes sure the entire expression returns the original object, not whatever the last message returned.

```
"Without yourself, you would get the number 2 instead of the collection"
numbers := OrderedCollection new
    add: 1;
    add: 2;
    yourself.

```

---

### 5. Extending Existing Classes (like `Integer`)

In Pharo, you don't need to subclass to add a method to built-in classes:

1. Select `Integer` in the browser.
2. Add new methods to `Integer`
3. Add new protocol by clicking `Extension` at the bottom right of console and typing name of package
