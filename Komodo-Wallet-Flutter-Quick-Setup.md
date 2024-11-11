# Komodo Wallet Flutter Quick Setup

Welcome to the Komodo Wallet Flutter setup guide\! This comprehensive guide will walk you through setting up, running, and deploying the Komodo Wallet application. Whether you're a developer getting started with the project or looking to deploy for production, we've got you covered.

## Initial setup

1. Install Flutter and switch to the *3.22.3* release if you aren’t already using it.
   See Flutter’s official setup steps [here](https://docs.flutter.dev/get-started/install) or our setup steps [here](https://github.com/KomodoPlatform/komodo-wallet/blob/master/docs/INSTALL_FLUTTER.md) if you encounter issues.

   For developers: [Sidekick](https://github.com/fluttertools/sidekick) is an excellent tool for working with multiple Flutter versions on your machine.

2. Install NPM and Node.js, if you don’t already have them installed. Preferrably LTS versions *v20* or *v18*, which are known to work. There are known issues with the current *v22.** LTS release. Verify installation by running `node --version` and `npm --version`.

3. Clone komodo-wallet repo: [https://github.com/KomodoPlatform/komodo-wallet.git](https://github.com/KomodoPlatform/komodo-wallet.git)

4. Check out the *sia-wallet* branch.  

5. Clean the build folder and fetch dependencies by running the following. Coin icons and other assets are downloaded as part of the initial build, so it is expected to fail, but subsequent builds should succeed.

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

1. Create a new Firebase project at [https://console.firebase.google.com](https://console.firebase.google.com). Alternatively, do this later via the [Firebase CLI](https://firebase.google.com/docs/cli#management-commands).

2. Install Firebase CLI

   ```bash
   npm install -g firebase-tools
   ```

3. Login to Firebase

   ```bash
   firebase login
   ```

4. Add the Firebase project created in step 1. as an alias. Select the project you wish to use when prompted.

      ```bash
      firebase use --add
      ```

5. Configure Firebase Hosting in the project root directory:

   ```bash
   firebase init hosting
   ```

   1. What do you want to use as your public directory: `build/web`
   2. Configure as a single-page app (rewrite all urls to /index.html)?: `y`
   3. Set up automatic builds and deploys with GitHub?: `N`
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

## Steps for initial iOS setup (macOS only)

1. Install the latest version of [ruby](https://www.ruby-lang.org/en/documentation/installation/)

   ```bash
   brew install ruby
   ```

2. Install the lates version of [cocoapods](https://cocoapods.org/)

   ```bash
   sudo gem install cocoapods
   ```

3. Navigate to the *ios* folder in the project root and run the following command

   ```bash
   pod install
   ```

4. Build the iOS application (from the project root)

   ```bash
   flutter build ios --release --no-codesign
   ```

## Troubleshooting

Please provide feedback on any issues you encounter so we can assist you in resolving them by opening a [GitHub Issue](https://github.com/KomodoPlatform/komodo-wallet/issues/new?assignees=&labels=dev&projects=&template=dev.md&title=). This section will be updated to document them for others experiencing the same problem.
