>[!WARNING]
>These are not yet available, clicking on links will take you no-where.

# API reference index
This is the index of all of the API routes, so it's easier to understand what everything does

| Section              | Route(s)                                  | Method | Links                                    | Description                                                                                           |
| -------------------- | ----------------------------------------- | ------ | ---------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| Config               | `/api/config`                             | `GET`  | [config](/docs/api/config.md)                 | Fetches the config                                                                                    |
| Authentication       | `/api/whatsmytoken`                       | `GET`  | [whatsmytoken](/docs/api/whatsmytoken.md)     | Fetches the token of the user requesting it                                                           |
| Data                 | `/api/latest` or `/api/latest/image`      | `GET`  | [latest](/docs/api/latest.md)                 | Fetches the latest data / Fetches the latest image                                                    |
| AI predictions       | `/api/prediction`                         | `GET`  | [prediction](/docs/api/prediction.md)         | Fetches the latest AI prediction (If enabled)                                                         |
| Taking photos        | `/take_photo`                             | `GET`  | [take_photo](/docs/api/take_photo.md)         | Sends a photo request and recieves the image                                                          |
| Data (index)         | `/api/full`                               | `GET`  | [full](/docs/api/full.md)                     | Fetches the index for all of the data (May get deprecated at some point)                              |
| Data                 | `/api/data/:year/:month/:day`             | `GET`  | [data/fetching](/docs/api/data/fetching.md)   | Fetches an entire days worth of data                                                                  |
| Image (Part of data) | `/api/image/:year/:month/:day/:datapoint` | `GET`  | [image/fetching](/docs/api/image/fetching.md) | Fetches an individual image                                                                           |
| Exporting            | `/api/export/:year/:month/:day`           | `GET`  | [export](/docs/api/export.md)                 | Exports a day worth of data                                                                           |
| Setup                | `/api/db/providers`                       | `GET`  | [db/providers](/docs/api/db/providers.md)     | Fetches all of the available (registered) database providers                                          |
| Authentication       | `/api/login`                              | `GET`  | [authentication](/docs/api/authentication.md) | Authenticates a user (And gives a token as well as a cookie), will probably be re-done before release |

## Internal API reference index
If your setup is different, you will need to work out how this needs to be setup for it to work, it may need a little tweaking.

### Inside Raspberry Pi
Routes exposed to the internal network via another port (**Needs** to be accessible to the other Raspberry Pi taking photos and recieving data from your Weather HAT otherwise it **will not work**).
Unless you have it set up differently and it's only running on one Raspberry Pi, in that case you need to make sure that they can communicate and that the port on the other Node.JS server is open so that your Weather HAT can send it data.

### Main part

| Section              | Route(s)       | Method | Links                                                    | Description                                                                         |
| -------------------- | -------------- | ------ | -------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| Database             | `/db/register` | `POST` | [internal/db/register](/docs/api/internal/db/register.md)     | Registers a database provider (Needs to be done every so often in case it restarts) |
| Data                 | `/send_data`   | `POST` | [internal/data/sending](/docs/api/internal/data/sending.md)   | Sends data to the server to be processed and saved                                  |
| Image (Part of data) | `/send_photo`  | `POST` | [internal/image/sending](/docs/api/internal/image/sending.md) | Sends an image to the server to be processed and saved                              |

### Database server
| Section  | Route(s)                                    | Method | Links                                                                       | Description                                                |
| -------- | ------------------------------------------- | ------ | --------------------------------------------------------------------------- | ---------------------------------------------------------- |
| Status   | `/`                                         | `GET`  | [internal/db_server/status](/docs/api/internal/db_server/status.md)              | Fetches the status/stats of the database server            |
| Database | `/query/data`                               | `POST` | [internal/db_server/query/data](/docs/api/internal/db_server/query/data.md)      | Queries the database for data                              |
| Database | `/query/images`                             | `POST` | [internal/db_server/query/images](/docs/api/internal/db_server/query/images.md)  | Queries the database for images                            |
| Database | `/query/data/count` or `/query/data/images` | `POST` | [internal/db_server/query/count.md](/docs/api/internal/db_server/query/count.md) | Queries the database to get the count of datapoints/images |
| Database | `/set/data`                                 | `POST` | [internal/db_server/set/data](/docs/api/internal/db_server/set/data.md)          | Sets data in the database                                  |
| Database | `/set/image`                                | `POST` | [internal/db_server/set/image](/docs/api/internal/db_server/set/image.md)        | Sets an image in the database                              |

### AI server

### Outside Raspberry Pi