---
author: mikben
ms.service: azure-communication-services
ms.topic: include
ms.date: 9/1/2020
ms.author: mikben
ms.openlocfilehash: 512b23b414328c0b7e9bbf8ef77a0d32083c84e5
ms.sourcegitcommit: b4647f06c0953435af3cb24baaf6d15a5a761a9c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/02/2021
ms.locfileid: "101661524"
---
## <a name="prerequisites"></a>Prérequis

- Compte Azure avec un abonnement actif. [Créez un compte gratuitement](https://azure.microsoft.com/free/?WT.mc_id=A261C142F). 
- Une ressource Communication Services déployée. [Créez une ressource Communication Services](../../create-communication-resource.md).
- Un `User Access Token` pour activer le client d’appel. Pour en savoir plus, consultez [Comment obtenir un `User Access Token`](../../access-tokens.md)
- Facultatif : Suivez le guide de démarrage rapide pour [prendre en main l’ajout des appels à votre application](../getting-started-with-calling.md)

## <a name="setting-up"></a>Configuration

### <a name="creating-the-xcode-project"></a>Création du projet Xcode

> [!NOTE]
> Ce document utilise la version 1.0.0-beta.8 de la bibliothèque de client appelante.

Dans Xcode, créez un projet iOS et sélectionnez le modèle **Single View App**. Ce démarrage rapide utilise le [framework SwiftUI](https://developer.apple.com/xcode/swiftui/) ; vous devez donc définir **Swift** comme **langage** et **SwiftUI** comme **interface utilisateur**. Vous n’allez pas créer de tests unitaires ou de tests d’interface utilisateur au cours de ce guide de démarrage rapide. N’hésitez pas à désactiver **Include Unit Tests** et **Include UI Tests**.

:::image type="content" source="../media/ios/xcode-new-ios-project.png" alt-text="Capture d’écran représentant la fenêtre de création de projet dans Xcode.":::

### <a name="install-the-package-and-dependencies-with-cocoapods"></a>Installer le package et les dépendances avec CocoaPods

1. Créez un Podfile pour votre application, comme suit :

   ```
   platform :ios, '13.0'
   use_frameworks!
   target 'AzureCommunicationCallingSample' do
     pod 'AzureCommunicationCalling', '~> 1.0.0-beta.8'
     pod 'AzureCommunication', '~> 1.0.0-beta.8'
     pod 'AzureCore', '~> 1.0.0-beta.8'
   end
   ```

2. Exécutez `pod install`.
3. Ouvrez le `.xcworkspace` avec Xcode.

### <a name="request-access-to-the-microphone"></a>Demander l’accès au microphone

Pour accéder au microphone de l’appareil, vous devez mettre à jour la liste des propriétés d’informations de votre application avec un `NSMicrophoneUsageDescription`. Vous affectez une valeur `string` comme valeur associée qui sera incluse dans la boîte de dialogue affichée par le système pour demander l’accès à l’utilisateur.

Cliquez avec le bouton droit sur l’entrée `Info.plist` de l’arborescence du projet, puis sélectionnez **Open As** > **Source Code**. Ajoutez les lignes suivantes dans la section `<dict>` tout en haut, puis enregistrez le fichier.

```xml
<key>NSMicrophoneUsageDescription</key>
<string>Need microphone access for VOIP calling.</string>
```

### <a name="set-up-the-app-framework"></a>Configurer le framework d’application

Ouvrez le fichier **ContentView.swift** de votre projet et ajoutez une déclaration `import` en haut du fichier pour importer l’`AzureCommunicationCalling library`. Importez également `AVFoundation`. Nous en aurons besoin pour la demande d’autorisation audio dans le code.

```swift
import AzureCommunicationCalling
import AVFoundation
```

## <a name="object-model"></a>Modèle objet

Les classes et les interfaces suivantes gèrent certaines des principales fonctionnalités de la bibliothèque de client Appel Azure Communication Services pour iOS.


| Nom                                  | Description                                                  |
| ------------------------------------- | ------------------------------------------------------------ |
| CallClient | CallClient est le point d’entrée principal de la bibliothèque de client Appel.|
| CallAgent | CallAgent sert à démarrer et à gérer les appels. |
| CommunicationTokenCredential | CommunicationTokenCredential est utilisé comme informations d’identification du jeton pour instancier CallAgent.| 
| CommunicationIdentifier | CommunicationIdentifier sert à représenter l’identité de l’utilisateur qui peut être l’une des suivantes : CommunicationUserIdentifier/PhoneNumberIdentifier/CallingApplication. |

> [!NOTE]
> Lors de l’implémentation des délégués d’événements, l’application doit contenir une référence forte aux objets qui requièrent des abonnements aux événements. Par exemple, lorsqu’un objet `RemoteParticipant` est retourné lors de l’appel de la méthode `call.addParticipant` et que l’application définit le délégué pour l’écoute du trafic sur `RemoteParticipantDelegate`, l’application doit contenir une référence forte à l’objet `RemoteParticipant`. Sinon, si cet objet est collecté, le délégué générera une exception irrécupérable lorsque le kit de développement logiciel (SDK) appelant tente d’appeler l’objet.

## <a name="initialize-the-callagent"></a>Initialiser CallAgent

Pour créer une instance de `CallAgent` à partir d’`CallClient`, vous devez utiliser la méthode `callClient.createCallAgent` qui retourne de manière asynchrone un objet `CallAgent` une fois qu’elle est initialisée

Pour créer un client d’appel, vous devez passer un objet `CommunicationTokenCredential`.

```swift

import AzureCommunication

let tokenString = "token_string"
var userCredential: CommunicationTokenCredential?
var userCredential: CommunicationTokenCredential?
   do {
       userCredential = try CommunicationTokenCredential(with: CommunicationTokenRefreshOptions(initialToken: token, 
                                                                     refreshProactively: true,
                                                                     tokenRefresher: self.fetchTokenSync))
   } catch {
       return
}

// tokenProvider needs to be implemented by contoso which fetches new token
public func fetchTokenSync(then onCompletion: TokenRefreshOnCompletion) {
    let newToken = self.tokenProvider!.fetchNewToken()
    onCompletion(newToken, nil)
}
```

Transmettez l’objet `CommunicationTokenCredential` créé plus haut à `CallClient` et définissez le nom d’affichage.

```swift

callClient = CallClient()
let callAgentOptions:CallAgentOptions = CallAgentOptions()!
options.displayName = " iOS User"

callClient?.createCallAgent(userCredential: userCredential!,
    options: callAgentOptions) { (callAgent, error) in
        if error == nil {
            print("Create agent succeeded")
            self.callAgent = callAgent
        } else {
            print("Create agent failed")
        }
})

```

## <a name="place-an-outgoing-call"></a>Passer un appel sortant

Pour créer et démarrer un appel, vous devez appeler l’une des API sur `CallAgent` et fournir l’identité Azure Communication Services d’un utilisateur que vous avez configuré à l’aide de la bibliothèque cliente de management des services de communication.

La création et le démarrage de l’appel sont synchrones. Vous recevrez une instance d’appel qui vous permet de vous abonner à tous les événements de l’appel.

### <a name="place-a-11-call-to-a-user-or-a-1n-call-with-users-and-pstn"></a>Passer un appel 1:1 à un utilisateur ou un appel 1:n avec des utilisateurs et RTC

```swift

let callees = [CommunicationUser(identifier: 'UserId')]
let oneToOneCall = self.callAgent.call(participants: callees, options: StartCallOptions())

```

### <a name="place-a-1n-call-with-users-and-pstn"></a>Passer un appel 1:n avec des utilisateurs et un RTC
Pour passer l’appel RTC, vous devez spécifier le numéro de téléphone acquis avec les services Azure Communication Services
```swift

let pstnCallee = PhoneNumberIdentifier(phoneNumber: '+1999999999')
let callee = CommunicationUserIdentifier(identifier: 'UserId')
let groupCall = self.callAgent.call(participants: [pstnCallee, callee], options: StartCallOptions())

```

### <a name="place-a-11-call-with-with-video"></a>Passer un appel 1:1 avec vidéo
Pour obtenir une instance du gestionnaire de périphériques, consultez [ici](#device-management)

```swift

let camera = self.deviceManager!.cameras!.first
let localVideoStream = LocalVideoStream(camera: camera)
let videoOptions = VideoOptions(localVideoStream: localVideoStream)

let startCallOptions = StartCallOptions()
startCallOptions?.videoOptions = videoOptions

let callee = CommunicationUserIdentifier(identifier: 'UserId')
let call = self.callAgent?.call(participants: [callee], options: startCallOptions)

```

### <a name="join-a-group-call"></a>Rejoindre un appel de groupe
Pour rejoindre un appel, vous devez appeler l’une des API sur *CallAgent*

```swift

let groupCallLocator = GroupCallLocator(groupId: UUID(uuidString: "uuid_string"))!
let call = self.callAgent?.join(with: groupCallLocator, joinCallOptions: JoinCallOptions())

```

### <a name="subscribe-for-incoming-call"></a>S’abonner à un appel entrant
S’abonner à un événement d’appel entrant

```
final class IncomingCallHandler: NSObject, CallAgentDelegate, IncomingCallDelegate
{
    // Event raised when there is an incoming call
    public func onIncomingCall(_ callAgent: CallAgent!, incomingcall: IncomingCall!) {
        self.incomingCall = incomingcall
        // Subscribe to get OnCallEnded event
        self.incomingCall?.delegate = self
    }

    // Event raised when incoming call was not answered
    public func onCallEnded(_ incomingCall: IncomingCall!, args: PropertyChangedEventArgs!) {
        self.incomingCall = nil
    }
}
```

### <a name="accept-an-incoming-call"></a>Acceptation d’un appel entrant
Pour accepter un appel, appelez la méthode « accept » sur un objet call.
Définition d’un délégué sur CallAgent 
```swift
final class CallHandler: NSObject, CallAgentDelegate
{
    public var incomingCall: Call?
 
    public func onCallsUpdated(_ callAgent: CallAgent!, args: CallsUpdatedEventArgs!) {
        if let incomingCall = args.addedCalls?.first(where: { $0.isIncoming }) {
            self.incomingCall = incomingCall
        }
    }
}

let firstCamera: VideoDeviceInfo? = self.deviceManager!.cameras!.first
let localVideoStream = LocalVideoStream(camera: firstCamera)
let acceptCallOptions = AcceptCallOptions()
acceptCallOptions!.videoOptions = VideoOptions(localVideoStream:localVideoStream!)
if let incomingCall = CallHandler().incomingCall {
   incomingCall.accept(options: acceptCallOptions) { (call, error) in
               if error == nil {
                   print("Incoming call accepted")
               } else {
                   print("Failed to accept incoming call")
               }
           }
} else {
   print("No incoming call found to accept")
}
```

## <a name="push-notification"></a>Notification Push

La notification Push mobile est la notification contextuelle que vous recevez sur un appareil mobile. Pour l’appel, nous utilisons des notifications Push VoIP (Voice over Internet Protocol). Nous vous offrirons la possibilité de vous inscrire et vous désinscrire aux notifications Push, ainsi que de les gérer.

### <a name="prerequisite"></a>Prérequis

- Étape 1 : Xcode -> Signature et fonctionnalités -> Ajouter une fonctionnalité -> « Notifications Push »
- Étape 2 : Xcode -> Signature et fonctionnalités -> Ajouter une fonctionnalité -> « Background Modes » (Modes d’arrière-plan)
- Étape 3 : « Background Modes » (Modes d’arrière-plan) -> sélectionner « Voix sur IP » et « Remote notifications » (Notifications distantes)

:::image type="content" source="../media/ios/xcode-push-notification.png" alt-text="Capture d’écran montrant comment ajouter des fonctionnalités dans Xcode." lightbox="../media/ios/xcode-push-notification.png":::

#### <a name="register-for-push-notifications"></a>Inscription aux notifications Push

Pour s’inscrire aux notifications Push, appelez registerPushNotification() sur une instance *CallAgent* avec un jeton d’inscription d’appareil.

L’inscription à la notification push doit être appelée après l’initialisation réussie. Lorsque l’objet `callAgent` est détruit, `logout` est appelé, ce qui annule automatiquement l’enregistrement des notifications push.


```swift

let deviceToken: Data = pushRegistry?.pushToken(for: PKPushType.voIP)
callAgent.registerPushNotifications(deviceToken: deviceToken) { (error) in
    if(error == nil) {
        print("Successfully registered to push notification.")
    } else {
        print("Failed to register push notification.")
    }
}

```

#### <a name="push-notification-handling"></a>Gestion des notifications Push
Pour recevoir les notifications Push d’appels entrants, appelez *handlePushNotification()* sur une instance *CallAgent* avec une charge utile de dictionnaire.

```swift

let callNotification = IncomingCallInformation.from(payload: pushPayload?.dictionaryPayload)

callAgent.handlePush(notification: callNotification) { (error) in
    if (error != nil) {
        print("Handling of push notification failed")
    } else {
        print("Handling of push notification was successful")
    }
}

```
#### <a name="unregister-push-notification"></a>Désinscription aux notifications Push

Les applications peuvent se désinscrire des notifications Push à tout moment. Appelez simplement la méthode `unregisterPushNotification` sur *CallAgent*.
> [!NOTE]
> Les applications ne sont pas automatiquement désinscrites de la notification Push lors de la déconnexion.

```swift

callAgent.unregisterPushNotifications { (error) in
    if (error != nil) {
        print("Unregister of push notification failed, please try again")
    } else {
        print("Unregister of push notification was successful")
    }
}

```

## <a name="mid-call-operations"></a>Opérations durant l’appel

Vous pouvez effectuer différentes opérations lors d’un appel pour gérer les paramètres liés à la vidéo et à l’audio.

### <a name="mute-and-unmute"></a>Activer et désactiver le son

Pour activer ou désactiver le son du point de terminaison local, vous pouvez utiliser les API asynchrones `mute` et `unmute`  :

```swift
call!.mute { (error) in
    if error == nil {
        print("Successfully muted")
    } else {
        print("Failed to mute")
    }
}

```

[Asynchrone] Réactivation locale du son

```swift
call!.unmute { (error) in
    if error == nil {
        print("Successfully un-muted")
    } else {
        print("Failed to unmute")
    }
}
```

### <a name="start-and-stop-sending-local-video"></a>Démarrer et arrêter l’envoi d’une vidéo locale

Pour commencer à envoyer une vidéo locale à d’autres participants de l’appel, utilisez l’API `startVideo` et transmettez `localVideoStream` avec `camera`

```swift

let firstCamera: VideoDeviceInfo? = self.deviceManager!.cameras!.first
let localVideoStream = LocalVideoStream(camera: firstCamera)

call!.startVideo(stream: localVideoStream) { (error) in
    if (error == nil) {
        print("Local video started successfully")
    } else {
        print("Local video failed to start")
    }
}

```

Une fois que vous avez commencé à envoyer de la vidéo, l’instance de `LocalVideoStream` est ajoutée à la collection `localVideoStreams` sur une instance d’appel :

```swift

call.localVideoStreams[0]

```

[Asynchrone] Pour arrêter la vidéo locale, transmettez le `localVideoStream` retourné depuis l’appel de `call.startVideo` :

```swift

call!.stopVideo(stream: localVideoStream) { (error) in
    if (error == nil) {
        print("Local video stopped successfully")
    } else {
        print("Local video failed to stop")
    }
}

```

## <a name="remote-participants-management"></a>Gestion des participants distants

Tous les participants distants sont représentés par le type `RemoteParticipant` et sont disponibles via la collection `remoteParticipants` sur une instance d’appel :

### <a name="list-participants-in-a-call"></a>Lister les participants d’un appel

```swift

call.remoteParticipants

```

### <a name="remote-participant-properties"></a>Propriétés du participant distant

```swift

// [RemoteParticipantDelegate] delegate - an object you provide to receive events from this RemoteParticipant instance
var remoteParticipantDelegate = remoteParticipant.delegate

// [CommunicationIdentifier] identity - same as the one used to provision token for another user
var identity = remoteParticipant.identity

// ParticipantStateIdle = 0, ParticipantStateEarlyMedia = 1, ParticipantStateConnecting = 2, ParticipantStateConnected = 3, ParticipantStateOnHold = 4, ParticipantStateInLobby = 5, ParticipantStateDisconnected = 6
var state = remoteParticipant.state

// [Error] callEndReason - reason why participant left the call, contains code/subcode/message
var callEndReason = remoteParticipant.callEndReason

// [Bool] isMuted - indicating if participant is muted
var isMuted = remoteParticipant.isMuted

// [Bool] isSpeaking - indicating if participant is currently speaking
var isSpeaking = remoteParticipant.isSpeaking

// RemoteVideoStream[] - collection of video streams this participants has
var videoStreams = remoteParticipant.videoStreams // [RemoteVideoStream, RemoteVideoStream, ...]

```

### <a name="add-a-participant-to-a-call"></a>Ajouter un participant à un appel

Pour ajouter un participant à un appel (un utilisateur ou un numéro de téléphone), vous pouvez appeler `addParticipant`. Cette opération retourne une instance de participant distant de façon synchrone .

```swift

let remoteParticipantAdded: RemoteParticipant = call.add(participant: CommunicationUserIdentifier(identifier: "userId"))

```

### <a name="remove-a-participant-from-a-call"></a>Supprimer un participant d’un appel
Pour supprimer un participant d’un appel (un utilisateur ou un numéro de téléphone), vous pouvez appeler l’API `removeParticipant`. Cela est résolu de façon asynchrone.

```swift

call!.remove(participant: remoteParticipantAdded) { (error) in
    if (error == nil) {
        print("Successfully removed participant")
    } else {
        print("Failed to remove participant")
    }
}

```

## <a name="render-remote-participant-video-streams"></a>Afficher les flux vidéo des participants distants

Les participants distants peuvent lancer un partage vidéo ou d’écran pendant un appel.

### <a name="handle-remote-participant-videoscreen-sharing-streams"></a>Gérer les flux de partage d’écran/vidéo de participants distants

Pour répertorier les flux de participants distants, examinez les collections `videoStreams` :

```swift

var remoteParticipantVideoStream = call.remoteParticipants[0].videoStreams[0]

```

### <a name="remote-video-stream-properties"></a>Propriétés du flux vidéo distant

```swift

var type: MediaStreamType = remoteParticipantVideoStream.type // 'MediaStreamTypeVideo'

var isAvailable: Bool = remoteParticipantVideoStream.isAvailable // indicates if remote stream is available

var id: Int = remoteParticipantVideoStream.id // id of remoteParticipantStream

```

### <a name="render-remote-participant-stream"></a>Afficher le flux des participants distants

Pour commencer à afficher les flux des participants distants :

```swift

let renderer: Renderer? = Renderer(remoteVideoStream: remoteParticipantVideoStream)
let targetRemoteParticipantView: RendererView? = renderer?.createView(with: RenderingOptions(scalingMode: ScalingMode.crop))
// To update the scaling mode later
targetRemoteParticipantView.update(scalingMode: ScalingMode.fit)

```

### <a name="remote-video-renderer-methods-and-properties"></a>Méthodes et propriétés du renderer vidéo à distance

```swift
// [Synchronous] dispose() - dispose renderer and all `RendererView` associated with this renderer. To be called when you have removed all associated views from the UI.
remoteVideoRenderer.dispose()
```

## <a name="device-management"></a>Gestion des appareils

`DeviceManager` permet d’énumérer les périphériques locaux qui peuvent être utilisés dans un appel pour transmettre des flux audio/vidéo. Il vous permet également de demander l’autorisation à un utilisateur d’accéder au microphone/à la caméra. Vous pouvez accéder à `deviceManager` sur l’objet `callClient`  :

```swift

self.callClient!.getDeviceManager { (deviceManager, error) in
        if (error == nil) {
            print("Got device manager instance")
            self.deviceManager = deviceManager
        } else {
            print("Failed to get device manager instance")
        }
    }
```

### <a name="enumerate-local-devices"></a>Énumérer les appareils locaux

Pour accéder aux appareils locaux, vous pouvez utiliser les méthodes d’énumération sur le gestionnaire d’appareils. L’énumération est une action synchrone.

```swift
// enumerate local cameras
var localCameras = deviceManager.cameras! // [VideoDeviceInfo, VideoDeviceInfo...]
// enumerate local cameras
var localMicrophones = deviceManager.microphones! // [AudioDeviceInfo, AudioDeviceInfo...]
// enumerate local cameras
var localSpeakers = deviceManager.speakers! // [AudioDeviceInfo, AudioDeviceInfo...]
``` 

### <a name="set-default-microphonespeaker"></a>Définir le microphone/haut-parleur par défaut

Le gestionnaire d’appareils vous permet de définir un appareil par défaut qui sera utilisé lors du démarrage d’un appel. Si les valeurs par défaut de la pile ne sont pas définies, Azure Communication Services bascule vers les valeurs par défaut du système d’exploitation.

```swift
// get first microphone
var firstMicrophone = self.deviceManager!.cameras!.first
// [Synchronous] set microphone
deviceManager.setMicrophone(microphoneDevice: firstMicrophone)
// get first speaker
var firstSpeaker = self.deviceManager!.speakers!
// [Synchronous] set speaker
deviceManager.setSpeaker(speakerDevice: firstSpeaker)
```

### <a name="local-camera-preview"></a>Aperçu de la caméra locale

Vous pouvez utiliser `Renderer` pour commencer à afficher un flux à partir de votre caméra locale. Ce flux n’est pas envoyé à d’autres participants ; il s’agit d’un flux d’aperçu local. Il s’agit d’une action asynchrone.

```swift

let camera: VideoDeviceInfo = self.deviceManager!.getCameraList()![0]
let localVideoStream: LocalVideoStream = LocalVideoStream(camera: camera)
let renderer: Renderer = Renderer(localVideoStream: localVideoStream)
self.view = try renderer!.createView()

```

### <a name="local-camera-preview-properties"></a>Propriétés de l’aperçu de la caméra locale

Le renderer a un ensemble de propriétés et de méthodes qui vous permettent de contrôler le rendu :

```swift

// Constructor can take in LocalVideoStream or RemoteVideoStream
let localRenderer = Renderer(localVideoStream:localVideoStream)
let remoteRenderer = Renderer(remoteVideoStream:remoteVideoStream)

// [StreamSize] size of the rendering view
localRenderer.size

// [RendererDelegate] an object you provide to receive events from this Renderer instance
localRenderer.delegate

// [Synchronous] create view
try! localRenderer.createView()

// [Synchronous] create view with rendering options
try! localRenderer.createView(with: RenderingOptions(scalingMode: ScalingMode.fit))

// [Synchronous] dispose rendering view
localRenderer.dispose()

```

## <a name="eventing-model"></a>Modèle d’événement

Vous pouvez vous abonner à la plupart des propriétés et collections pour être averti quand des valeurs changent.

### <a name="properties"></a>Propriétés
Pour vous abonner à des événements `property changed` :

```swift
call.delegate = self
// Get the property of the call state by doing get on the call's state member
public func onCallStateChanged(_ call: Call!,
                               args: PropertyChangedEventArgs!)
{
    print("Callback from SDK when the call state changes, current state: " + call.state.rawValue)
}

 // to unsubscribe
 self.call.delegate = nil

```

### <a name="collections"></a>Collections
Pour vous abonner à des événements `collection updated` :

```swift
call.delegate = self
// Collection contains the streams that were added or removed only
public func onLocalVideoStreamsChanged(_ call: Call!,
                                       args: LocalVideoStreamsUpdatedEventArgs!)
{
    print(args.addedStreams.count)
    print(args.removedStreams.count)
}
// to unsubscribe
self.call.delegate = nil
```
