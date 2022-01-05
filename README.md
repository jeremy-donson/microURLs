## microURLs: TinyURL.com clone

- v1: Create friendly url aliases that include utf8 support. Support performant lookups.  Develop [benchmarks](https://www.toptechskills.com/elixir-phoenix-tutorials-courses/benchmark-elixir-code-benchee/) for load testing baselines.
---

- Possible boilerplates: [Github Repo](https://github.com/toranb/elixir-url-shortener) • [medium article](https://medium.com/free-code-camp/how-to-write-a-super-fast-link-shortener-with-elixir-phoenix-and-mnesia-70ffa1564b3c) • [corresponding repo](https://github.com/bechurch/shorten_api_tutorial)

- Tests
  - 1. URL HTTP Query 1: Does that target URL exist on web?  Do we want to extract anything from header?  Go = True
  - 2. URL Database Query 2: Does that target URL exist in our database?  Good to know!
  - 3. URL HTTP Query 3: Does that friendly URL OR alias exist on web?  Extract from header? Go = False
  - 4. URL Database Query 4: Does that friendly URL exist in our database? Go = False
  - 5. [ True, False, False ] => Create new URL Alias: [ user_id, alias_id, alias, target_url, create_stamp ]  ??checksums??
  - 6. Test new url alias resolves to target URL.
  - 7. Show aliases per user.
  - 8. Separate preflight GETs from POSTs, and both from lookup GETs 
  - 9. Set up batch processing requests.

- Test Inputs:
  - role_id: public = 1
  - user_id: admin = 1
  - target_url
  - friendly_alias

- Examples:  [ user_id, alias_id, alias, target_url ]
  - [ 1, 1, http://www.google.com, https://µ.domain.com/GoogleAlias1 ]  => Success
  - [ 1, 2, http://www.google.com, https://µ.domain.com/GoogleAlias2 ]  => Success
  - [ 1, 3, http://www.google.com, https://µ.domain.com/GoogleAlias3 ]  => Success
  - [ 1, 4, http://www.gloogle.com, https://µ.domain.com/GoogleAlias1 ] => FAIL on URL target not exists
  - [ 1, 4, http://www.google.com, https://µ.domain.com/GoogleAlias4 ]  => Success
  - [ 1, 5, http://www.google.com, https://µ.domain.com/GoogleAlias1 ]  => FAIL on URL Alias exists in database
  - [ 1, 5, http://www.google.com, https://µ.domain.com/你好世界！ ]      => Success

- Performance tests:
  - POST batch tests
  - GET batch  tests

- Rails7 Benchmarking tool: https://blog.saeloun.com/2021/02/25/rails-allows-benchmark-method-to-be-called-from-anywhere.html

---
- These further versions will bear a higher hourly rate:

- Performance improvements should happen in parallel with providing two new features in v2:

  - v2: Add bulk upload option for $.
  - v2: Add custom domain options. Integrate with sofiasys.urbanspectra.net
  - Make this code proprietary.

- User Roles:
  - public
  - users
  - admins

---

- Enhancement Configs:
  - dns
  - domains+subdomains
  - blacklisted referrers

- v3: Gather target page metadata and content. Generate page optimization suggestions.

  - Make this code proprietary.
