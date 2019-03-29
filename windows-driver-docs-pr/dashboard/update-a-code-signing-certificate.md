---
title: コード署名証明書の追加または更新
description: コード署名証明書の追加または更新
ms.assetid: 120AA970-D981-4E7D-A9BD-68125D90A0EE
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7c3f1b42f1269f4666a73744d415e93c8cbf959
ms.sourcegitcommit: a58b4859254a651502e4329a6e521fe0fa11c7f2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/15/2019
ms.locfileid: "56519012"
---
# <a name="add-or-update-a-code-signing-certificate"></a>コード署名証明書の追加または更新

デジタル証明書の情報を最新に保つのは、ハードウェア デベロッパー センター ダッシュボード管理者の役割です。 元の証明書の有効期限が切れたときは、新しい証明書を入手し、その新しいデジタル証明書で署名した新しいファイルをアップロードする必要があります。 

ハードウェア デベロッパー センターでは、1 つのアカウントに複数の証明書を関連付けることができます。  追加の証明書を追加する場合は、これと同じプロセスを使用します。

会社を初めてダッシュボードに登録する場合は、「[新しい会社の開設](https://msdn.microsoft.com/windows/hardware/drivers/dashboard/establish-a-new-company)」をご覧ください。

> [!IMPORTANT]
> ハードウェア デベロッパー センター ダッシュ ボードのすべての申請パッケージ用にアップロードおよび使用される証明書について、以下の変更が実施されました。
> * 拡張検証 (EV) コード署名証明書は、**すべて**の申請に必要です。  
> * すべての証明書は SHA2 である必要があり、**/fd sha256** signtool コマンド ライン スイッチを使用して署名される必要があります 
> * (詳しくは、[HLK ブログの投稿](https://blogs.msdn.microsoft.com/windows_hardware_certification/2017/11/13/starting-in-february-2018-packages-signed-using-a-sha-1-digest-algorithm-and-certificate-chain-will-no-longer-be-accepted/)をご覧ください)。

## <a name="to-add-or-update-a-code-signing-certificate"></a>コード署名証明書を追加または更新するには

**手順 1: 必要に応じてコード署名証明書を更新する**  

1. 必要なコード署名証明書の種類を確認します (詳しくは、「[コード署名証明書の取得](https://msdn.microsoft.com/windows/hardware/drivers/dashboard/get-a-code-signing-certificate)」をご覧ください)。

2. 新しい証明書を取得するか、既にある証明書を再利用します。

3. 証明機関から検証済みの証明書を受け取ったら、**手順 2** に進んで "Signablefile.bin" をダウンロードし、署名します 

**手順 2:"Signablefile.bin" ファイルに署名してアップロードする**

1. ハードウェア ダッシュ ボードの証明書をアップロードしたり失効させることができるのは、**管理者**だけです。 

2. **管理者**がサインインしたら、こちらのダイレクト リンクから[ファイルに署名してアップロード](https://partner.microsoft.com/dashboard/account/CertificateUpload)するか、これらの手順に従って手動でページに移動できます。

3. 右上にある歯車アイコンをクリックし、**[開発者向け設定]** をクリックした後、左側のウィンドウで **[証明書の管理]** をクリックします。

4. **[新しい証明書を追加します]** をクリックして、**[次へ]** ボタンをクリックします。  
   
5. Signablefile.bin をダウンロードし、SignTool で **/fd sha256** スイッチと適切な SHA-2 タイムスタンプを使用して、会社の新しいデジタル証明書でファイルに署名します。

6. 署名済みのファイルをハードウェア デベロッパー センター ダッシュ ボードにアップロードします。

## <a name="related-topics"></a>関連トピック

- [サインインする前に](https://msdn.microsoft.com/windows/hardware/drivers/dashboard/before-you-sign-in)

- [新しい会社の開設](https://msdn.microsoft.com/windows/hardware/drivers/dashboard/establish-a-new-company)

- [ハードウェア認定の申請](https://msdn.microsoft.com/windows/hardware/drivers/dashboard/hardware-certification-submissions)

- [認定取得のためのアプリの提出](https://msdn.microsoft.com/windows/hardware/drivers/dashboard/app-certification-submissions)