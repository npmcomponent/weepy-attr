*This repository is a mirror of the [component](http://component.io) module [weepy/attr](http://github.com/weepy/attr). It has been modified to work with NPM+Browserify. You can install it using the command `npm install npmcomponent/weepy-attr`. Please do not open issues or send pull requests against this repo. If you have issues with this repo, report it to [npmcomponent](https://github.com/airportyh/npmcomponent).*
# component-attr

evented attributes with automatic dependencies

## API

### attr(val)

  Create a new attr with value set to val

```javascript
attr = require('attr')

name = attr('Homer Simpson')
```

### xxx()
  
  Read a value

```javascript
name() // => 'Homer Simpson'
```

### xxx(val)

   Write a value

```javascript
name('Bart Simpson')

name() // => 'Bart Simpson'
```

  - Emits "change" event with `(value, previousValue)`.

```javascript
name.on('change', function(new_name, old_name) {
  console.log('my name changed from', old_name, 'to', new_name)
})
```

## Computed attr

  Has the same API, except function is passed in and is run to determine the initial value. (has no setter)

```javascript
fullName = attr(function() {
  return firstName() + ' ' + surName()
})

fullName() // => 'Homer Simpson'

fullName.dependencies // => [ firstName, surName ]
```

Dependencies on other simple (non-computed) are automatically calculated unless set explicitly via a second argument as in:

```
fullName = attr(function() {
  return firstName() + ' ' + surName()
}, [firstName])

fullName.dependencies // => [ firstName ]
```

## attr methods

### .toggle()

  Flips truthy to false and falsey to true

### .incr(val) 
  
  Increments value by 1 or val

### .change(fn)

  Binds fn to the `change` event

### .change()

 force a change event

### .value
  
  contains the current value. Use to get value without running the getter (most useful for computed attr)

### .old
  
  contains the last value 

### .dependencies

  Contains a list of dependencies (this will be null for simple attr)

## additional

### attr.autocompute

  By default function values are assumed to be computed. This behaviour can be turned off by setting autocompute. 

### attr.computed(fn, dependencies)
  
  Explicitly creates a computed attr - this is only useful if autocompute is turned off

### attr.dependencies(fn)

  Calculates a list of the simple (non-computed) attributes called by running this function

# Testing

  make && open test/index.html 

# License

  MIT