---
title: '方法: ファイル名とパスを検証する'
ms.date: 07/20/2015
helpviewer_keywords:
- file names [Visual Basic], validating
- strings [Visual Basic], validating
- Boolean values [Visual Basic]
- paths [Visual Basic], validating
ms.assetid: f673462d-57b7-4120-b13a-6a7592f7ab2c
ms.openlocfilehash: b722222ea8b8088a6b326eef27147c08f8419272
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "91072653"
---
# <a name="how-to-validate-file-names-and-paths-in-visual-basic"></a>方法: Visual Basic でファイル名とパスを検証する

この例では、文字列がファイル名とパスのどちらを表すかを示す `Boolean` 値が返されます。 この検証では、ファイル システムで許可されていない文字が名前に含まれているかどうかがチェックされます。  
  
## <a name="example"></a>例  

 [!code-vb[VbVbcnRegEx#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnRegEx/VB/Class1.vb#4)]  
  
 この例では、名前にコロンが正しく配置されていないか、名前のないディレクトリがあるか、または名前の長さがシステム定義の最大長を超えているかどうかはチェックされません。 また、アプリケーションが指定された名前のファイル システム リソースにアクセスするアクセス許可を持っているかどうかもチェックされません。  
  
## <a name="see-also"></a>関連項目

- <xref:System.IO.Path.GetInvalidPathChars%2A>
- [Visual Basic における文字列の検証](validating-strings.md)
