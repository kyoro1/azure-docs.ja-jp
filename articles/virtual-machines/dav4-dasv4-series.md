---
title: Dav4 および Dasv4 シリーズ
description: Dav4 および Dasv4 シリーズ VM の仕様。
author: mamccrea
ms.author: mamccrea
ms.service: virtual-machines
ms.subservice: vm-sizes-general
ms.topic: conceptual
ms.date: 02/03/2020
ms.reviewer: jushiman
ms.openlocfilehash: c35f0958b8bfd5aa2695e3387710eb4afb895af0
ms.sourcegitcommit: 702df701fff4ec6cc39134aa607d023c766adec3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2021
ms.locfileid: "131463128"
---
# <a name="dav4-and-dasv4-series"></a>Dav4 および Dasv4 シリーズ

**適用対象:** :heavy_check_mark: Linux VM :heavy_check_mark: Windows VM :heavy_check_mark: 柔軟なスケール セット :heavy_check_mark: 均一のスケール セット

Dav4 シリーズと Dasv4 シリーズは、マルチスレッド構成で AMD の 2.35 GHz EPYC<sup>TM</sup> 7452 プロセッサを利用する新しいサイズです。最大 256 MB の L3 キャッシュを備え、8 つのコアのそれぞれにその L3 キャッシュの 8 MB が専用に割り当てられており、汎用ワークロードを実行するためのカスタマー オプションが増えています。 Dav4 シリーズと Dasv4 シリーズは、D および Dsv3 シリーズと同じメモリおよびディスク構成を備えています。

## <a name="dav4-series"></a>Dav4 シリーズ

Dav4 シリーズのサイズは、2.35Ghz AMD EPYC<sup>TM</sup> 7452 プロセッサをベースにしています。このプロセッサでは 3.35 GHz のブースト最大周波数を達成できます。 Dav4 シリーズのサイズでは、ほとんどの運用環境のワークロードに適した vCPU、メモリ、および一時ストレージの組み合わせが提供されます。 データ ディスク ストレージは、仮想マシンとは別に課金されます。 Premium SSD を使用するには、Dasv4 サイズを使用します。 Dasv4 サイズの価格および課金の計算方法は、Dav4 シリーズと同じです。

[ACU](acu.md): 230-260<br>
[Premium Storage](premium-storage-performance.md): サポートされていません<br>
[Premium Storage キャッシュ](premium-storage-performance.md): サポートされていません<br>
[ライブ マイグレーション](maintenance-and-updates.md): サポートされています<br>
[メモリ保持更新](maintenance-and-updates.md): サポートされています<br>
[VM 世代サポート](generation-2.md): 第 1 世代<br>
[高速ネットワーク](../virtual-network/create-vm-accelerated-networking-cli.md):サポートされています<br>
[エフェメラル OS ディスク](ephemeral-os-disks.md):サポートされています <br>
<br>

| サイズ | vCPU | メモリ:GiB | 一時ストレージ (SSD) GiB | 最大データ ディスク数 | 一時ストレージの最大スループット: IOPS/読み取り MBps/書き込み MBps | 最大 NIC 数 | 必要なネットワーク帯域幅 (Mbps) |
|-----|-----|-----|-----|-----|-----|-----|-----|
| Standard_D2a_v4<sup>1</sup> |  2  | 8  | 50  | 4  | 3000/46/23   | 2 | 2000 |
| Standard_D4a_v4 |  4  | 16 | 100 | 8  | 6000/93/46   | 2 | 4000 |
| Standard_D8a_v4 |  8  | 32 | 200 | 16 | 12000/187/93 | 4 | 8000 |
| Standard_D16a_v4|  16 | 64 | 400 |32  | 24000/375/187 |8 | 10000 |
| Standard_D32a_v4|  32 | 128| 800 | 32 | 48000/750/375 |8 | 16000 |
| Standard_D48a_v4| 48 | 192| 1200 | 32 | 96,000/1,000/500 | 8 | 24000 |
| Standard_D64a_v4| 64 | 256 | 1600 | 32 | 96,000/1,000/500 | 8 | 32000 |
| Standard_D96a_v4| 96 | 384 | 2400 | 32 | 96,000/1,000/500 | 8 | 40000 |

<sup>1</sup> 高速ネットワークは、1 つの NIC にのみ適用できます。 

## <a name="dasv4-series"></a>Dasv4 シリーズ

