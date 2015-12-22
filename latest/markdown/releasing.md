Release engineering for uw-frame is pretty automated. We actually only have to do a few things.

### Select a version

Look at the [closed pull requests](https://github.com/UW-Madison-DoIT/uw-frame/pulls?q=is%3Apr+is%3Aclosed) that were done since the last release. There should be tags on pull requests that deem a release: major, minor, or patch (x.y.z respectively).

Now that you have a version you need to update that in a few places.

### Release steps

+ Update the version in `package.json` that is in the root directory. Commit that.
+ Make tag for bower: `git tag <version>; git push <version>`
+ Now do release for Java.

`cd uw-frame-java`
`mvn release:prepare`
`mvn release:perform`
_Iff it went well_
`git push master`
`git push uw-frame-maven-<version>`

+ Release maven artifacts from central staging repository
+ Create release docs on gh-pages (Jenkins job) using the tag created for bower.

### Documentation branching

+ Update version.md to have the latest tag as a folder
+ Run jenkins job to release a new version of the documentation
+ Verify you can get to that version of the documentation on gh-pages