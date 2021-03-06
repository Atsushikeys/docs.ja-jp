---
title: ICLRSyncManager インターフェイス
ms.date: 03/30/2017
api_name:
- ICLRSyncManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRSyncManager
helpviewer_keywords:
- ICLRSyncManager interface [.NET Framework hosting]
ms.assetid: a49f9d80-1c76-4ddd-8c49-34f913a5c596
topic_type:
- apiref
ms.openlocfilehash: b0b9c0b7d178557806a9ab2893bff2d34dc408ff
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/15/2020
ms.locfileid: "90557737"
---
# <a name="iclrsyncmanager-interface"></a>ICLRSyncManager インターフェイス
ホストが要求されたタスクに関する情報を取得し、その同期実装でデッドロックを検出できるようにするメソッドを定義します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[CreateRWLockOwnerIterator メソッド](iclrsyncmanager-createrwlockowneriterator-method.md)|リーダーライターロックを待機しているタスクのセットを決定するために使用するホストの反復子を共通言語ランタイム (CLR) が作成することを要求します。|  
|[DeleteRWLockOwnerIterator メソッド](iclrsyncmanager-deleterwlockowneriterator-method.md)|の呼び出しによって作成された反復子が CLR によって破棄されることを要求 `CreateRWLockOwnerIterator` します。|  
|[GetMonitorOwner メソッド](iclrsyncmanager-getmonitorowner-method.md)|指定したモニターを所有しているタスクを取得します。|  
|[GetRWLockOwnerNext メソッド](iclrsyncmanager-getrwlockownernext-method.md)|現在のリーダーライターロックを待機している次のタスクを取得します。|  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** MSCorEE.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Threading.Thread>
- [IHostSyncManager インターフェイス](ihostsyncmanager-interface.md)
- [マネージド スレッドとアンマネージド スレッド](/previous-versions/dotnet/netframework-4.0/5s8ee185(v=vs.100))
- [ホスト インターフェイス](hosting-interfaces.md)