Easv4 シリーズのサイズは、2.35Ghz AMD EPYC<sup>TM</sup> 7452 プロセッサをベースにしています。このプロセッサでは 3.35 GHz のブースト最大周波数を達成し、Premium SSD を使用できます。 Dasv4 シリーズのサイズでは、ほとんどの運用環境のワークロードに適した vCPU、メモリ、および一時ストレージの組み合わせが提供されます。

[ACU](acu.md): 230-260<br>
[Premium Storage](premium-storage-performance.md): サポートされています<br>
[Premium Storage キャッシュ](premium-storage-performance.md): サポートされています<br>
[ライブ マイグレーション](maintenance-and-updates.md): サポートされています<br>
[メモリ保持更新](maintenance-and-updates.md): サポートされています<br>
[VM 世代サポート](generation-2.md): 第 1 世代と第 2 世代<br>
[高速ネットワーク](../virtual-network/create-vm-accelerated-networking-cli.md):サポートされています<br>
[エフェメラル OS ディスク](ephemeral-os-disks.md):サポートされています <br>
<br>

| サイズ | vCPU | メモリ:GiB | 一時ストレージ (SSD) GiB | 最大データ ディスク数 | キャッシュが有効な場合および一時ストレージの最大スループットIOPS/MBps (キャッシュ サイズは GiB 単位) | バースト キャッシュが有効な一時ストレージの最大スループット: IOPS/MBps<sup>1</sup> | キャッシュが無効な場合の最大ディスク スループット: IOPS/MBps | バースト キャッシュが無効なディスクの最大スループット: IOPS/MBps<sup>1</sup> | 最大 NIC 数 | 必要なネットワーク帯域幅 (Mbps) |
|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|----|
| Standard_D2as_v4<sup>2</sup>| 2  | 8   | 16  | 4  | 4000 / 32 (50)       | 4000/100    | 3200 / 48    | 4000/200   | 2 | 2000  |
| Standard_D4as_v4            | 4  | 16  | 32  | 8  | 8000 / 64 (100)      | 8000/200    | 6400 / 96    | 8000/200   | 2 | 4000  |
| Standard_D8as_v4            | 8  | 32  | 64  | 16 | 16000 / 128 (200)    | 16000/400   | 12800 / 192  | 16000/400  | 4 | 8000  |
| Standard_D16as_v4           | 16 | 64  | 128 | 32 | 32000 / 255 (400)    | 32000/800   | 25600 / 384  | 32000/800  | 8 | 10000 |
| Standard_D32as_v4           | 32 | 128 | 256 | 32 | 64000 / 510 (800)    | 64000/1600  | 51200 / 768  | 64000/1600 | 8 | 16000 |
| Standard_D48as_v4           | 48 | 192 | 384 | 32 | 96000 / 1020 (1200)  | 96000/2000  | 76800 / 1148 | 80000/2000 | 8 | 24000 |
| Standard_D64as_v4           | 64 | 256 | 512 | 32 | 128000 / 1020 (1600) | 128000/2000 | 80000 / 1200 | 80000/2000 | 8 | 32000 | 
| Standard_D96as_v4           | 96 | 384 | 768 | 32 | 192000 / 1020 (2400) | 192000/2000 | 80000 / 1200 | 80000/2000 | 8 | 40000 |

<sup>1</sup>  Dasv4 シリーズの VM では、ディスクのパフォーマンスを[バースト](disk-bursting.md)でき、一度に最大 30 分間バーストを最大にしておくことができます。<br>
<sup>2</sup> 高速ネットワークは、1 つの NIC にのみ適用できます。



[!INCLUDE [virtual-machines-common-sizes-table-defs](../../includes/virtual-machines-common-sizes-table-defs.md)]

## <a name="other-sizes-and-information"></a>その他のサイズと情報

- [汎用](sizes-general.md)
- [メモリの最適化](sizes-memory.md)
- [ストレージの最適化](sizes-storage.md)
- [GPU の最適化](sizes-gpu.md)
- [ハイ パフォーマンス コンピューティング](sizes-hpc.md)
- [旧世代](sizes-previous-gen.md)

料金計算ツール: [料金計算ツール](https://azure.microsoft.com/pricing/calculator/)

ディスクの種類の詳細情報: [ディスクの種類](./disks-types.md#ultra-disks)

## <a name="next-steps"></a>次のステップ

[Azure コンピューティング ユニット (ACU)](acu.md) を確認することで、Azure SKU 全体の処理性能を比較できます。
