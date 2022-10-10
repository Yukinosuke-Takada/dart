# Class Singleton

## Basic

Singleton class has same instance over every creation.

```dart
class Account {
  static final Account _shared = Account._sharedInstance();
  Account._sharedInstance();
  factory Account() => _shared;
  
  final int t = 100;
}

class Person {
  final int t = 10;
}

void main() {
  final a = Person();
  final b = Person();
  
  print(a.hashCode);
  print(b.hashCode);
  
  final t = Account();
  final s = Account();
  
  print(t.hashCode);
  print(s.hashCode);
}

```

Output:

```bash
258290586
559245668
809817532
809817532
```

### Usecase

field value etc are same across all.

```dart
class Account {
  static final Account _shared = Account._sharedInstance();
  Account._sharedInstance();
  factory Account() => _shared;
  
  int value = 100;
}

void main() {
  final t = Account();
  final s = Account();
  
  print(t == s);
  
  t.value = 200;
  print(s.value);
}
```

Output:

```bash
true
200
```

## Advanced

### Parameters

final field value can be overriden with keeping the same instance. Useful for unit testing.

```dart
class Account {
  late int value;

  static final Account _shared = Account._sharedInstance();
  Account._sharedInstance();
  factory Account({int value = 100}) {
    _shared.value = value;
    return _shared;
  }
}

void main() {
  final t = Account(value: 500);
  
  print("value: ${t.value}, hashCode: ${t.hashCode}");
  
  final s = Account(value: 400);
  
  print("value: ${t.value}, hashCode: ${t.hashCode}");
  print("value: ${s.value}, hashCode: ${s.hashCode}");
  
  final u = Account();
  
  print("value: ${t.value}, hashCode: ${t.hashCode}");
  print("value: ${s.value}, hashCode: ${s.hashCode}");
  print("value: ${u.value}, hashCode: ${u.hashCode}");
}

```

Output: 

```bash
value: 500, hashCode: 502709583
value: 400, hashCode: 502709583
value: 400, hashCode: 502709583
value: 100, hashCode: 502709583
value: 100, hashCode: 502709583
value: 100, hashCode: 502709583
```

