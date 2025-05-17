Key Terms
signInWithCredential Asynchronously signs in with the given credentials.

When registering your app with Google, you will need to provide the following for development in the Expo Go app:

Aplication Type: Web Application
URIs (Authorized JavaScript origins): https://auth.expo.io
Authorized redirect URIs: https://auth.expo.io/@your-username/your-project-slug
In the Firebase console activate Google as a provider.

Open "Web SDK configuration"
Save "Web client ID" you'll need it later
Replace YOUR_GUID with your "Web client ID" and open this link:
https://console.developers.google.com/apis/credentials/oauthclient/YOUR_GUID
Under "URIs" add your hosts URLs
Under "Authorized redirect URIs" add your hosts URLs
Web dev: https://localhost:19006
Expo Go Proxy: https://auth.expo.io
Under "Authorized redirect URIs"
Web dev: https://localhost:19006
Expo Go Proxy: https://auth.expo.io/@yourname/your-app
Dependencies
expo install expo-auth-session expo-random
expo install expo-web-browser
Google Sign In Component
import * as React from "react";
import * as WebBrowser from "expo-web-browser";
import * as Google from "expo-auth-session/providers/google";
import { Button } from "react-native";
import { auth } from "../../firebaseConfig";
import { GoogleAuthProvider, signInWithCredential } from "firebase/auth";
 
WebBrowser.maybeCompleteAuthSession();
 
export default function GoogleSignInButton() {
  const [request, response, promtAsync] = Google.useIdTokenAuthRequest({
    clientId: "yourCliendId.apps.googleusercontent.com",
  });
 
  React.useEffect(() => {
    if (response?.type === "success") {
      const { id_token } = response.params;
      const credential = GoogleAuthProvider.credential(id_token);
      signInWithCredential(auth, credential);
    }
  }, [response]);
 
  return (
    <Button
      title="Sign In with Google"
      disabled={!request}
      onPress={() => promtAsync()}
    />
  );
}
Resources
Code for this lesson https://github.com/betomoedano/react-navigation-example

See the Google Guide for more information https://docs.expo.dev/guides/authentication/#google
