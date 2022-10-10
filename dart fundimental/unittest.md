# Unit Test

## Functions:

### SetUp, SetUpAll, tearDown, tearDownAll

```dart
import 'package:test/test.dart';

void main() {
  setUp(() {
    print('setUp Outer');
  });

  setUpAll(() {
    print('setUpAll Outer');
  });

  tearDown(() {
    print('tearDown Outer');
  });

  tearDownAll(() {
    print('tearDownAll Outer');
  });

  test('test 1', () {
    print('test 1');
  });

  test('test 2', () {
    print('test 2');
  });

  group('group 1', () {
    setUp(() {
      print('setUp Inner');
    });

    setUpAll(() {
      print('setUpAll Inner');
    });

    tearDown(() {
      print('tearDown Inner');
    });

    tearDownAll(() {
      print('tearDownAll Inner');
    });

    test('test 3', () {
      print('test 3');
    });

    test('test 4', () {
      print('test 4');
    });
  });
}

```

Output:

```bash
setUpAll Outer
setUp Outer
test 1
tearDown Outer
✓ test 1
setUp Outer
test 2
tearDown Outer
✓ test 2
setUpAll Inner
setUp Outer
setUp Inner
test 3
tearDown Inner
tearDown Outer
✓ group 1 test 3
setUp Outer
setUp Inner
test 4
tearDown Inner
tearDown Outer
✓ group 1 test 4
tearDownAll Inner
tearDownAll Outer
Exited
```

