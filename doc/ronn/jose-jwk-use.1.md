jose-jwk-use(1) -- Validates a key for the specified use(s)
===========================================================

## SYNOPSIS

`jose jwk use` -i JWK [-a] [-r] -u OP

## OVERVIEW

The `jose jwk use` command validates one or more JWK(Set) inputs for a given
set of usages. This will be validated against the "use" and "key_ops"
properties of each JWK.

By default, if a JWK has no restrictions an operation will be allowed.
However, by specifying the `-r` option you can ensure that a JWK will not
be allowed unless it explicitly permits the option.

In normal operation, `jose jwk use` will fail if any of the JWKs do not
validate. However, if the `-o` option is used `jose jwk use` will instead
write a JWK(Set) containing all of the input keys that validate. If no JWKs
validate, the command will fail.

## OPTIONS

* `-i` _JSON_, `--input`=_JSON_ :
  Parse JWK(Set) from JSON

* `-i` _FILE_, `--input`=_FILE_ :
  Read JWK(Set) from FILE

* `-i` -, `--input`=- :
  Read JWK(Set) standard input

* `-u` sign, `--use`=sign :
  Validate the key for signing

* `-u` verify, `--use`=verify :
  Validate the key for verifying

* `-u` encrypt, `--use`=encrypt :
  Validate the key for encrypting

* `-u` decrypt, `--use`=decrypt :
  Validate the key for decrypting

* `-u` wrapKey, `--use`=wrapKey :
  Validate the key for wrapping

* `-u` unwrapKey, `--use`=unwrapKey :
  Validate the key for unwrapping

* `-u` deriveKey, `--use`=deriveKey :
  Validate the key for deriving keys

* `-u` deriveBits, `--use`=deriveBits :
  Validate the key for deriving bits

* `-a`, `--all` :
  Succeeds only if all operations are allowed

* `-r`, `--required` :
  Operations must be explicitly allowed

* `-o` _FILE_, `--output`=_FILE_ :
  Filter keys to FILE as JWK(Set)

* `-o` -, `--output`=- :
  Filter keys to standard output as JWK(Set)

* `-s`, `--set` :
  Always output a JWKSet

## EXAMPLES

Examples of both success and failure from a private and public key:

    $ jose jwk gen -i '{"alg":"ES256"}' -o prv.jwk
    $ jose jwk pub -i prv.jwk -o pub.jwk
    $ jose jwk use -i prv.jwk -u sign
    $ echo $?
    0
    $ jose jwk use -i pub.jwk -u sign
    $ echo $?
    1

## AUTHOR

Nathaniel McCallum &lt;npmccallum@redhat.com&gt;

## SEE ALSO

`jose-jwk-gen`(1)
