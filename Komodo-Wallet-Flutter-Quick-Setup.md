# Komodo Wallet Flutter Quick Setup

Welcome to the Komodo Wallet Flutter setup guide\! This comprehensive guide will walk you through setting up, running, and deploying the Komodo Wallet application. Whether you're a developer getting started with the project or looking to deploy for production, we've got you covered.

## Initial setup

1. Install Flutter and switch to the *3.22.3* release if you aren’t already using it.
   See Flutter’s official setup steps [here](https://docs.flutter.dev/get-started/install) or our setup steps [here](https://github.com/KomodoPlatform/komodo-wallet/blob/master/docs/INSTALL_FLUTTER.md) if you encounter issues.

   For developers: [Sidekick](https://github.com/fluttertools/sidekick) is an excellent tool for working with multiple Flutter versions on your machine.

2. Install NPM and Node.js (LTS) if you don’t already have them installed. Preferrably LTS versions *20* or *18*, which are known to work. There are known issues with the current LTS release (*22*) Verify installation by running `node --version` and `npm --version`.

3. Clone komodo-wallet repo: [https://github.com/KomodoPlatform/komodo-wallet.git](https://github.com/KomodoPlatform/komodo-wallet.git)

4. Check out the *sia-wallet* branch.  

5. Clean the build folder and fetch dependencies by running the following. Coin icons and other assets are downloaded as part of the initial build, so the first build is expected to fail, but subsequent runs should succeed.

```bash
flutter clean && flutter pub get && flutter build web --release > /dev/null 2>&1 || true
```

## Running Locally

Run the Flutter app with the standard Flutter build command. For example, `flutter run -d chrome` or press the launch in your IDE if the launch configurations are set up.

Do not commit the changes made under the *web* folder. You can mark them as excluded (or ignored) in your local git.

## Building and Publishing

1. Run the project locally per the section above, “*Running Locally*”, and verify that the app launches and you can create or login to a wallet.

2. Clear any existing builds and compile a fresh one. The build process is run twice in case new assets are downloaded during the first run, which would cause the build to fail - requiring a second run to succeed.

```bash
flutter clean && flutter pub get && flutter build web --release || flutter build web --release
```

### Deploying to web hosting

The *build/web* folder can be deployed to your preferred static web-hosting service. Alternatively, you can follow the steps below to set up and deploy to a Firebase Hosting project (free).

### Deploying to Firebase

1. Create a new Firebase project at [https://console.firebase.google.com](https://console.firebase.google.com).

2. Install Firebase CLI

   ```bash
   npm install -g firebase-tools
   ```

3. Login to Firebase

   ```bash
   firebase login
   ```

4. Create a Firebase project and add it as an alias (via the [Console](https://docs.appmachine.com/app-details/firebase/create-firebase-project) or the [CLI](https://firebase.google.com/docs/cli#management-commands)).
   1. (Optional) Create a project via the Firebase CLI if you don’t already have one.

      ```bash
      firebase projects:create <unique project name>
      ```

   2. Select the  Firebase project that you want to use, and add it as an alias.

      ```bash
      firebase use --add
      ```

5. Configure Firebase Hosting in the project root directory:

   ```bash
   firebase init hosting
   ```

   1. What do you want to use as your public directory: `build/web`
   2. Configure as a single-page app (rewrite all urls to /index.html)?: `y`
   3. Set up automatic builds and deployws with GitHub?: `N`
   4. File `build/web/index.html` already exists. Overwrite? `N`

6. (Optional) Test locally with `firebase serve`:

   ```bash
   firebase serve --only hosting
   ```

7. Deploy to Firebase

   ```bash
   firebase deploy --only hosting
   ```

8. Your app will be live. Check the terminal for the link to access the site; alternatively, check the Firebase Console website. You might need to change the site name in `firebase.json` in the project root if there are conflicts.

9. (Optional) Configure a custom domain: If you wish to host the site using your domain, follow the steps [here](https://firebase.google.com/docs/hosting/custom-domain).

## Setup after checking out a new branch

1. Terminate the build session.  
2. Run flutter clean
3. Run flutter pub get  
4. Build/run the application as per the “Running Locally” section.

## Steps for initial iOS setup

TODO

## Troubleshooting

Please provide feedback on any issues you encounter so we can assist you in resolving them by opening a [GitHub Issue](https://github.com/KomodoPlatform/komodo-wallet/issues/new?assignees=&labels=dev&projects=&template=dev.md&title=). This section will be updated to document them for others experiencing the same problem.
