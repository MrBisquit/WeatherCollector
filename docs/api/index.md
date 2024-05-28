>[!WARNING]
>These are not yet available, clicking on links will take you no-where.

# API reference index
This is the index of all of the API routes, so it's easier to understand what everything does

| Section              | Route(s)                                  | Method | Links                                    | Description                                                                                           |
| -------------------- | ----------------------------------------- | ------ | ---------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| Config               | `/api/config`                             | `GET`  | [config](/api/config.md)                 | Fetches the config                                                                                    |
| Authentication       | `/api/whatsmytoken`                       | `GET`  | [whatsmytoken](/api/whatsmytoken.md)     | Fetches the token of the user requesting it                                                           |
| Data                 | `/api/latest`                             | `GET`  | [latest](/api/latest.md)                 | Fetches the latest data                                                                               |
| Image (Part of data) | `/api/latest/image`                       | `GET`  | [latest/image](/api/latest/image.md)     | Fetches the latest image                                                                              |
| AI predictions       | `/api/prediction`                         | `GET`  | [prediction](/api/prediction.md)         | Fetches the latest AI prediction (If enabled)                                                         |
| Taking photos        | `/take_photo`                             | `GET`  | [take_photo](/api/take_photo.md)         | Sends a photo request and recieves the image                                                          |
| Data (index)         | `/api/full`                               | `GET`  | [full](/api/full.md)                     | Fetches the index for all of the data (May get deprecated at some point)                              |
| Data                 | `/api/data/:year/:month/:day`             | `GET`  | [data/fetching](/api/data/fetching.md)   | Fetches an entire days worth of data                                                                  |
| Image (Part of data) | `/api/image/:year/:month/:day/:datapoint` | `GET`  | [image/fetching](/api/image/fetching.md) | Fetches an individual image                                                                           |
| Exporting            | `/api/export/:year/:month/:day`           | `GET`  | [export](/api/export.md)                 | Exports a day worth of data                                                                           |
| Setup                | `/api/db/providers`                       | `GET`  | [db/providers](/api/db/providers.md)     | Fetches all of the available (registered) database providers                                          |
| Authentication       | `/api/login`                              | `GET`  | [authentication](/api/authentication.md) | Authenticates a user (And gives a token as well as a cookie), will probably be re-done before release |

## Internal API reference index

| Section              | Route(s)       | Method | Links                                                    | Description                                                                         |
| -------------------- | -------------- | ------ | -------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| Database             | `/db/register` | `POST` | [internal/db/register](/api/internal/db/register.md)     | Registers a database provider (Needs to be done every so often in case it restarts) |
| Data                 | `/send_data`   | `POST` | [internal/data/sending](/api/internal/data/sending.md)   | Sends data to the server to be processed and saved                                  |
| Image (Part of data) | `/send_photo`  | `POST` | [internal/image/sending](/api/internal/image/sending.md) | Sends an image to the server to be processed and saved                              |