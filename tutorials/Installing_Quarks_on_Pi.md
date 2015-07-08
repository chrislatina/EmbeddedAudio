# Installing Quarks on Pi

** This tutorial is still in progress **

Create a script in SuperCollider called installQuarks.sc

```
~newQuarksSourceForge = Quarks.new( "https://svn.code.sf.net/p/quarks/code/", Platform.userAppSupportDir +/+ "quarks" );
~newQuarksSourceForge.updateDirectory;
```

scp this script to your synthdefs folder on the pi and run

```sh
sclang installQuarks.sc
```

## References

[http://supercollider.github.io/development/quarks-repository-moved.html]( http://supercollider.github.io/development/quarks-repository-moved.html)
