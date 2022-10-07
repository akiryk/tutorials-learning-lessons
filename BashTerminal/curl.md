# Curl

### How to POST and format json

```sh
URL="http://whatever"

# use -X or --request to specify the type of request (GET, POST, etc)
# add headers with --header or -H
# then output to json formatter

curl --url $URL \
  -X POST  \
  --header "Content-Type: application/json"  \
  --header "Administrator: Yes" \
  -d '{"quote_id":16067777 }' | \
  python3 -m json.tool
```
