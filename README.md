# form

Decodes and encodes HTML form bodies. It reads and writes `application/x-www-form-urlencoded` text with nested keys, parses and builds `multipart/form-data` bodies with file uploads, and adds a body parser for both to `web` applications.

```lus nocheck
local form = require("https://atmosp.here/2.0/form.lus")

local fields = form.decode("user[name]=Ada&tags[]=a&tags[]=b")
print(fields.user.name, #fields.tags)             --> Ada  2
print(form.encode({ user = { name = "Ada" } }))   --> user[name]=Ada

-- Parse an upload. Each file holds its bytes in a vector.
local parts = form.multipart(req.body, req.headers["content-type"], { max_file_size = 10 * 1024 * 1024 })
for _, file in ipairs(parts.files) do
    print(file.name, file.filename, file.content_type, #file.data)
end

-- Build a multipart body for network.fetch.
local body, content_type = form.encode_multipart({ title = "x", upload = { filename = "a.png", data = bytes } })
network.fetch(url, "POST", { ["Content-Type"] = content_type }, body)

-- As a web plugin, decode both body types into req.body and req.files.
app:register(form, { max_file_size = 5 * 1024 * 1024 })
app:post("/profile", function(req)
    return { name = req.body.user.name, uploads = #(req.files or {}) }
end)
```

The package requires Lus 2.0. It needs no permissions. It calls no `pledge` of its own, so the program that loads it keeps control of its permissions.

The reference is in the doc comments of `form.lus`. Run `lus doc form.lus` to print it.
