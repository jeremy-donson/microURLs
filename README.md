## microURLs

- Inputs:
 - role_id: public = 1
 - user_id: admin = 1
 - target_url
 - friendly_alias

- Examples:
 - [ 1, 1, http://www.google.com, https://µ.domain.com/GoogleAlias1 ]  => Success
 - [ 1, 2, http://www.google.com, https://µ.domain.com/GoogleAlias2 ]  => Success
 - [ 1, 3, http://www.google.com, https://µ.domain.com/GoogleAlias3 ]  => Success
 - [ 1, 4, http://www.gloogle.com, https://µ.domain.com/GoogleAlias1 ] => FAIL on URL target not exists
 - [ 1, 4, http://www.google.com, https://µ.domain.com/GoogleAlias4 ]  => Success
 - [ 1, 5, http://www.google.com, https://µ.domain.com/GoogleAlias1 ]  => FAIL on URL Alias exists in database
 - [ 1, 6, http://www.google.com, https://µ.domain.com/你好世界！ ]      => Success

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

- User Roles:
 - Users
 - Devs
 - Admins

- Configs:
 - dns
 - domains+subdomains
 - blacklisted referrers

- Performance tests:
 - POST batch tests
 - GET batch  tests
