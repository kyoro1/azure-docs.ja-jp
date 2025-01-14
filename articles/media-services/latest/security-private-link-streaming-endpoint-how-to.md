---
title: ストリーミング エンドポイントのプライベート リンクを作成する
description: この記事では、ストリーミング エンドポイントでプライベート リンクを使用する方法について説明します。 仮想ネットワークとストリーミング エンドポイント間のリンクであるプライベート エンドポイント リソースを作成します。 このデプロイでは、仮想ネットワーク内にネットワーク インターフェイスの IP アドレスが作成されます。 プライベート リンクを使用すると、プライベート ネットワーク内のネットワーク インターフェイスを Media Services アカウントのストリーミング エンドポイントに接続できます。 プライベート IP アドレスを渡す DNS ゾーンを作成することもできます。
services: media-services
author: IngridAtMicrosoft
manager: femila
ms.service: media-services
ms.topic: how-to
ms.date: 10/22/2021
ms.author: inhenkel
ms.openlocfilehash: 3175925fe8d5273ec5f9bb0220b439a01df5ef11
ms.sourcegitcommit: 106f5c9fa5c6d3498dd1cfe63181a7ed4125ae6d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2021
ms.locfileid: "131092276"
---
# <a name="create-a-private-link-for-a-streaming-endpoint"></a>ストリーミング エンドポイントのプライベート リンクを作成する

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

この記事では、ストリーミング エンドポイントでプライベート リンクを使用する方法について説明します。 [Azure リソース グループ](/azure-resource-manager/management/manage-resource-groups-portal)、[Media Services アカウント](account-create-how-to.md)、[Azure 仮想ネットワーク](/virtual-network/quick-create-portal)を作成する方法が既にわかっていることを前提としています。

仮想ネットワークとストリーミング エンドポイント間のリンクであるプライベート エンドポイント リソースを作成します。 このデプロイでは、仮想ネットワーク内にネットワーク インターフェイスの IP アドレスが作成されます。 プライベート リンクを使用すると、プライベート ネットワーク内のネットワーク インターフェイスを Azure Media Services アカウントのストリーミング エンドポイントに接続できます。 プライベート IP アドレスを渡す DNS ゾーンを作成することもできます。

このチュートリアルで作成した仮想ネットワークは、この例を支援するためのものです。  運用環境で使用する既存の仮想ネットワークがあることを前提としています。

> [!NOTE]
> 手順に従ってリソースに似た名前を付けて、同じ目的を持つものとして簡単に理解できるようにします。  たとえば、ストレージ アカウントの場合は *privatelink1stor*、マネージド ID の場合は *privatelink1mi* になります。

## <a name="create-a-resource-group-and-a-media-services-account"></a>リソース グループと Azure Media Services アカウントを作成する

1. Azure リソース グループを作成します。
1. Azure Media Services アカウントを作成します。  既定のストリーミング エンドポイントは、アカウントの作成時に作成されます。 設定プロセス中に、マネージド ID を作成する必要があります。
1. 既定の設定を使用して Azure 仮想ネットワークを作成します。

この時点で、インターネットに接続するストリーミング エンドポイント、キー配信、ライブ イベントを含む、インターネットに接続するエンドポイントがある Azure Media Services アカウントの仮想ネットワークには何もありません。  次の手順では、ストリーミング エンドポイントをプライベートにします。

## <a name="start-the-streaming-endpoint"></a>ストリーミング エンドポイントを開始する

1. 作成した Azure Media Services アカウントに移動します。  
1. メニューから **[ストリーミング エンドポイント]** を選択します。 [ストリーミング エンドポイント] 画面が表示されます。
1. Azure Media Services アカウントを設定するときに作成した既定のストリーミング エンドポイントを選択します。  既定のストリーミング エンドポイント画面が表示されます。
1. **[スタート]** を選択します。 開始オプションが表示されます。
1. CDN 価格レベル ドロップダウン リストから **[なし]** を選択します。
1. **[スタート]** を選択します。  これでストリーミング エンドポイントが開始されます。 エンドポイントはまだインターネットに接続されています。

## <a name="create-a-private-endpoint"></a>プライベート エンドポイントの作成

1. Azure Media Services アカウントに戻ります。
1. メニューから **[ネットワーキング]** を選択します。
1. **[プライベート エンドポイント接続]** タブを選択します。プライベート エンドポイント接続画面が表示されます。
1. **[プライベート エンドポイントの追加]** を選択します。 [プライベート エンドポイントの作成] 画面が表示されます。
1. **[名前]** フィールドで、プライベート エンドポイントに *privatelinkpe* などの名前を付けます。
1. **[地域]** ドロップダウン リストで、 *[米国西部 2]* などのリージョンを選択します。
1. **[Next:リソース]** を選択します。 リソース画面が表示されます。

## <a name="assign-the-private-endpoint-to-a-resource"></a>プライベート エンドポイントをリソースに割り当てる

1. **[接続方法]** ラジオ ボタンで、 *[マイ ディレクトリ内の Azure リソースに接続します]* のラジオ ボタンを選択します。
1. **[リソースの種類]** ドロップダウン リストで、*Microsoft.Media/mediaservices* を選択します。
1. **[リソース]** ドロップダウン リストから、作成した Azure Media Services アカウントを選択します。
1. **[ターゲット サブリソース]** ドロップダウン リストから、作成したストリーミング エンドポイントを選択します。

## <a name="deploy-the-private-endpoint-to-the-virtual-network"></a>プライベート エンドポイントを仮想ネットワークにデプロイする

1. **[仮想ネットワーク]** ドロップダウン リストから、作成した仮想ネットワークを選択します。
1. **[サブネット]** ドロップダウン リストから、操作するサブネットを選択します。
1. この画面を表示したままにします。

## <a name="create-dns-zones-to-use-with-the-private-endpoint"></a>プライベート エンドポイントで使用する DNS ゾーンを作成する

仮想ネットワーク内でストリーミング エンドポイントを使用するには、プライベート DNS ゾーンを作成します。 同じ DNS 名を使用して、ストリーミング エンドポイントのプライベート IP アドレスを取得することができます。

1. 同じ画面の **media-azure-net** 構成で、 **[リソース グループ]** ドロップダウン リストから、作成したリソース グループを選択します。
1. **privatelink-media-azure-net** 構成の場合は、 **[リソース グループ]** ドロップダウン リストから、同じリソース グループを選択します。
1. **タグ** を選択します。 リソースにタグを追加する場合は、ここで作成します。
1. **確認と作成** をクリックします。 [確認と作成] 画面が表示されます。
1. 設定を確認し、正しいことを確認します。
1. **［作成］** を選択します [プライベート エンドポイントのデプロイ] 画面が表示されます。

デプロイの進行中、[Azure Resource Manager (ARM) テンプレート](/azure-resource-manager/templates/overview)も作成されます。 ARM テンプレートを使用して、デプロイを自動化できます。 テンプレートを表示するには、メニューから **[テンプレート]** を選択します。

## <a name="clean-up-resources"></a>リソースをクリーンアップする

この演習で作成したリソースを使用する予定がない場合は、単にリソース グループを削除します。 リソースを削除しない場合は、そのリソースに対して課金されます。