ruby-benchmarks
===============

Some Ruby benchmarks in my system

## System information
```sh
$ ruby -v
ruby 1.9.3p327 (2012-11-10 revision 37606) [x86_64-darwin12.2.0]
```


## Range#includes? (n..m) | number >= n and <= m

```ruby
require 'benchmark'

range = (0.1..0.9)

Benchmark.bm(7) do |x|
  x.report("includes?:\t")   { 10000.times { range.include? 0.9 } }
  x.report("< && >:\t\t") { 10000.times { 0.9 >= 0.1 && 0.9 <= 0.9 } }
end
```

Result:
```ruby

                    user     system      total        real
includes?:      0.010000   0.000000   0.010000 (  0.005760)
< && >:    	    0.000000   0.000000   0.000000 (  0.002913)
```

## String interpolation ("#{x}") | "%s" % x | "" + x
```ruby
require 'benchmark'

a = "hola"

Benchmark.bm(7) do |x|
  x.report("\#{} :")   { 10000.times { "\t#{a}" } }
  x.report("%s % :") { 10000.times { "\t%s" % a } }
  x.report(" + :") { 10000.times { "\t" + a } }
end
```

Result:
```sh
              user     system      total        real
#{} :     0.010000   0.000000   0.010000 (  0.003372)
%s % :    0.050000   0.000000   0.050000 (  0.057712)
 + :      0.010000   0.000000   0.010000 (  0.002924)
```


## Array.each | for in
```ruby
require 'benchmark'

array = (0..100).to_a

Benchmark.bm(7) do |x|
  x.report("each")   { 10000.times { array.each { |element| element  } } }
  x.report("for in") {
    10000.times {
      for element in array
        element
      end
    }
  }
end
```

Results:
```sh
              user     system      total        real
each      0.110000   0.000000   0.110000 (  0.116206)
for in    0.130000   0.000000   0.130000 (  0.142046)
```
