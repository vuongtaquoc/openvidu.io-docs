<h2 id="section-title">openvidu-java-client API</h2>
<hr>

> NOTE: all input parameters ("Parameters" columns) are listed in strict order, optional ones in _italics_

| Class        | Description   										     |
| ------------ | ------------------------------------------------------- |
| [OpenVidu](#openvidu)     | Use it to create all the sessions you need |
| [Session](#session)      | Allows for the creation of tokens |
| [OpenViduRole](#openvidurole) | Enum that defines the values accepted by _TokenOptions.Builder.role(OpenViduRole role)_ method |
| [TokenOptions](#tokenoptions) | Customize each token with this class when generating them |

#### **OpenVidu**
| Method         | Returns | Parameters | Description |
| -------------- | ------- | --------------------------------------------- | ----------- |
| OpenVidu() | | `String:urlOpenViduServer`<br>`String:secret` | The constructor receives the URL of your OpenVidu Server and the secret shared with it |
| createSession() | [Session](#session) |  | Get a Session object by calling this method. You can then store it as you want |

#### **Session**
| Method         | Returns | Parameters  | Description |
| -------------- | ------- | --------------------------------------------- | ----------- |
| getSessionId() | String |  | Returns the unique identifier of the session. You will need to return this parameter to the client side to pass it during the connection process to the session |
| generateToken() | String | _`TokenOptions:tokenOptions`_  | The value returned is required in the client side just as the sessionId in order to connect to a session |

#### **OpenViduRole**
| Enum       | Description |
| ---------- | ------- |
| SUBSCRIBER | They can subscribe to published streams of other users |
| PUBLISHER  | They can subscribe to published streams of other users and publish their own streams|
| MODERATOR  | They can subscribe to published streams of other users, publish their own streams and force _unpublish()_ and _disconnect()_ over a third-party stream or user |

#### **TokenOptions**
| Method         | Returns | Parameters | Description |
| -------------- | ------- | -------------------------------------------| -- |
| getData() | String |        | Returns the metadata associated to the token |
| getRole() | [OpenViduRole](#openvidurole) |  | Returns the role associated to the token     |

##### **TokenOptions.Builder**
_(inner static class)_

| Method         | Returns | Parameters | Description |
| -------------- | ------- | --------------------------------------------- | ----------- |
| TokenOptions.Builder() |  |  | Constructor |
| build() | [TokenOptions](#tokenoptions) |  | Returns a new **TokenOptions** object with the stablished properties. Default values if methods _data()_ and _role()_ are not called are an empty string and OpenViduRole.PUBLISHER, respectively |
| data() | [TokenOptions.Builder](#tokenoptionsbuilder) | `String:data` | Some extra metadata to be associated to the user through its token. The structure of this string is up to you (maybe some standarized format as JSON or XML is a good idea), the only restriction is a maximum length of 1000 chars |
| role() | [TokenOptions.Builder](#tokenoptionsbuilder) | `OpenViduRole:role` | The role associated to this token |
