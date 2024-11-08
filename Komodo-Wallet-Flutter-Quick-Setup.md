# Komodo Wallet Flutter Quick Setup

Welcome to the Komodo Wallet Flutter setup guide\! This comprehensive guide will walk you through setting up, running, and deploying the Komodo Wallet application. Whether you're a developer getting started with the project or looking to deploy for production, we've got you covered.

# Initial setup

1. Install Flutter and switch to the latest stable release if you aren’t already using it.   
   See Flutter’s official setup steps [here](https://docs.flutter.dev/get-started/install) or our setup steps [here](https://github.com/KomodoPlatform/komodo-wallet/blob/master/docs/INSTALL_FLUTTER.md) if you encounter issues.

   For developers: [Sidekick](https://github.com/fluttertools/sidekick) is an excellent tool for working with multiple Flutter versions on your machine.

2. Install NPM and Node.js if you don’t already have them installed. Verify installation by running node \--version and npm \--version

3. Clone komodo-wallet repo: [https://github.com/KomodoPlatform/komodo-wallet.git](https://github.com/KomodoPlatform/komodo-wallet.git)

4. Check out the *sia-wallet* branch.  
     
5. Clean the build folder and fetch dependencies by running the following:

|  flutter clean && flutter pub get |
| :---- |

# Running Locally

Run the Flutter app with the standard Flutter build command. For example, flutter run \-d chrome or press the launch in your IDE if the launch configurations are set up.

Do not commit the changes made under the *web* folder. You can mark them as excluded (or ignored) in your local git.

# Building and Publishing

1. Run the project locally per the section above, “*Running Locally*”, and verify that the app launches and you can create or login to a wallet.

2. Clear any existing builds and compile a fresh one

| flutter clean && flutter pub get && flutter build web \--release  |
| :---- |

### Deploying to web hosting

The *build/web* folder can be deployed to your preferred static web-hosting service. Alternatively, you can follow the steps below to set up and deploy to a Firebase Hosting project (free).

### Deploying to Firebase:

1. Create a new Firebase project at [https://console.firebase.google.com](https://console.firebase.google.com).

2. Install Firebase CLI

| npm install \-g firebase-tools |
| :---- |

3. Login to Firebase

| firebase login |
| :---- |

4. In your project folder, run Set up your project. Ensure “Hosting” and (optionally)  “Analytics” are selected. 

| firebase init |
| :---- |

   1. Select services you need (at minimum, select "Hosting")  
   2. Choose your Firebase project  
   3. *Detected an existing Flutter Web codebase in the current directory, should we use this?*: **Yes**  
   4. Select your preferred region for server-side content. Note: The application does not use this, but you may need the functionality in the future.

   5. *Set up automatic builds and deploys with GitHub?*: **No**

5. Deploy to Firebase

| firebase deploy |
| :---- |

6. Your app will be live. Check the terminal for the link to access the site; alternatively, check the Firebase Console website.

7. (Optional) Configure a custom domain: If you wish to host the site using your domain, follow the steps [here](https://firebase.google.com/docs/hosting/custom-domain). 

# Setup after checking out a new branch:

1. Terminate the build session.  
2. Run flutter clean   
3. Run flutter pub get  
4. Build/run the application as per the “Running Locally” section.

# Steps for initial iOS setup:

TODO

# Troubleshooting

Please provide feedback on any issues you encounter so we can assist you in resolving them by opening a [GitHub Issue](https://github.com/KomodoPlatform/komodo-wallet/issues/new?assignees=&labels=dev&projects=&template=dev.md&title=). This section will be updated to document them for others experiencing the same problem.