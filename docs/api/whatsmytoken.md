# What's my token API route
Returns the contents of the authentication cookie (Made something easier so I made it, probably won't be removed and may break stuff if you remove it)

- URL: `/api/whatsmytoken`
- Method: `GET`

## What it returns
What this API route returns

```json
{
    "token": "A long string"
}
```

>[!WARNING]
> If no cookie is present, it will return `undefined` as the token field.