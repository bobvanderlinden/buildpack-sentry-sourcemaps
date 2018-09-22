# buildpack-sentry-sourcemaps

This is a simple [Heroku buildpack][] used to uploads JavaScript sourcemaps
to [Sentry][], as described in [the Sentry docs][docs].

## Usage

Several environment variables are needed:

- `SOURCEMAP_DIR` (optional): the folder (relative to the app root) where the sourcemaps can be found
- `SOURCEMAP_SENTRY_TOKEN`: an authentication token for the Sentry API. You can
  get it on the [API page][]. The token needs the `project:write` scope.
- `SOURCEMAP_SENTRY_PROJECT`: the project slug of your Sentry project. (`myproject` in case of `https://sentry.io/myorg/myproject`)
- `SOURCEMAP_SENTRY_ORG`: the organisation slug of your Sentry project. (`myorg` in case of `https://sentry.io/myorg/myproject`)
- `SOURCEMAP_REPO` (optional): the source code repository where the source files are located. For instance `https://github.com/myorg/myproject`.
- `SOURCEMAP_URL_PREFIX`: the prefix to prepend to each sourcemap.
For browser-based applications this can be a full URL (`https://example.com/dist/js/`) or a tilde-based prefix (`~/dist/js/`.
For server-side applications this can be `/app/`, as that is where Heroku places the server files.
**Note** Always make sure this value ends with `/`.
See the [documentation][docs] for details.

Then add this buildpack to your app:

    heroku buildpacks:add https://github.com/Schnouki/buildpack-sentry-sourcemaps

And push a new relase.

The buildpack will use the current git commit number (environment variable
`$SOURCE_VERSION`) as the Sentry release. Make sure to add that in your app as
well!

## License

MIT.


[Heroku buildpack]: https://devcenter.heroku.com/articles/buildpacks
[Sentry]: https://sentry.io/
[docs]: https://docs.sentry.io/clients/javascript/sourcemaps/
[API page]: https://sentry.io/api/
