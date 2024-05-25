> [!WARNING]
> If you're using a Raspberry Pi running Raspbian, do not use MongoDB, it will not work and is not supported.

# Creating a custom database connector

There are a few API routes that need to be completed and working for WeatherCollector to be able to use it properly.

## API routes
| Route                  | Method | More info (Please read)                    |
|:-----------------------|:------:|:-------------------------------------------|
| `/`                    | `GET`  | [More info](#status-api-route)             |
| `/query/data/`         | `POST` | [More info](#data-query-api-route)         |
| `/query/images/`       | `POST` | [More info](#image-query-api-route)        |
| `/query/data/count/`   | `POST` | [More info](#data-count-query-api-route)   |
| `/query/images/count/` | `POST` | [More info](#images-count-query-api-route) |
| `/set/data/`           | `POST` | [More info](#set-data-api-route)           |
| `/set/image/`          | `POST` | [More info](#set-image-api-route)          |

### Registering the database
For a custom database connector to be recognised, it must send a request to the internal API (Default port: **90**).

To: `/db/register/`
Method: `POST`

| Item          | Required | Value type |
|:--------------|:--------:|:-----------|
| `name`        | Yes      | `string`   |
| `ip`          | Yes      | `string`   |
| `port`        | Yes      | `string`   |
| `version`     | Yes      | `string`   |
| `description` | Yes      | `string`   |
| `link`        | Yes      | `string`   |

Expected outcomes:
```js
{
    "success" : true,
    "alreadyRegistered" : true
}
```

```js
{
    "success" : true,
    "alreadyRegistered" : false
}
```

Then the database provider will show up, and if set as the default will be used, you may need to send this request every 15-30 seconds depending on how often it restarts, just so that if things restart the database will be registered again, if it doesn't detect the set database in the config, it will default to flat files.

### Status API route
This API route is basically to check that the database is running and get some basic information,
the expected outcome of this is as following:

```js
{
    // To check that it's working
    "success": true,
    "online": true,
    "message": "I am online.",

    // Statistics
    "stats": {
        "totalQueries": 0, // Total amount of queries since start
        "totalSaved": 0,   // Total amount of data/images saved.
        "startedAt": ""    // new Date()
    }
}
```

If there is an error, the expected output would be:

```js
{
    "success" : false,
    "err" : "500" // 500, etc...
}
```

### Data query API route
The API route for finding data in the database, for instance: finding all of the datapoints for a certain day.

Expected body (Raw JSON):

| Item    | Required | Value type |
|:--------|:--------:|:-----------|
| `year`  | Yes      | `number`   |
| `month` | No       | `number`   |
| `day`   | No       | `number`   |
| `dp`    | No       | `number`   |

Expected output:
```js
{
    "data" : [
        // This is just an example of what the data should look like
        // This'll output more than just this, with actual data as well
        {
            "dp" : 0,    // The datapoint (id) of the saved data
            "date" : "", // A Date object (As a string)

            "temp" : 0,           // Saved temperature  (°C)
            "humidity" : 0,       // Saved humidity     (%)
            "pressure" : 0,       // Saved air pressure (hPa)
            "light" : 0,          // Light              (lx)
            "wind_speed": 0,      // Wind speed         (m/s)
            "rain": 0,            // Rain               (mm)
            "rain_per_second": 0, // Rain per second    (mm/s)
            "wind_direction": 0,  // Wind direction     (°)

            // These exist purely for finding things easier
            "Year" : 0,  // Year saved
            "Month" : 0, // Month saved
            "Day" : 0    // Day saved
        }
    ],

    "success" : true // If the query was successful
}
```

If there is an error, the expected output would be:

```js
{
    "success" : false, // If the query was successful
    "err" : "404" // 404, 500, etc...
}
```

### Image query API route
The API route for finding images in the database, for instance: finding all images in a certain day.

Expected body (Raw JSON):

| Item    | Required | Value type |
|:--------|:--------:|:-----------|
| `year`  | Yes      | `number`   |
| `month` | No       | `number`   |
| `day`   | No       | `number`   |
| `dp`    | No       | `number`   |

Expected output:
```js
{
    "data" : [
        // This is just an example of what the data should look like
        // This'll output more than just this, with actual images as well
        {
            "dp" : 0,    // The datapoint (id) of the saved data
            "date" : "", // A Date object (As a string)

            "image" : "", // The image (Saved as Base64, or atleast converted to Base64 as this output)

            // These exist purely for finding things easier
            "Year" : 0,  // Year saved
            "Month" : 0, // Month saved
            "Day" : 0    // Day saved
        }
    ],

    "success": true // If the query was successful
}
```

If there is an error, the expected output would be:

```js
{
    "success" : false, // If the query was successful
    "err" : "404" // 404, 500, etc...
}
```

### Data count query API route
The API route for finding the count of how many items there are that match that query, for instance: finding the amount of datapoints taken on certain day

Expected body (Raw JSON):
| Item    | Required | Value type |
|:--------|:--------:|:-----------|
| `year`  | Yes      | `number`   |
| `month` | No       | `number`   |
| `day`   | No       | `number`   |
| `dp`    | No       | `number`   |

> [!NOTE]
> If you do set the `dp` value, it will be either `{ "success" : true, "count" : 1}` or `{ "success" : false, "err" : "404" }`.

Expected output:
```js
{
    "count" : 0, // The amount of datapoints found matching that query

    "success" : true // If the query was successful
}
```

If there is an error, the expected output would be:

```js
{
    "success" : false,
    "err" : "404" // 404, 500, etc...
}
```

### Images count query API route
The API route for finding the count of how many images there are that match that query, for instance: finding the amount of images taken on certain day

Expected body (Raw JSON):
| Item    | Required | Value type |
|:--------|:--------:|:-----------|
| `year`  | Yes      | `number`   |
| `month` | No       | `number`   |
| `day`   | No       | `number`   |
| `dp`    | No       | `number`   |

> [!NOTE]
> If you do set the `dp` value, it will be either `{ "success" : true, "count" : 1}` or `{ "success" : false, "err" : "404" }`.

Expected output:
```js
{
    "count" : 0, // The amount of images found matching that query

    "success" : true // If the query was successful
}
```

If there is an error, the expected output would be:

```js
{
    "success" : false,
    "err" : "404" // 404, 500, etc...
}
```

### Set data API route
The API route for setting a datapoint in the database.

Expected body (Raw JSON):
| Item              | Required | Value type |
|:------------------|:--------:|:-----------|
| `dp`              | Yes      | `number`   |
| `date`            | Yes      | `string`   |
| `temp`            | Yes      | `number`   |
| `humidity`        | Yes      | `number`   |
| `pressure`        | Yes      | `number`   |
| `light`           | Yes      | `number`   |
| `wind_speed`      | Yes      | `number`   |
| `rain`            | Yes      | `number`   |
| `rain_per_second` | Yes      | `number`   |
| `wind_direction`  | Yes      | `number`   |

Expected output:
```js
{
    "success": true // If setting the datapoint was successful
}
```

If there is an error, the expected output would be:

```js
{
    "success" : false // If setting the datapoint was successful
}
```

### Set image API route
The API route for setting an image in the database.

> [!NOTE]
> The image will be sent as Base64, you do not have to store it as Base64, but it sends it and expects it back as Base64.

Expected body (Raw JSON):
| Item    | Required | Value type |
|:--------|:--------:|:-----------|
| `dp`    | Yes      | `number`   |
| `date`  | Yes      | `string`   |
| `image` | Yes      | `string`   |

Expected output:
```js
{
    "success": true // If setting the datapoint was successful
}
```

If there is an error, the expected output would be:

```js
{
    "success" : false // If setting the datapoint was successful
}
```