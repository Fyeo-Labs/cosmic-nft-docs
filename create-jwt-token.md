# create jwt token

- Go to dev.cosmicnft.io
- Click login on top right corner
- Login using Xaman app
- Open developer panel (Ctrl+shift+i or cmd+option+i)
- Click application tab
- Click https://dev.cosmicnft.com under Local storage on left nav
- Look for key `XummPkceJwt`
- Copy the `jwt` value in the JSON object of `XummPkceJwt`
- All mutation and authenticated queries will require this bearer token