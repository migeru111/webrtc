参考
    https://webrtcforthecurious.com/ja/

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
        rfc8866で定義されてる
            https://tools.ietf.org/html/rfc8866
        
        読み方
            各行は、以下の形式で表現される
                {keyとなるある一文字}={value}

        webrtcでは一部のキーしか使用しない。
            rfc8829で定義されたキーのみ重要
                https://datatracker.ietf.org/doc/html/rfc8829
                v - バージョン(Version)、0 と同じでなければなりません。
                o - オリジン(Origin)、再交渉に便利なユニークな ID を含む。
                s - セッション名(Session Name)、- と同じでなければなりません。
                t - タイミング(Timing)、0 0 と同じでなければなりません。
                m - メディア記述(Media Description: m=<media> <port> <proto> <fmt> ...)、詳細は以下の通りです。
                a - 属性(Attribute)、フリーテキストのフィールドです。これは WebRTC で最も一般的な行です。
                c - 接続データ(Connection Data)、 IN IP4 0.0.0.0 と等しくなければなりません。
        
        メディア記述
            0個以上のメディア記述からなり、無制限に含めることができる
            メディア記述はメディアの１つのストリームに対応する
        
        オファーとアンサー
            webrtcはオファー/アンサーモデルを使用している
                一方がオファーを出して通話をかけ、もう一方がオファーを受け入れるかを決定する。
                これによりコーデックやメディア記述を拒否するきっかけを与える。

        トランシーバー
            webrtc特有の概念
            メディア記述をjavascriptAPIに公開するもの
            各メディア記述はトランシーバーになる
            トランシーバーを作成するたびに、新しいメディア記述がトランシーバーに追加される
            各メディア記述はdirection属性を持つ。
                direction属性により、コーデックの送受信の有無を宣言できる
                有効な値は以下の４つ
                    send (送信)
                    recv (受信)
                    sendrecv (送受信)
                    inactive (非アクティブ)

    
    シグナリングはwebrtcを使用して行われるわけではない。

接続
    ICE(Interactive connectivity Establishment)を用いることで、直接接続を確立する
    これを可能にするのは、NATトラバーサル と STUN/TURNサーバー

セキュリティの確保
    安全な通信の確立のために、以下二つのプロトコルを使用する。
        DTLS(datagram transport layer securrity)
            udp上のTLSに過ぎない
        SRTP secure realtime transport protocol
        
    