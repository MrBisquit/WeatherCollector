# Config API route
Fetches the basic config from the server, without any of the admin credentials or anything like that

- URL: `/api/config`
- Method: `GET`

## What it returns
What this API route returns

### Successful
If the request is successful, it should return something a little like this
```json
{
    "config" : {
        "UseReact" : false,
        "requires_setup" : true,

        "selected_db_provider" : "PrismaDB",
    },
    "success" : true
}
```

### Unsuccessful
>[!NOTE]
> If the user is not logged in, it currently returns a login page (Not good, hopefully will change later)

Hopefully once I've made it nicer, if unauthenticated it should return:
```json
{
    "success" : false
}
```