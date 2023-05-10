# heroku-buildpack-magnus

Compile [magnus](https://github.com/matsadler/magnus) powered Ruby native extensions on Heroku.

## Dependencies

This buildpack assumes that [heroku-buildpack-apt](https://github.com/heroku/heroku-buildpack-apt) runs before this buildpack
and that the `Aptfile` that configures it specifies `clang` (a dependency of magnus).

This buildpack also assumes that `MAGNUS_RAKE_BUILD_TASK` is set on the Heroku environment and available at build time.

## Notes

* The dependency on heroku-buildpack-apt is required since only Heroku's privileged buildpacks are allowed to do `apt-get install`
* This package is very aggressive about cleanup from the `apt-install` artifacts as well as the target outputs from `cargo build`.
  This is in order to reduce slug size.

## References

* Heavily inspired by [emk/heroku-buildpack-rust](https://github.com/emk/heroku-buildpack-rust). Use that if you can. This buildpack
  was made for a very specific task that the generic Rust buildpack doesn't seem to support.
