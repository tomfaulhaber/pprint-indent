# Pretty Print Dispatch with Indenting #

This sample code shows you how to modify the clojure pretty printer to do "non-lisp" style indenting, with brackets on their own line and elements indented 2 spaces instead of one.

To use it, include:

```clj
(:use indent.indent :only [indent-dispatch]) 
```

in your `ns` directive.

Then use `with-pprint-dispatch` to prefer `indent-dispatch`:

```clj
user> (def h {:remote-addr "127.0.0.1", :scheme :http, :query-params {},
:session {}, :form-params {}, :request-method :get, :query-string nil,
:content-type nil, :cookies {"ring-session" {:value
"b3493c6e-40c3-441c-a75a-19d1a67e7b8d"}}, :uri "/", :server-name
"localhost", :params {}, :headers {"cache-control" "max-age=0",
"cookie" "ring-session=b3493c6e-40c3-441c-a75a-19d1a67e7b8d",
"accept-charset" "ISO-8859-1,utf-8;q=0.7,*;q=0.3", "accept-language"
"en-US,en;q=0.8", "accept-encoding" "gzip,deflate,sdch", "accept"
"text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8",
"user-agent" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_6_8)
AppleWebKit/534.30 (KHTML, like Gecko) Chrome/12.0.742.122
Safari/534.30", "connection" "keep-alive", "host" "localhost:8080"},
:content-length nil, :server-port 8080, :character-encoding nil, :body
nil }) 
#'user/h
user> (with-pprint-dispatch indent.indent/indent-dispatch (pprint h))
{
  :remote-addr "127.0.0.1",
  :scheme :http,
  :query-params {},
  :session {},
  :form-params {},
  :request-method :get,
  :query-string nil,
  :content-type nil,
  :cookies
  {"ring-session" {:value "b3493c6e-40c3-441c-a75a-19d1a67e7b8d"}},
  :uri "/",
  :server-name "localhost",
  :params {},
  :headers
  {
    "user-agent"
    "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_6_8)\nAppleWebKit/534.30 (KHTML, like Gecko) Chrome/12.0.742.122\nSafari/534.30",
    "cookie" "ring-session=b3493c6e-40c3-441c-a75a-19d1a67e7b8d",
    "accept-charset" "ISO-8859-1,utf-8;q=0.7,*;q=0.3",
    "accept"
    "text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8",
    "host" "localhost:8080",
    "cache-control" "max-age=0",
    "accept-encoding" "gzip,deflate,sdch",
    "accept-language" "en-US,en;q=0.8",
    "connection" "keep-alive"
  },
  :content-length nil,
  :server-port 8080,
  :character-encoding nil,
  :body nil
}
nil
user> 
```

### Notes ###
This isn't currently built into a jar on clojars or anywhere, but I suppose I could if anyone really wanted it.

This implementation is somewhat slower than the normal simple-dispatch owing to pprint's current architecture. (Format statements are really compiled in the current cl-format.)

To change the indent to 4, go through the code and change occurences of ~1i to ~3i. Leave the ~-1i format alone.