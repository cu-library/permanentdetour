# permanentdetour
A tiny web service which redirects Sierra Web OPAC requests to Primo URLs.

```
Permanent Detour: A tiny web service which redirects Sierra Web OPAC requests to Primo URLs.
Usage: permanentdetour [flag...] [file...]
If 'landingpage' flag is supplied, redirects will go to page?dest=finaldest

  -address string
        Address to bind on. (default ":8877")
  -landingpage string
        Landing page for redirects. Optional.
  -primo string
        The subdomain of the target Primo instance, ?????.primo.exlibrisgroup.com. Required.
  -vid string
        VID parameter for Primo. Required.

  Environment variables read when flag is unset:
  PERMANENTDETOUR_ADDRESS
  PERMANENTDETOUR_LANDINGPAGE
  PERMANENTDETOUR_PRIMO
  PERMANENTDETOUR_VID

```

The following redirects are supported (with examples in the Carleton context):

- Permalinks. `/record=b2405380` is redirected to `https://ocul-crl.primo.exlibrisgroup.com/discovery/fulldisplay?docid=alma991018705459705153&vid=01OCUL_CRL:CRL_DEFAULT`
- Patron login. `/patroninfo` is redirected to `https://ocul-crl.primo.exlibrisgroup.com/discovery/login?vid=01OCUL_CRL:CRL_DEFAULT`
- Author index, call number index, and title search index. `/search/a?SEARCH=twain&sortdropdown=-&searchscope=9` is redirected to `https://ocul-crl.primo.exlibrisgroup.com/discovery/browse?browseQuery=twain&browseScope=author&vid=01OCUL_CRL:CRL_DEFAULT`
- Searches. `/search/?searchtype=t&SORT=D&searcharg=spiders&searchscope=9&submit=Submit` redirects to `https://ocul-crl.primo.exlibrisgroup.com/discovery/search?query=title,contains,spiders&search_scope=MyInst_and_CI&tab=Everything&vid=01OCUL_CRL:CRL_DEFAULT`

Searches are not automatically translated to Primo syntax. To do so would require lexing and parsing Sierra searches, which is outside the immediate scope of this tool.

The `landingpage` flag, if used, will redirect all requests to that landing page with the final destination url passed as the `dest` query parameter.
Check out https://github.com/cu-library/permanentdetour/wiki/Using-the-landingpage-parameter for some javascript for the landing page.
