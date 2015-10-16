# Cake.Gitter
Cake Addin that extend Cake with Gitter messaging features

## License
[![License](http://img.shields.io/:license-mit-blue.svg)](http://gep13.mit-license.org)

## Build Status

AppVeyor (develop)  | AppVeyor (master)
------------- | -------------
[![AppVeyor Develop Build Status](https://ci.appveyor.com/api/projects/status/j27gftbv67vgq05r/branch/develop?svg=true)](https://ci.appveyor.com/project/GaryEwanPark/cake-gitter) | [![AppVeyor Master Build Status](https://ci.appveyor.com/api/projects/status/j27gftbv67vgq05r/branch/master?svg=true)](https://ci.appveyor.com/project/GaryEwanPark/cake-gitter)


## Chat Room

Come join in the conversation about ChocolateyGUI in our Gitter Chat Room

[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/gep13/Cake.Gitter?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)

## Usage

### Post Message

#### Using Token

```
#addin "Cake.Slack"
var gitterToken         = EnvironmentVariable("GITTER_TOKEN");
var gitterRoomId        = EnvironmentVariable("gitterRoomId");

try
{
    var postMessageResult = Gitter.Chat.PostMessage(
                message:"Hello from Cake.Gitter API",
				        messageSettings:new GitterChatMessageSettings { Token = gitterToken, RoomId = gitterRoomId}
        );

    if (postMessageResult.Ok)
    {
        Information("Message {0} succcessfully sent", postMessageResult.TimeStamp);
    }
    else
    {
        Error("Failed to send message: {0}", postMessageResult.Error);
    }
}
catch(Exception ex)
{
    Error("{0}", ex);
}
```

Cake output will be similar to below:

```
Message 2015-10-16T11:18:14.078Z successfully sent
```

This will result in a message appearing in the Gitter Room similar to the following:

![image](https://cloud.githubusercontent.com/assets/1271146/10540458/1c5fd648-7400-11e5-9529-1f3729850300.png)

#### Using Web Hook Url

```
#addin "Cake.Slack"
var gitterWebHookUri    = EnvironmentVariable("gitterWebHookUri");
try
{
    var postMessageResult = Gitter.Chat.PostMessage(
                message:"Hello from Cake.Gitter WebHook",
                messageSettings:new GitterChatMessageSettings { IncomingWebHookUrl = gitterWebHookUri }
        );

    if (postMessageResult.Ok)
    {
        Information("Message {0} succcessfully sent", postMessageResult.TimeStamp);
    }
    else
    {
        Error("Failed to send message: {0}", postMessageResult.Error);
    }
}
catch(Exception ex)
{
    Error("{0}", ex);
}
```

Cake output will be similar to below:

```
Message 2015-10-16 11:26:23Z successfully sent
```

This will result in a message appearing in the Activity Feed for the Gitter Room similar to the following:

![image](https://cloud.githubusercontent.com/assets/1271146/10540466/2eb1905c-7400-11e5-89ad-6e58b6b7508b.png)

