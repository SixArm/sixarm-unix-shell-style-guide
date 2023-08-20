# URL encode and URL decode

Credit: https://stackoverflow.com/questions/296536/how-to-urlencode-data-for-curl-command

```sh
# Return a string in which the sequences with URL-sensitive characters are
# replaced with a percent sign then two hex digits. Compare url_decode.
url_encode() {
  local string="${1}"
  local strlen=${#string}
  local encoded=""
  local pos c o
  for (( pos=0 ; pos<strlen ; pos++ )); do
     c=${string:$pos:1}
     case "$c" in
        [-_.~a-zA-Z0-9] ) o="${c}" ;;
        * ) printf -v o '%%%02x' "'$c"
     esac
     encoded+="${o}"
  done
  echo "${encoded}"
}

# Return a string in which the sequences with percent (%) signs followed by
# two hex digits are replaced with literal characters. Compare url_encode.
url_decode() {
  # Because all escape characters must be encoded, we can replace %NN with \xNN
  # and pass the lot to printf -b, which will decode hex for us.
  printf -v REPLY '%b' "${1//%/\\x}" # You can either set a return variable (FASTER)
  echo "${REPLY}"
}
```
