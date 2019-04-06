// code to apply firebase functions
const functions = require('firebase-functions');
//code to apply firebase admin
const admin = require('firebase-admin');
// code to initialize the firebase app
admin.initializeApp(functions.config().firebase);
// // Create and Deploy Your First Cloud Functions
// // https://firebase.google.com/docs/functions/write-firebase-functions
//
// exports.helloWorld = functions.https.onRequest((request, response) => {
//  response.send("Hello from Firebase!");
// });
// the main function which sends notification
exports.sendMessageNotification = functions.database.ref('/requests/{pushId}/des_rchd').onUpdate((change,context) => {
  //if (event.data.previous.exists()) {
  //  return;
  //}

	//firebase.database().ref('requests').child(event.params.).once('value').then(function(snap) {
    //var token = snap.val();
  //var topic = 'notifications_' + messageData.receiverKey;
  // code to find pushId from the database
  var eventPushId = context.params.pushId;
  // finding the reference of the database with which we could find message_token
  return admin.database().ref('/requests/' + eventPushId).child('message_token').once('value').then(snap =>{
    const token = snap.val();
    // actual message that a user recieves
    var payload = {
      notification: {
        title: "You got a new Message",
        body: "ARIS completed your request",
      }
    };
    // sendtodevice function to send push notification to a specific device
    admin.messaging().sendToDevice(token,payload)
        .then(function(response){
          console.log("Successfully sent message:", response);
        })
        .catch(function(error) {
          console.log("Error sending message:", error);
        });
  });
});

