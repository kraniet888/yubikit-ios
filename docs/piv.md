## PIV Session

The `YKFPIVSession` provides access to the PIV application on a YubiKey. This allows the iOS application to enable or disable applications and transports on the YubiKey.

### Communicating with the PIV application on the YubiKey

Communication with the PIV application is done through the `YKFPIVSession` and the methods it expose. You obtain the session by calling `(void)pivSession:(YKFPIVSessionCallback _Nonnull)callback;` on a `YKFConnectionProcotol`. The method is guaranteed to either return the session or an error, never both nor neither.

#### Swift

```swift
connection.pivSession { session, error in
    guard let session = session else { /* handle error */ return }
    session.generateKey(in: .signature, type: .ECCP256) { publicKey, error in
        // Handle the response
    }
}
```

#### Objective-C

```objective-c
[connection pivSession:^(YKFPIVSession * session, NSError * error) {
    if (session == nil) { /* Handle error */ return; }
    [session generateKeyInSlot:YKFPIVSlotSignature type:YKFPIVKeyTypeECCP256 completion:^(NSData * publicKey, NSError * error) {
        // Handle the response
    }];
}];
```