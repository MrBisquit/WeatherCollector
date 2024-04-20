> [!NOTE]
> If you're wondering where the code is, I'm slowly going to be cleaning it up and building new bits onto it, since it was originally intended to be for personal-use, if you watch the repository hopefully it'll tell you when I add things to it.
> <br><br>This may take a little while, so please be patient.
> <br>If you have any questions, please DM or email me.

# Open-Source weather station data collector software

Open-source software for the Pimoroni Weather Kit (Or any other that can send weather data to a local HTTP endpoint) with support for a camera attached to a Raspberry Pi as well, really customisable, and swappable parts (If you don't want to use files, or Prisma DB, you can make your own DB connector, [find out how to](docs/custom-db.md)).

It has an AI model that automatically trains its self based on your data (Also optional) and can make predictions based on your collected weather data.

Will eventually have an app for computers and your phone that will allow a background process to continue to update the weather data (With your set interval) in a notification with alerts.

## Perquisites
Here's a list of things you'll need (* = Required)

- A raspberry Pi (*)
  - Or any other device, but a Raspberry Pi is recommended
  - 2 Optional but recommended (since you'll probably want one outside taking pictures)
  - If you're using it outside, make sure it's WiFi capable, also make sure that the WiFi signal reaches far enough for the Weather HAT (If you're using one) can connect.
- An external drive
  - [Find out how much storage it needs](docs/external-drive.md)
- A camera
  - I recommend this: [Raspberry Pi Camera Module 3](https://shop.pimoroni.com/products/raspberry-pi-camera-module-3?variant=40448391774291)
- Pimoroni Weather Kit (*)
  - You don't have to use it, but it's what it was built for.
  - [Enviro Weather (Pico W Aboard) - Weather Station Kit](https://shop.pimoroni.com/products/enviro-weather?variant=40056776917075)