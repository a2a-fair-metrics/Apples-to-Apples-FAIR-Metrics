# Benchmarks for Apples-to-Apples FAIR Signposting


These are the [Apples-to-Apples FAIR Signposting](https://signposting.org/FAIR/apples-hackathon/)
benchmark tests for tools to verify parsing and compliance with the
[FAIR Signposting](https://signposting.org/FAIR/) profile of 
[RFC8288](https://tools.ietf.org/html/rfc8288#section-2)
and the [Linkset media types](https://datatracker.ietf.org/doc/draft-ietf-httpapi-linkset/)

Tests named `*-http-*` are meant to be published on a [Apache HTTPd](https://httpd.apache.org/) server using `.htaccess` rules to insert the `Link` http headers. These are currently deployed on <https://w3id.org/a2a-fair-metrics/> with PIDs corresponding to the `cite-as` links.

Tests named `*-html-*` can be consumed independently for testing for HTML `<link>` headers.

A [spreadsheet describing the individual benchmarks](https://docs.google.com/spreadsheets/d/1XWkHRldJDAAa733we2TFFBweUWu5w6lsC90LgQCAOoE/edit#gid=0) and the behaviours they are testing is available.  We _strongly encourage_ that anyone creating a new benchmark should add it into that spreadsheet to ensure clarity to help us to code the associated tests.

## License

![CC0](cc-zero.svg) [Creative Commons Zero v1.0 Universal](https://spdx.org/licenses/CC0-1.0)

SPDX-Identifier: CC0-1.0


## Contact

* [GitHub source](https://github.com/a2a-fair-metrics/a2a-fair-metrics/tree/main/benchmark)
* [GitHub issues](https://github.com/a2a-fair-metrics/a2a-fair-metrics/issues)
* [Slack](https://join.slack.com/t/applestoapples/shared_invite/zt-15iuqnirp-~91h2i4ltn1kdZdNPea0Xw)
* [Stian Soiland-Reyes](https://s11.no/) ([email](mailto:soiland-reyes@manchester.ac.uk))


## Running locally

For development you can run this locally using [Docker](https://www.docker.com/) by running:

    make docker

This will expose an Apache HTTPd on <http://localhost:8080/> (where the w3id base URL has been disabled).


## Adding tests

Use the `./clone-test.bash` tool to add additional tests. The numeric prefix is meant to be sequential and unique, but gaps are allowed.
In order to work as PIDs, there is a regular expression check for `^([0-9][0-9]*-[a-z0-9-]*)$` for the folder name.  This is enforced by a regular expression on w3id.org.

Remember to update both the `index.html` for humans and HTTP signposting in `.htaccess`, which generally use this style:

```
<Files crate-34.zip>  
  Header add Link <https://w3id.org/ro/crate>;rel="profile"
  Header add Link <https://s11.no/2022/a2a-fair-metrics/34-http-item-rocrate/>;rel="collection"
</Files>
```

The above only applies the header when a request is answered by the file `crate-34.zip`, similarly headers on the landing page should be set on `index.html` (which answers requests for `00-foo/` as well as `00-foo/index.html`).

If a link attribute contains spaces (e.g. multiple listings in `profile` or a human readable `title`) you will need to wrap the whole header with `"` quotes and escape the inner quotes to be transmitted with `\"`, e.g.

```
  Header add Link "<https://s11.no/2022/a2a-fair-metrics/34-http-item-rocrate/ro-crate-preview.html>;rel=\"describedby\";type=\"text/html\";profile=\"http://www.w3.org/ns/json-ld#flattened http://www.w3.org/ns/json-ld#compacted https://w3id.org/ro/crate\""
```
