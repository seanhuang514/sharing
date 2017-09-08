# Setter & Method Return
---
# setter
```ruby
class Person
  def initialize(v = nil)
    self.name = v
  end

  def name
    @name
  end

  def name=(v)
    @name = v
  end
end
```
+++
```ruby
class Person
  attr_reader :name
  def initialize(v = nil)
    self.name = v
  end

  def name=(v)
    @name = v
  end
end
```
+++
```ruby
class Person
  attr_accessor :name
  def initialize(v = nil)
    self.name = v
  end
end
```
---
# Method Return
> Every method in Ruby returns a value by default.
This returned value will be the value of the last statement

+++
```ruby
def test
   i = 100
   j = 10
   k = 0
end

p test #=> 0
```
---
# Q1
```ruby
class Person
  attr_reader :name

  def initialize(name = nil)
    self.name = name
  end
  def name=(value)
    @name = value.upcase
  end
end
```
```ruby
boy = Person.new('tom')
p boy.name #=> ??? (lowcase or upcase)
p boy.name = 'john' #=> ??? (lowcase or upcase)
```
+++

```ruby
class Person
  attr_reader :name

  def initialize(name = nil)
    self.name = name
  end
  def name=(value)
    @name = value.upcase
  end
end

boy = Person.new('tom')
p boy.name #=> "TOM"
p boy.name = 'john' #=> "john"
```  
---
Q2
```ruby
class Person
  attr_reader :name

  def initialize(name = nil)
    self.name = name
  end

  def change_name(new_name)
    self.name = new_name
  end

  def name=(value)
    @name = value.upcase
  end
end

boy = Person.new('tom')
new_name_1 = boy.change_name('john')
p new_name_1 #=> ???

new_name_2 = boy.name = 'peter'
p new_name_2 #=> ???
p boy.name #=> ???
```

+++

```ruby
boy = Person.new('tom')
new_name_1 = boy.change_name('john')
p new_name_1 #=> john

new_name_2 = boy.name = 'peter'
p new_name_2 #=> peter
p boy.name #=> PETER
```
---

```ruby
class A
  def initialize(v) end
end

class B
  def initialize() end
end

class C
  attr_reader :aa
  def initialize()
    self.aa = B.new
  end

  def xxx
    self.aa = B.new()
  end

  def aa=(v)
    @aa = A.new(v)
  end
end

p c = C.new() #=> ??? (C class or B Class)
p c.aa = B.new #=> ??? (what class will return?)
p c.xxx #=> ??? (what class will return?)
```
+++
```ruby
p c = C.new() #= C
p c.aa = B.new #=> B
p c.xxx #=> B
```

---
# conclusion

> Setters always return the value they were originally assigned It's a design choice. We defined the value of the assignment as the value of the right hand expression, not the return value from the assigning method.

---

>If you define an « assignment-like » method (with an equal sign at the end), Ruby will execute the method when you call it, but will always return the supplied parameter and never the result of the method.

---
```ruby
class Person
  attr_reader :name

  def initialize(name = nil)
    self.name = name
  end
  def name=(value)
    @name = value.upcase
  end
end
new_name_1 = boy.name = 'john'
boy.name #=> JOHN
new_name_1 #=> john
```
>You can’t chain assignent-like methods, so if you need such a thing, do it differently
