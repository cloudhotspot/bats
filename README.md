# Alpine Docker Image for BATS

This image provides a minimal image for running the [Bash Automated Testing System (BATS)](https://github.com/sstephenson/bats).

The default entrypoint for this image runs `bats` and the default command argument specifies the folder `/tests`.  This will run any Bats tests located in this folder.  

## Writing Tests

See the BATS Github README for details on writing tests.

A [sample test script](./tests/sample.bats) is included in this repository and the `cloudhotspot/bats` image:

```
#!/usr/bin/env bats

@test "addition using bc" {
  result="$(echo 2+2 | bc)"
  [ "$result" -eq 4 ]
}

@test "addition using dc" {
  result="$(echo 2 2+p | dc)"
  [ "$result" -eq 4 ]
}
```

## Running Tests

To run the sample tests:

```
$ docker run -it --rm cloudhotspot/bats
1..2
ok 1 addition using bc
ok 2 addition using dc
```

To run your own tests it is recommended to create a new child image based from this image and copy your tests to the /tests folder:

```
# Example child image
FROM cloudhotspot/bats
COPY my-tests /tests
```