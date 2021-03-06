# chai-lodash

Fuzzy matchers for chai based on lodash and inspired by chai-fuzzy.

Make assertions that values have all the same attributes and values without asserting strict object equality.

[![Build Status](https://travis-ci.org/morrissinger/chai-lodash.png)](https://travis-ci.org/morrissinger/chai-lodash)

## Using

Also see the [tests](https://github.com/morrissinger/chai-lodash/tree/master/test/) and [examples](https://github.com/morrissinger/chai-lodash/tree/master/examples/).

### browser-side

include chai lodash after chai and lodash:

```html
    <script src="lodash.js"></script>
    <script src="chai.js"></script>
    <script src="chai-lodash.js"></script>
```

### server-side

have chai use chai-lodash:

```javascript
    var chai = require('chai');
    chai.use(require('chai-lodash'));
```

## Assertions


### like(value)

compare object attributes and values rather than checking to see if they're the same reference

```javascript
    var subject = {a: 'a'};
    subject.should.be.like({a: 'a'});
    subject.should.not.be.like({x: 'x'});
    subject.should.not.be.like({a: 'a', b: 'b'});

    expect(subject).to.be.like({a: 'a'});
    expect(subject).not.to.be.like({x: 'x'});
    expect(subject).not.to.be.like({a: 'a', b: 'b'});

    assert.like(subject, {a: 'a'});
    assert.notLike(subject, {x: 'x'});
    assert.notLike(subject, {a: 'a', b: 'b'});

    var subject = ['a'];
    subject.should.be.like(['a']);
    subject.should.not.be.like(['x']);
    subject.should.not.be.like(['a', 'b']);

    expect(subject).to.be.like(['a']);
    expect(subject).not.to.be.like(['x']);
    expect(subject).not.to.be.like(['a', 'b']);

    assert.like(subject, ['a']);
    assert.notLike(subject, ['x']);
    assert.notLike(subject, ['a', 'b']);
```

## containOneLike(value)

check the first level of the container for a value like the one provided

```javascript
    var subject = {
      a:   'alphabet',
      b: 'butternut',
      c: {
        name: 'chowder',
        attributes: [
          'scales',
          'fins'
        ]
      },
      x: 'xylophone',
      z: 'xylophone'
    };

    subject.should.containOneLike({
      name: 'chowder',
      attributes: [
        'scales', 'fins'
      ]
    });

    subject.should.not.containOneLike({
      name: 'chowder',
      attributes: [
        'scales',
        'fins',
        'cream'
      ]
    });

    subject.should.containOneLike('xylophone');
    subject.should.not.containOneLike('cow patties');

    expect(subject).to.containOneLike('xylophone');
    expect(subject).to.not.containOneLike('cow patties');

    assert.containOneLike(subject, 'xylophone');
    assert.notContainOneLike(subject, 'cow patties');

    // same for arrays
```

# jsonOf(value)

check that the given javascript object is like the JSON-ified expected value.  Useful for checking stringification and parsing of an object.

```javascript
    var apple = {
      skin: 'thin', colors: ['red', 'green', 'yellow'], isFruit: true, picked: new Date()
    };

    var orange = {
      skin: 'thin',
      colors: [
      	'red',
      	'green',
      	'yellow'
      ],
      isFruit: true,
      picked: new Date()
    };

    // here appleJSON would be the json result of some process like a JSON api
    var appleJSON  = JSON.parse(JSON.stringify(apple));

    appleJSON.should.be.jsonOf(apple);
    appleJSON.should.not.be.jsonOf(orange);

    expect(appleJSON).to.be.jsonOf(apple);
    expect(appleJSON).to.not.be.jsonOf(orange);

    assert.jsonOf(appleJSON, apple);
    assert.notJsonOf(appleJSON, orange);
```

# Thanks

Thanks to [Elliotf](http://github.com/elliotf/ "Elliotf") for contributing the very excellent [Chai-Fuzzy](http://github.com/elliotf/chai-fuzzy), on which this is based.
