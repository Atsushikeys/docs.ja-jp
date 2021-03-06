---
title: リプレイ攻撃
ms.date: 03/30/2017
ms.assetid: 7a17e040-93cd-4432-81b9-9f62fec78c8f
ms.openlocfilehash: 47a4726859605415b4e3e1b4d523f2f8059a3989
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84586300"
---
# <a name="replay-attacks"></a>リプレイ攻撃
*リプレイ攻撃*は、攻撃者がメッセージのストリームを2つのパーティ間でコピーし、そのストリームを1つ以上のパーティにリプレイする場合に発生します。 攻撃が和らげられていない場合、攻撃対象になったコンピューターはストリームを正当なメッセージとして処理するため、項目の順序が重複するなど、望ましくない状況に陥ります。  
  
## <a name="bindings-may-be-subject-to-reflection-attacks"></a>バインディングはリフレクション攻撃にさらされる可能性がある  
 *リフレクション攻撃*は、応答として受信者から送信されたメッセージと同じように、送信側からのメッセージを再生します。 Windows Communication Foundation (WCF) メカニズムでの標準の*再生検出*では、これは自動的には処理されません。  
  
 既定では、リフレクション攻撃が軽減されます。これは、WCF サービスモデルが署名付きメッセージ ID を要求メッセージに追加し、応答メッセージに署名済みヘッダーを要求するため `relates-to` です。 その結果、要求メッセージを応答としてリプレイできません。 セキュリティで保護された信頼できるメッセージ (RM) シナリオでは、リフレクション攻撃は次の理由で軽減されます。  
  
- シーケンス メッセージの作成スキーマとシーケンス応答メッセージの作成スキーマが異なります。  
  
- 一方向シーケンスの場合、クライアントから送信されたシーケンス メッセージをクライアントに対してリプレイすることはできません。これは、クライアントがこのようなメッセージを認識できないためです。  
  
- 双方向シーケンスの場合、2 つのシーケンス ID が一意である必要があります。 このため、送信シーケンス メッセージを受信シーケンス メッセージとしてリプレイできません (すべてのシーケンス ヘッダーと本文も署名されています)。  
  
 リフレクション攻撃の影響を受けやすい唯一のバインディングは WS-Addressing を使用しないバインディング (WS-Addressing を無効にして、対称キー ベースのセキュリティを使用するカスタム バインド) です。 <xref:System.ServiceModel.BasicHttpBinding> は、既定では WS-Addressing を使用しませんが、この攻撃を受けやすい方法で対称キー ベースのセキュリティを使用することはありません。  
  
 カスタム バインドに対する攻撃を軽減するには、セキュリティ コンテキストを確立しないか、WS-Addressing ヘッダーを要求します。  
  
## <a name="web-farm-attacker-replays-request-to-multiple-nodes"></a>Web ファーム : 攻撃者が複数のノードに対して要求をリプレイする  
 クライアントは、Web ファームに実装されているサービスを使用します。 攻撃者は、ファーム内の特定のノードに送信された要求を同じファーム内の別のノードに対してリプレイします。 また、サービスが再開されると、リプレイ キャッシュがフラッシュされ、攻撃者が要求をリプレイできるようになります  (このキャッシュには、以前使用されたメッセージ署名の値が格納されています。これにより、メッセージ署名は一度しか使用できないため、リプレイを防止できます。 リプレイ キャッシュは Web ファーム内で共有されません)。  
  
 回避事項を次に示します。  
  
- ステートフルなセキュリティ コンテキスト トークンと共にメッセージ モード セキュリティを使用します (セキュリティで保護されたメッセージ交換を有効にするかどうかは任意)。 詳細については、「[方法: セキュリティで保護されたセッションのセキュリティコンテキストトークンを作成](how-to-create-a-security-context-token-for-a-secure-session.md)する」を参照してください。  
  
- トランスポート レベルのセキュリティを使用するようにサービスを構成します。  
  
## <a name="see-also"></a>関連項目

- [セキュリティの考慮事項](security-considerations-in-wcf.md)
- [情報の公開](information-disclosure.md)
- [特権の昇格](elevation-of-privilege.md)
- [サービス拒否](denial-of-service.md)
- [改ざん](tampering.md)
- [サポートされていないシナリオ](unsupported-scenarios.md)
