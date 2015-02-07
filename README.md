# Yii2-Ant
A set of targets for running Yii using Ant. To be used mostly with CI systems.

# How to use it
This Yii Ant project has been created specifically for Yii version 2.

It comes with a pre-defined target and a MarcoDef if you want to extend it.

The simplest use you can make of it is by including it and then invoking it in your project as follows:

```xml
    <!-- include the codeception ant project file -->
    <include file="${basedir}/build/yii.xml" as="yii"/>

    <!-- invoke it by creating a dependency on any of your targets -->
    <target name="prepare"
            unless="prepare.done"
            depends="clean, yii.migrate-all"
            description="Prepare for build">
        <!-- ... -->
    </target>
```

`yii.migrate-all` will invoke the basic `yii` executable to re-run all the migrations by doing a `migrate/redo` followed by a `migrate/up` to run any new migration. It will also run the same sequence of calls with the `yii` executable on the test folder.

You can also use the MarcoDef to build the sequence of call you want, e.g.:

```xml
    <migrate exec="${yii.script}" action="down"/>
    <migrate exec="${yii.script}" action="up"/>
    <migrate exec="${yii.tests.script}" action="down"/>
    <migrate exec="${yii.tests.script}" action="up"/>
```

## Parameters

There are no parameters that can be passed to the script.

The only two properties used internally are where the basic and test `yii` scripts are found:

```xml
    <property name="yii.script" value="${basedir}/yii"/>
    <property name="yii.tests.script" value="${basedir}/tests/codeception/bin/yii"/>
```

You won't normally need to update these.

# Contributions are welcome

Please contribute by opening an issue or by forking and issuing a Pull Request.

If you want to do a Pull request, please be sure to read the following article first:
[How to write the perfect pull request](https://github.com/blog/1943-how-to-write-the-perfect-pull-request).
