---
title: Windows フォームに関する破壊的変更
description: .NET Core および .NET 5 の Windows フォームにおける破壊的変更の一覧を示します。
ms.date: 09/08/2020
ms.openlocfilehash: 3e7d077d07203d9c231ae4a7805e593c5432c135
ms.sourcegitcommit: aa6d8a90a4f5d8fe0f6e967980b8c98433f05a44
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/16/2020
ms.locfileid: "90679002"
---
# <a name="breaking-changes-in-windows-forms"></a>Windows フォームでの破壊的変更

Windows フォームのサポートは、.NET Core にバージョン 3.0 で追加されました。 この記事では、Windows フォームの破壊的変更を、導入された .NET のバージョン別に説明します。 この記事は、.NET Framework または以前のバージョンの .NET Core (3.0 以降) から Windows フォーム アプリをアップグレードするユーザーを対象としています。

このページでは、次の破壊的変更について説明します。

| 互換性に影響する変更点 | 導入されたバージョン |
| - | :-: |
| [WPF アプリと WinForms アプリで OutputType が WinExe に設定されている](#outputtype-set-to-winexe-for-wpf-and-winforms-apps) | 5.0 |
| [DataGridView 関連の API が InvalidOperationException をスローするようになった](#datagridview-related-apis-now-throw-invalidoperationexception) | 5.0 |
| [WinForms と WPF アプリで Microsoft.NET.Sdk が使用される](#winforms-and-wpf-apps-use-microsoftnetsdk) | 5.0 |
| [削除されたステータス バー コントロール](#removed-status-bar-controls) | 5.0 |
| [WinForms メソッドで ArgumentException がスローされるようになった](#winforms-methods-now-throw-argumentexception) | 5.0 |
| [WinForms メソッドで ArgumentNullException がスローされるようになった](#winforms-methods-now-throw-argumentnullexception) | 5.0 |
| [WinForms プロパティによる ArgumentOutOfRangeException のスロー](#winforms-properties-now-throw-argumentoutofrangeexception) | 5.0 |
| [削除されたコントロール](#removed-controls) | 3.1 |
| [ヒントが表示されていると CellFormatting が発生しない](#cellformatting-event-not-raised-if-tooltip-is-shown) | 3.1 |
| [Control.DefaultFont を Segoe UI 9 pt に変更](#default-control-font-changed-to-segoe-ui-9-pt) | 3.0 |
| [FolderBrowserDialog の最新化](#modernization-of-the-folderbrowserdialog) | 3.0 |
| [一部の Windows フォーム型から SerializableAttribute を削除](#serializableattribute-removed-from-some-windows-forms-types) | 3.0 |
| [AllowUpdateChildControlIndexForTabControls 互換性スイッチがサポートされない](#allowupdatechildcontrolindexfortabcontrols-compatibility-switch-not-supported) | 3.0 |
| [DomainUpDown.UseLegacyScrolling 互換性スイッチがサポートされない](#domainupdownuselegacyscrolling-compatibility-switch-not-supported) | 3.0 |
| [DoNotLoadLatestRichEditControl 互換性スイッチがサポートされない](#donotloadlatestricheditcontrol-compatibility-switch-not-supported) | 3.0 |
| [DoNotSupportSelectAllShortcutInMultilineTextBox 互換性スイッチがサポートされない](#donotsupportselectallshortcutinmultilinetextbox-compatibility-switch-not-supported) | 3.0 |
| [DontSupportReentrantFilterMessage 互換性スイッチがサポートされない](#dontsupportreentrantfiltermessage-compatibility-switch-not-supported) | 3.0 |
| [EnableVisualStyleValidation 互換性スイッチがサポートされない](#enablevisualstylevalidation-compatibility-switch-not-supported) | 3.0 |
| [UseLegacyContextMenuStripSourceControlValue 互換性スイッチがサポートされない](#uselegacycontextmenustripsourcecontrolvalue-compatibility-switch-not-supported) | 3.0 |
| [UseLegacyImages 互換性スイッチがサポートされない](#uselegacyimages-compatibility-switch-not-supported) | 3.0 |

## <a name="net-50"></a>.NET 5.0

[!INCLUDE [automatically-infer-winexe-output-type](../../../includes/core-changes/windowsforms/5.0/automatically-infer-winexe-output-type.md)]

***

[!INCLUDE [null-owner-causes-invalidoperationexception](../../../includes/core-changes/windowsforms/5.0/null-owner-causes-invalidoperationexception.md)]

***

[!INCLUDE [sdk-and-target-framework-change](../../../includes/core-changes/windowsforms/5.0/sdk-and-target-framework-change.md)]

***

[!INCLUDE [winforms-deprecated-controls](../../../includes/core-changes/windowsforms/5.0/winforms-deprecated-controls.md)]

***

[!INCLUDE [invalid-args-cause-argumentexception](../../../includes/core-changes/windowsforms/5.0/invalid-args-cause-argumentexception.md)]

***

[!INCLUDE [null-args-cause-argumentnullexception](../../../includes/core-changes/windowsforms/5.0/null-args-cause-argumentnullexception.md)]

***

[!INCLUDE [invalid-args-cause-argumentoutofrangeexception](../../../includes/core-changes/windowsforms/5.0/invalid-args-cause-argumentoutofrangeexception.md)]

***

## <a name="net-core-31"></a>.NET Core 3.1

[!INCLUDE[Removed controls](~/includes/core-changes/windowsforms/3.1/remove-controls-3.1.md)]

***

[!INCLUDE[CellFormatting event](~/includes/core-changes/windowsforms/3.1/cellformatting-event-not-raised.md)]

***

## <a name="net-core-30"></a>.NET Core 3.0

[!INCLUDE[Control.DefaultFont changed to Segoe UI 9pt](~/includes/core-changes/windowsforms/3.0/control-defaultfont-changed.md)]

***

[!INCLUDE[Modernization of the FolderBrowserDialog](~/includes/core-changes/windowsforms/3.0/modernized-folderbrowserdialog.md)]

***

[!INCLUDE[SerializableAttribute removed from some Windows Forms types](~/includes/core-changes/windowsforms/3.0/remove-serializationattribute.md)]

***

[!INCLUDE[Switch.System.Windows.Forms.AllowUpdateChildControlIndexForTabControls compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-allowupdatechildcontrolindexfortabcontrols.md)]

***

[!INCLUDE[Switch.System.Windows.Forms.DomainUpDown.UseLegacyScrolling compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-uselegacyscrolling.md)]

***

[!INCLUDE[Switch.System.Windows.Forms.DoNotLoadLatestRichEditControl compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-donotloadlatestricheditcontrol.md)]

***

[!INCLUDE[Switch.System.Windows.Forms.DoNotSupportSelectAllShortcutInMultilineTextBox compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-donotsupportselectallshortcutinmultilinetextbox.md)]

***

[!INCLUDE[Switch.System.Windows.Forms.DontSupportReentrantFilterMessage compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-dontsupportreentrantfiltermessage.md)]

***

[!INCLUDE[Switch.System.Windows.Forms.EnableVisualStyleValidation compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-enablevisualstylevalidation.md)]

***

[!INCLUDE[Switch.System.Windows.Forms.UseLegacyContextMenuStripSourceControlValue compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-uselegacycontextmenustripsourcecontrolvalue.md)]

***

[!INCLUDE[Switch.System.Windows.Forms.UseLegacyImages compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-uselegacyimages.md)]

***

## <a name="see-also"></a>関連項目

- [Windows フォーム アプリを .NET Core に移植する](../porting/winforms.md)
