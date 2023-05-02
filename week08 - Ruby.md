# Ruby

Check your version:
`ruby -v`

Run on CLI: `irb` (Interactive Ruby Shell)

Syntax primer:\
https://learnxinyminutes.com/docs/ruby/

Notes:

- Use double quotes if you want to use string literals.
- Ruby is strictly sync.
- retrieve data off the CLI using gets:

```ruby
print "How old are you? "
age = gets.chomp`
```

- `ARGV` for command line arguments
- Functions take the form of:

```ruby
def sum(arg1, arg2)
  # arbitrary code...
  arg1 + arg2
end
# returns whatever is on the last line unless otherwise specified.
```

- Loops:
  A few ways to write them, but this is most common:

```ruby
fruits = ['apples', 'oranges', 'pears', 'apricots']

fruits.each do |fruit|
  puts "A fruit of type: #{fruit}"
end

# Or...
# Closer to the C style loop.
(0..5).each do |i|
  puts "adding #{i} to the list."
  elements.push(i)
end

# also while loops:
i = 0
while i < 6
# Code...
  i += 1
end
```


Load a file into irb and effectively extend it:
`irb -r './<filename>.rb`

## Instance vs Local variables:
Instance variables are accessible all through the instance and are marked with @. eg `@subtotal`\
Local variables are only accessible within their code blocks. eg. `tax amount`.

```ruby
class Invoice

  def initialize(subtotal)
    @subtotal = subtotal
    @items    = []
  end

  def with_tax
    tax_amount = @subtotal * 0.20
    @subtotal + tax_amount
  end

  def add_item(item)
    # The << method is often used to add an item to the end of an array
    @items << item
    @subtotal += item.price
  end

end
```