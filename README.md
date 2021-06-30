# React + Firebase

**This project is a good starting point for any realtime project**

### Features
* **Security:** the logged in users ONLY allowed to enter the chat room
* **Sign in with Google accounts**
* **Realtime data straming:** each messages is a document in the firestore database contains: text, user id, time stamp for the message
* **Modern and responsive UI**

### Before Starting
* Create a new firebase project and copy your configs
* Replace the values of the "firebaseConfig" object in the App.js with your config values

### To Run The Project Locally
```sh
git clone https://github.com/mariazayed/react-chat-room.git
cd react-chat-room
npm install
npm start
```

### Cloud Firestore rules
**Replace the default firestore rules to the following code to allow the logged in users enter the chat room**
```sh
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if false;
    }
    
    match /messages/{docId} {
      allow read: if request.auth.uid != null;
      allow create: if canCreateMessage();
    }
    
    function canCreateMessage() {
      let isSignedIn = request.auth.uid != null;
      let isOwner = request.auth.uid == request.resource.data.uid;
     
      return isSignedIn && isOwner;
    }
  }
}
```

**Happy Coding! 😍**
