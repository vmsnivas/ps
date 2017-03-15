# PERL Variables

- There are 3 types of variables in PERL
	- Scalars
	- Arrays
	- Hashes

- Scalar variables stores a single value like name or word etc.
- Arrays are list of values
- Hashes are Key, Value pairs like dictionaries in Python

- ***Scalar Variables***
	- We should use the variable names in perl like dollor symbol followed by a name while assigning the variable as well.
	
	```
	$NAME = "Arjun"
	```

	- `strict`
		- The `strict` pragma disables certain Perl expressions that could behave unexpectedly or are difficult to debug, turning them into errors. The effect of this pragma is limited to the current file or scope block. If no import list is supplied, all possible restrictions are assumed. (This is the safest mode to operate in, but is sometimes too strict for casual programming.) Currently, there are three possible things to be strict about: "subs", "vars", and "refs".
		- `strict refs`
			- This generates a runtime error if you use symbolic references

			```
		    	use strict 'refs';
			$ref = \$foo;
			print $$ref;	# ok
			$ref = "foo";
			print $$ref;	# runtime error; normally ok
			$file = "STDOUT";
			print $file "Hi!";	# error; note: no comma after $file
			```

		- `strict vars`
			- This generates a compile-time error if you access a variable that was neither explicitly declared (using any of my, our, state, or use vars ) nor fully qualified. (Because this is to avoid variable suicide problems and subtle dynamic scoping issues, a merely local variable isn't good enough.)

			```
			use strict 'vars';
			$X::foo = 1;	 # ok, fully qualified
			my $foo = 10;	 # ok, my() var
			local $baz = 9;	 # blows up, $baz not declared before
			package Cinna;
			our $bar;			# Declares $bar in current package
			$bar = 'HgS';		# ok, global declared via pragma
			```

			- `my`
			A my declares the listed variables to be local (lexically) to the enclosing block, file, or eval. If more than one variable is listed, the list must be placed in parentheses.

			```
			my ( undef, $min, $hour ) = localtime;
			```

			- `our`
			our makes a lexical alias to a package (i.e. global) variable of the same name in the current package for use within the current lexical scope.

			```
			package Foo;
			use strict;
			$Foo::foo = 23;
			{
				our $foo;   # alias to $Foo::foo
				print $foo; # prints 23
			}
			print $Foo::foo; # prints 23
			print $foo; # ERROR: requires explicit package name
			```

			```
			package Foo;
			use strict;
			our $foo = 23;   # just like $Foo::foo = 23
			print $Foo::foo; # prints 23
			```

			```
			package Foo;
			use strict;
			my  $foo = $foo; # error, undeclared $foo on right-hand side
			our $foo = $foo; # no errors
			```

			- `state`
			state declares a lexically scoped variable, just like my. However, those variables will never be reinitialized, contrary to lexical variables that are reinitialized each time their enclosing block is entered. If more than one variable is listed, the list must be placed in parentheses. With a parenthesised list, undef can be used as a dummy placeholder. However, since initialization of state variables in list context is currently not possible this would serve no purpose.