---
title: ストアド プロシージャのみによる操作のカスタマイズ
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 441e8ef3-998c-4d12-8825-ce66a178f90f
ms.openlocfilehash: 78db5cf448a19056d7265ab84d97d055748c3faa
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2020
ms.locfileid: "91164325"
---
# <a name="customizing-operations-by-using-stored-procedures-exclusively"></a>ストアド プロシージャのみによる操作のカスタマイズ

ストアド プロシージャのみを使用してデータにアクセスすることは、一般的なシナリオです。  
  
## <a name="example"></a>例  
  
### <a name="description"></a>説明  

 最初のクエリ (動的に SQL を実行するクエリ) をストアド プロシージャのラップ メソッド呼び出しで置き換えることで、「[ストアド プロシージャによる操作のカスタマイズ](customizing-operations-by-using-stored-procedures.md)」に用意されたサンプル コードを変更できます。  
  
 次の例に示すように、`CustomersByCity` がこのメソッドであることを前提とします。  
  
### <a name="code"></a>コード  

 [!code-csharp[DLinqOverrideDefaultSproc#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqOverrideDefaultSproc/cs/northwind.cs#4)]
 [!code-vb[DLinqOverrideDefaultSproc#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqOverrideDefaultSproc/vb/northwind.vb#4)]  
  
 次のコードは、動的 SQL を使わずに実行されます。  
  
 [!code-csharp[DLinqOverrideDefaultSproc#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqOverrideDefaultSproc/cs/Program.cs#5)]
 [!code-vb[DLinqOverrideDefaultSproc#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqOverrideDefaultSproc/vb/Module1.vb#5)]  
  
## <a name="see-also"></a>関連項目

- [既定の動作をオーバーライドするときの開発者の責任](responsibilities-of-the-developer-in-overriding-default-behavior.md)
