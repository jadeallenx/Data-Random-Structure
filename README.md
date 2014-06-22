# NAME

Data::Random::Structure - Generate random data structures

# VERSION

version 0.01

# SYNOPSIS

    use Test::More;
    use Data::Random::Structure;
    use JSON::PP;

    my $g = Data::Random::Structure->new(
          max_depth => 2,
          max_elements => 5,
    );

    my $ref = $g->generate();

    diag explain $ref; 

    my $json = JSON::PP->new;

    print $json->pretty->encode($ref);

    ok(1);

    done_testing();

# OVERVIEW

This is a library to create random Perl data structures, mostly as a means to
create input for benchmarking and testing various serialization libraries.

It uses grotty 'classic' Perl 5 OO mostly because I think having Moo as a
dependency for a testing module is pretty gross.  On the other hand, original
flavor Perl OO is pretty gross.

# ATTRIBUTES

## max\_depth

The maximum depth to embed data structures

## max\_elements

The maximum number of elements (array items or hash key/value pairs) per data structure.

# METHODS

## new

Constructor. May optionally pass:

- max\_depth
- max\_elements

If not set, these default to 3 and 6 respectively. Throws an exception if the argument
list is not a multiple of 2.

## generate

Recursively generate a data structure using hashes and arrays. The data structure
will not contain more than `max_depth` nested data structures.

## generate\_scalar

Randomly generates one of the following scalar values:

- float
- integer (between 0 and 999\_999)
- string (see [Data::Random](http://search.cpan.org/perldoc?Data::Random) `rand_chars`)
- bool (value based 50/50 coin toss)

## generate\_array

Generate an arrayref and populate it with no more than `max_element` items. May be
empty.

## generate\_hash

Generate a hashref and populate it with no more than `max_element` key/value pairs.
May be empty.

# AUTHOR

Mark Allen <mrallen1@yahoo.com>

# COPYRIGHT AND LICENSE

This software is copyright (c) 2014 by Mark Allen.

This is free software; you can redistribute it and/or modify it under
the same terms as the Perl 5 programming language system itself.
