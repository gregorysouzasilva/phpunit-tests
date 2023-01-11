# phpunit-tests
Github hook pre-commit that show progress.

## .git/hooks/pre-commit
```
#!/bin/bash

exec < /dev/tty
vendor/bin/phpunit --colors -c $(echo $PWD)/phpunit.xml --stop-on-failure

#Get the last processes exit code
rc=$?
if [[ $rc != 0 ]] ; then
    echo -n "It looks like some of your tests failed. Would you like to see a more detailed test output? (y/n) "
    read YN
    if [ -z "$YN" ]; then
        exit $rc;
    elif [ "$YN" != "y" ]; then
        exit $rc;
    fi
    vendor/bin/phpunit/phpunit --colors -c $(echo $PWD)/phpunit.xml --verbose --stop-on-failure
fi

exit $rc;
```
