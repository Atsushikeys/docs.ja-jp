---
title: カスタム データ サービス プロバイダー (WCF Data Services)
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, providers
ms.assetid: e702ecdb-3419-4743-92a9-c3c0e7d44082
ms.openlocfilehash: 4c92bf2f4e75b78cd6236c023246cc6c999086fa
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2020
ms.locfileid: "91186693"
---
# <a name="custom-data-service-providers-wcf-data-services"></a>カスタム データ サービス プロバイダー (WCF Data Services)

WCF Data Services には、遅延バインディング データ型に基づいてデータ モデルを定義できるプロバイダーのセットが含まれています。  
  
|プロバイダー|説明|  
|--------------|-----------------|  
|メタデータ プロバイダー|これは、<xref:System.Data.Services.Providers.IDataServiceMetadataProvider> インターフェイスを実装することによって実行時にカスタム データ モデルを定義できるコア カスタム データ サービス プロバイダーです。|  
|クエリ プロバイダー|このプロバイダーを使用すると、<xref:System.Data.Services.Providers.IDataServiceMetadataProvider> インターフェイスを使用して定義されたカスタム データ モデルに対してクエリを実行できます。 クエリ プロバイダーは、<xref:System.Data.Services.Providers.IDataServiceQueryProvider> インターフェイスを実装することによって作成されます。|  
|更新プロバイダー|このプロバイダーを使用すると、カスタム データ サービス プロバイダー内で公開されている型を更新してコンカレンシーを管理できます。 更新プロバイダーは、<xref:System.Data.Services.Providers.IDataServiceUpdateProvider> インターフェイスを実装することによって作成されます。|  
|ページング プロバイダー|このプロバイダーは、サーバー ドリブン ページング サポートを有効にするためにカスタム データ サービス プロバイダーと一緒に使用します。 カスタム データ サービスのページング プロバイダーは、<xref:System.Data.Services.Providers.IDataServicePagingProvider> インターフェイスを実装することによって作成されます。|  
|ストリーミング プロバイダー|このプロバイダーを使用すると、ストリームとしてバイナリ ラージ オブジェクト データ型を公開できます。 ストリーミング プロバイダーは、<xref:System.Data.Services.Providers.IDataServiceStreamProvider> インターフェイスを実装することによって作成されます。 ストリーミング プロバイダーは、Entity Framework プロバイダーおよびリフレクション データ ソース プロバイダーと共に使用することもできます。 詳細については、「[ストリーミング プロバイダー](streaming-provider-wcf-data-services.md)」を参照してください。|  
  
## <a name="see-also"></a>関連項目

- [Data Services プロバイダー](data-services-providers-wcf-data-services.md)
- [Entity Framework プロバイダー](entity-framework-provider-wcf-data-services.md)
- [リフレクション プロバイダー](reflection-provider-wcf-data-services.md)
