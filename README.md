# mock-datasource

Stationary JSON served raw from GitHub, read by the samples through the `hashicorp/http` data source as a stand-in for a real remote data source — no server, no credentials:

```hcl
data "http" "stack" {
  url = "https://raw.githubusercontent.com/snapcd-samples/mock-datasource/main/stack.json"
}

locals {
  stack = jsondecode(data.http.stack.response_body)
}
```

`stack.json` and `runner.json` each back one data source. The values feed `keepers` blocks, so they must never change: an edit would force resource replacements in every deployment that reads them.
