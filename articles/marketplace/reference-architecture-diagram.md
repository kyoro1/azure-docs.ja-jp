---
title: 参照アーキテクチャ図 | Azure Marketplace
description: Microsoft コマーシャル マーケットプレース内のプランの参照アーキテクチャ図を作成する方法。
author: mingshen-ms
ms.author: mingshen
ms.reviewer: stmummer
ms.service: marketplace
ms.subservice: partnercenter-marketplace-publisher
ms.topic: reference
ms.date: 09/22/2021
ms.openlocfilehash: 63c820a7dd4bcbe1322478a46043963edc45dd2b
ms.sourcegitcommit: 48500a6a9002b48ed94c65e9598f049f3d6db60c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2021
ms.locfileid: "129054264"
---
# <a name="reference-architecture-diagram"></a>参照アーキテクチャ図

参照アーキテクチャ図は、お客様のプランが依存するインフラストラクチャを表すモデルです。 Azure IP ソリューションについては、IP 共同販売の技術的な要件に従って、お客様のプランで Microsoft のクラウド サービスがどのように使用されているのかについても、この図で示す必要があります。 これは、アーキテクチャの品質を評価するためのものではありません。 お客様のソリューションで Microsoft サービスをどのように使用しているかを示すためのものです。

参照アーキテクチャ図は複数のツールを使用して作成できます。 Microsoft Visio には Azure のアーキテクチャのモデルを表す複数のステンシルが用意されているため、これをお勧めします。

参照アーキテクチャ図を作成するための有用な出発点は、[Azure のアーキテクチャのモデル](/azure/architecture/browse/)を活用することです。

## <a name="typical-components-of-a-reference-architecture-diagram"></a>参照アーキテクチャ図の代表的なコンポーネント

この図では、Microsoft Azure 上にデプロイされ、その利用を促進するソリューション、アプリケーション、またはサービス コードとして IP を明確に識別する必要があります。 このコードは再利用性が高く、デプロイごとの広範なカスタマイズに依存しないようにする必要があります。

- プランをホスト、操作するクラウド サービス (Azure リソースを使用するものを含む)
- プランで使用されているデータ接続、データ レイヤー、データ サービス
- プランのセキュリティ、認証、およびユーザーを制御するために使用されるクラウド サービス
- ユーザーにプランを公開するユーザー インターフェイスおよびその他のサービス
- ハイブリッドまたはオンプレミスの接続と統合、または両方の組み合わせ

このスクリーンショットは、参照アーキテクチャ図の例を示しています。

[![このイメージは、共同販売アーキテクチャ図の例です。](./media/co-sell/co-sell-arch-diagram.png)](./media/co-sell/co-sell-arch-diagram.png#lightbox)

この参照アーキテクチャ図の例は、垂直業界のチャットボット向けです。これは、イントラネット サイトと統合して、機械学習アルゴリズムによって需要予測シナリオに役立てることができます。 このソリューションでは、さまざまな ERP システムからのサプライ チェーンおよび製造スケジュール データを使用します。 このボットは、販売担当者が注文の配送予定日を確定できるタイミングに関する質問に対応するように設計されています。

## <a name="next-steps"></a>次のステップ

- [コマーシャル マーケットプレース プランの共同販売を構成する](./co-sell-configure.md)
