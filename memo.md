memo

webrtc
    web real time communicationの略
    APIでもありプロトコルでもある
    APIはjavascriptのみで規定されている
    プロトコルはjavascript以外の言語でも利用可能であり、さまざまなOSSで提供されている。
    プロトコルはIETFのrtcwebというワーキンググループで管理されている。
        https://datatracker.ietf.org/wg/rtcweb/documents/
    APIはW3Cのwebrtcで文書化されている
        https://www.w3.org/TR/webrtc/
        
    主に4つのプロセスで行われる
        シグナリング
        接続
        セキュリティの確保
        通信

シグナリング
    webrtcでピアがお互いを見つける方法。
    既存のプロトコルであるSDP(session description protocol)を使用する。

    SDP(session description protocol)
        プレーンテキストのプロトコル
        sdpメッセージはキーバリューのペアで構成される
    
    シグナリングはwebrtcを使用して行われるわけではない。

接続
    ICE(Interactive connectivity Establishment)を用いることで、直接接続を確立する
    これを可能にするのは、NATトラバーサル と STUN/TURNサーバー

セキュリティの確保
    安全なDTLSと