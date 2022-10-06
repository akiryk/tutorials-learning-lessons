# Curl

### How to POST and format json
```sh
URL="http://whatever"
curl --url $URL \
  # use -X or --request to specify the type of request (GET, POST, etc)
  -X POST  \
  # add headers with --header or -H
  --header "Content-Type: application/json"  \
  # administrator not typically needed, but if you need additional headers, add them here.
  --header "Administrator: Yes" \
  -d '{"quote_id":16067777 }' \
  # output to json formatter
  | python3 -m json.tool
```
