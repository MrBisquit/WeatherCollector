# Getting started with WeatherCollector

Before jumping straight in, please make sure you have the right prerequisites ([View them here](/README.md#prerequisites))

## Using Docker
> [!NOTE]
> Not yet available

There are 2 docker images provided:
- First docker image contains
   - The files you should be using for the Raspberry Pi running inside
   - Features
      - 2 database providers
        - Flat files (Not a DB though)
        - PrismaDB (Can be a pain)
        - [You can also make your own](/docs/custom-db.md) and you'll probably want to
      - AI server
      - Base
      - 2 UIs
      - API
      - Will need Cloudflared setting up to support a website on a domain
    - Uses PM2 (PM2 Plus monitoring)
- The second docker image contains
   - The files you should be using for the Raspberry Pi running outside
     - Supports taking photos (Through the embedded camera port on the Raspberry Pi)
     - Takes data in, caches and then sends it through to the main Raspberry Pi
     - Supports manually taking photos
     - Hopefully will support other sensors like pollution sensors
     - Can provide power over SUB A &rightarrow; USB Micro to the Pimoroni Weather HAT
       - Since I'm sure no one wants to go outside every month to change some batteries
     - Uses PM2 (PM2 Plus monitoring)

## Doing it manually