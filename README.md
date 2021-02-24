# Reproduce https://github.com/Azure/azure-functions-host/issues/7176

There's a dev container for VS Code included to start quickly with all tools pre-installed.

Login with Azure CLI:

```bash
az login
```

Deploy infra:

```bash
cd terraform

terraform init

terraform apply
```

Check Azure Functions runtime version:

```
curl -sS 'https://<function app name>.azurewebsites.net/admin/host/status?code=<master key>' | jq
```

**Expected:** Version 2.xx (because of ~2.0 pinning)

**Actual:** Version 3.xx

Publish the function to print Node.js version:

```bash
func azure functionapp publish <function app name>
```

Check Node.js version:

```bash
curl https://<function app name>.azurewebsites.net/api/print-node-version
```

