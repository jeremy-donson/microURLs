## microURLs: TinyURL.com clone

- [Serviced From](https://github.com/opnchaudhary/flask-tinyurl-clone)

- v1: Create friendly url aliases that include utf8 support. Support performant lookups.
    - Develop [benchmarks](https://www.toptechskills.com/elixir-phoenix-tutorials-courses/benchmark-elixir-code-benchee/) for load testing baselines.

- We are looking to get V1 done for about $50.  Further versions will be revenue generating, so they will bear > hourly rate.

- We would like to leave v1 open source.  V2+ are proprietary for now.

- V1 benchmarks are discussed [here](docs/BENCHMARKS.md)

---

- Possible boilerplates: [Github Repo](https://github.com/toranb/elixir-url-shortener) • [medium article](https://medium.com/free-code-camp/how-to-write-a-super-fast-link-shortener-with-elixir-phoenix-and-mnesia-70ffa1564b3c) • [corresponding repo](https://github.com/bechurch/shorten_api_tutorial)

- This ugly UI will help us walk thru the logic...
![form](https://user-images.githubusercontent.com/34130568/148222599-3ce27d91-decc-4519-a9c5-a74b1e78ee38.png)

- Tests
  - 1. URL HTTP Query 1: Does that target URL exist on web?  Do we want to extract anything from header?  Go = True
  - 2. URL Database Query 2: Does that target URL exist in our database?  Good to know!
  - 3. URL HTTP Query 3: Does that friendly URL OR alias exist on web?  Extract from header? Go = False
  - 4. URL Database Query 4: Does that friendly URL exist in our database? Go = False
  - 5. [ True, False, False ] => Create new URL Alias: [ user_id, alias_id, alias, target_url, create_stamp ]  ??checksums??
  - 6. Test new url alias resolves to target URL.
  - 7. Show aliases per user.
  - 8. Identify all endpoints!!
  - 9. Set up batch processing requests: upload, verify format, GO rowcount, noGO rowcount, submit=run, report back and offer single button to test all in browser and generate equiv curl statements,

---

- Test Inputs:
  - role_id: public = 1
  - user_id: admin = 1
  - target_url: https://www.google.com
  - suggested_alias: 
  - friendly_alias: 

- Examples:  [ user_id, alias_id, alias, target_url ]
  - [ 1, 1, https://µ.domain.com/GoogleAlias1, http://www.google.com ]  => Success
  - [ 1, 2, https://µ.domain.com/GoogleAlias2, http://www.google.com ]  => Success
  - [ 1, 3, https://µ.domain.com/GoogleAlias3, http://www.google.com ]  => Success
  - [ 1, 4, https://µ.domain.com/GoogleAlias1, http://www.gloogle.com ] => FAIL on URL target not exists
  - [ 1, 4, https://µ.domain.com/GoogleAlias4, http://www.google.com ]  => Success
  - [ 1, 5, https://µ.domain.com/GoogleAlias1, http://www.google.com ]  => FAIL on URL Alias exists in database
  - [ 1, 5, https://µ.domain.com/你好世界, http://www.google.com ]      => Success

- Some testing we will need to clarify and set up.
  - TargetURLExists
  - GenerateShortAlias
  - AliasExistsAsURL
  - AliasExistsAsMicro
  - AliasExistsAsMicroTargetURLGone

- Hashes and hash ids and hash lookups are under the hood!
  - string2Hash
  - hash2HashID
  - hashID2Hash

- Endpoints
  - preflightGETs
  - actionPOST
  - lookupGET
  - requestBatchTokenPOST
  - batchPOST
  - reportBatchGET

- Performance tests:
  - POST batch tests => create hash and hash ID
  - GET batch  tests => resolve on hash and hash id => https://medium.com/@wttj_tech/elixir-how-to-distribute-mnesia-between-multiple-nodes-cb7c851b1ed1

- Rails7 Benchmarking tool: https://blog.saeloun.com/2021/02/25/rails-allows-benchmark-method-to-be-called-from-anywhere.html

- Deploy to Heroku for load testing.....

---
### These further versions will bear a higher hourly rate:

- Performance improvements should happen in parallel with providing two new features in v2:

  - v2: Add bulk upload option for $.
  - v2: Add custom domain options. Integrate with sofiasys.urbanspectra.net
  - Make this code proprietary.

- User Roles:
  - public
  - users
  - admins

- Cloud services we may wish to leverage: https://www.mitrais.com/news-updates/aws-amplify-vs-google-firebase-which-is-better/

- DynamoDB or cloud datastores could be used for hash uniqueness.  SQL database might be overkill?

- Universities can trade cloud credit for services:  https://edu.google.com/intl/ALL_us/programs/credits/research/?modal_active=none

---

- V3: Enhancement Configs:
  - dns
  - domains+subdomains
  - blacklisted referrers

- v3: Gather target page metadata and content. Generate page optimization suggestions.

  - Make this code proprietary.
  - Scan html for object graph metadata so that Custom URL aliases are rich urls.
``` <meta property="og:url" content="<?php the_permalink() ?>"/>  
<meta property="og:title" content="<?php single_post_title(''); ?>" />  
<meta property="og:description" content="<?php echo strip_tags(get_the_excerpt($post->ID)); ?>" />  
<meta property="og:type" content="article" />  
<meta property="og:image
```
