# Test2::Tools::JSON::Pointer [![Build Status](https://secure.travis-ci.org/plicease/Test2-Tools-JSON-Pointer.png)](http://travis-ci.org/plicease/Test2-Tools-JSON-Pointer)

Compare parts of JSON string to data structure using JSON pointers VERSION

# SYNOPSIS

    use utf8;
    use Test2::V0;
    use Test2::Tools::JSON::Pointer;
    
    is(
      '{"a":"龍"}',
      json '/a' => "龍",
    );
    
    is(
      '{"a":[1,2,3],"b":{"x":"y"}',
      json '/a' => [1,2,3],
    );
    
    is(
      '{"a":[1,2,3],"b":{"x":"y"}',
      json '/b' => hash {
        field 'x' => 'y';
      },
    );
    
    done_testing;

# DESCRIPTION

This module provides a comparison for a JSON string with a JSON pointer.  This
module was inspired by [Test::Mojo](https://metacpan.org/pod/Test::Mojo), which provides a mechanism for checking
the JSON response from a HTTP body.  This module provides a generic way to
write tests for JSON using a JSON pointer with or without the context of 
[Mojolicious](https://metacpan.org/pod/Mojolicious) or [HTTP](https://metacpan.org/pod/HTTP).  It also has a [Test2::Suite](https://metacpan.org/pod/Test2::Suite) style interface.

This module expects a Perl string in Perl's internal representation (utf-8),
NOT raw encoded bytes.  Thus if you are reading files they need to be read
in with the appropriate encoding.  If you are testing against the content
of a [HTTP::Response](https://metacpan.org/pod/HTTP::Response) object you want to use `decoded_content`.

# FUNCTIONS

## json

    is(
      $json_string,
      json($pointer, $check)
    );
    is(
      $json_string,
      json($check),
    );

Compare the `$json_string` to the given [Test2::Suite](https://metacpan.org/pod/Test2::Suite) `$check` after
decoding the string into a deep reference (array or hash) and starting
at the position of the given `$pointer`.

# SEE ALSO

- [Test2::Tools::JSON](https://metacpan.org/pod/Test2::Tools::JSON)

    Provides a similar check without JSON pointers.

- [Test::Deep::JSON](https://metacpan.org/pod/Test::Deep::JSON)

    Provides a similar check in a [Test::Deep](https://metacpan.org/pod/Test::Deep) context.

- [Test::Mojo](https://metacpan.org/pod/Test::Mojo)

    Among many other capabilities, this great testing library allows you to make checks against JSON on
    an HTTP response object with JSON pointers.

# AUTHOR

Graham Ollis <plicease@cpan.org>

# COPYRIGHT AND LICENSE

This software is copyright (c) 2018 by Graham Ollis.

This is free software; you can redistribute it and/or modify it under
the same terms as the Perl 5 programming language system itself.
