# Curl

### How to POST and format json
```sh
curl --url "http://some.endpoint.com" \
  -X POST  \
  # add headers with --header or -H
  --header "Content-Type: application/json"  \
  # administrator not typically needed, but if you need additional headers, add them here.
  --header "Administrator: Yes" \
  -d '{"quote_id":16067777 }' \
  | python3 -m json.tool
```
