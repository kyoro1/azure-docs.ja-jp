---
title: 'データセット内の列の選択: コンポーネント リファレンス'
titleSuffix: Azure Machine Learning
description: Azure Machine Learning のデータセット内の列の選択コンポーネントを使用し、ダウンストリーム演算で使用する列のサブセットを選択する方法を学習します。
services: machine-learning
ms.service: machine-learning
ms.subservice: core
ms.topic: reference
author: likebupt
ms.author: keli19
ms.date: 10/22/2019
ms.openlocfilehash: 724a40cbe711e5bb06174533aaf477f7c01d6ac9
ms.sourcegitcommit: e41827d894a4aa12cbff62c51393dfc236297e10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2021
ms.locfileid: "131565787"
---
# <a name="select-columns-in-dataset-component"></a>データセット内の列の選択コンポーネント

この記事では Azure Machine Learning デザイナーのコンポーネントについて説明します。

このコンポーネントを使用し、ダウンストリーム演算で使用する列のサブセットを選択します。 このコンポーネントでは、列がソース データセットから物理的に削除されることはありません。その代わりに、データベースの *ビュー* や *プロジェクション* のように、列のサブセットが作成されます。

このコンポーネントは、ダウンストリーム演算で利用できる列を制限する必要があるときに、あるいは不要な列を削除し、データセットのサイズを減らす場合に役立ちます。

データセット内の列は、元のデータと同じ順序で出力されます。指定した順序が違っても結果は同じになります。

## <a name="how-to-use"></a>使用方法

このコンポーネントにはパラメーターはありません。 列セレクターを使用し、含める列か除外する列を選択します。

### <a name="choose-columns-by-name"></a>名前で列を選択する

このコンポーネントには名前で列を選択する方法が複数存在します。 

+ フィルターと検索

    **[名前別]** オプションをクリックします。

    既に入力済みのデータセットを関連付けている場合、利用できる列が一覧表示されるはずです。 列が表示されないときは、場合によっては、アップストリーム コンポーネントを実行して列を一覧表示する必要があります。

    一覧にフィルターを適用するには、検索ボックスに入力します。 たとえば、検索ボックスに「`w`」という文字を入力すると、一覧にフィルターが適用され、「`w`」という文字を含む列の名前が表示されます。

    列を選択し、右矢印ボタンをクリックし、右側のウィンドウにある一覧に選択した列を移動します。

    + 列名を一定の範囲で連続して選択するには、**Shift キーを押しながら列名をクリックします**。
    + 列を個別に選択するには、**Ctrl キーを押しながら列名をクリックします**。

    チェックマーク ボタンをクリックし、保存して終了します。

+ 他の規則との組み合わせで名前を使用する

    **[WITH RULES]\(規則を使用\)** オプションをクリックします。
    
    特定のデータ型の列を表示するなど、規則を選択します。

    次に、その型の列を名前で個別にクリックし、選択一覧に追加します。

+ 列名のコンマ区切り一覧を入力するか、貼り付ける

    データセットが広範囲にわたる場合、列を個別に選択するより、索引を利用したり、名前の一覧を生成したりするほうが簡単かもしれません。 一覧を前もって準備している場合:

    1. **[WITH RULES]\(規則を使用\)** オプションをクリックします。 
    2. **[No columns]\(列なし\)** を選択し、**[Include]\(含める\)** を選択し、赤の感嘆符が付いているテキスト ボックスの内側をクリックします。 
    3. 前に検証した列名のコンマ区切り一覧を貼り付けるか、入力します。 列の名前が無効な場合、コンポーネントを保存できません。そのため、あらかじめ名前を確認してください。
    
    この方法を利用し、索引値で列の一覧を指定することもできます。 

### <a name="choose-by-type"></a>型別に選択する

**[WITH RULES]\(規則を使用\)** オプションを使用する場合、列の選択に複数の条件を適用できます。 たとえば、数値データ型のフィーチャー列のみを取得したりできます。

**[BEGIN WITH]\(次で始まる\)** オプションでは始点が決定されます。結果を理解するために重要です。 

+ **[すべての列]** オプションを選択した場合、すべての列が一覧に追加されます。 その後、**[除外]** オプションを使用し、特定の条件を満たさない列を *削除* する必要があります。 

    たとえば、最初にすべての列を選択し、それから名前や型に基づいて列を削除します。

+ **[NO COLUMNS]\(列なし\)** オプションを選択した場合、列の一覧は空の状態から始まります。 その後、条件を指定し、列を一覧に *追加* します。 

    複数の規則を適用する場合、各条件は **付加** されます。 たとえば、列なしから始め、数値列をすべて取得する規則を追加します。 自動車の価格のデータセットで、結果的に 16 の列が追加されます。 次に、 **+** 記号をクリックして新しい条件を追加し、 **[Include all features]\(すべてのフィーチャーを含める\)** を選択します。 結果的に得られるデータセットにはすべての数値列が含まれ、さらに文字列のフィーチャー列など、すべてのフィーチャー列が含まれます。

### <a name="choose-by-column-index"></a>列の索引別に選択する

列の索引は、元のデータセットにおける列の順序を指します。

+ 列には 1 から始まる連続番号が付けられます。  
+ ある範囲の列を得るには、ハイフンを使用します。 
+ `1-` や `-3` のように、始まりや終わりを指定しないことは許可されません。
+ 索引値 (または列名) の重複は許可されません。エラーを起こす可能性があります。

たとえば、データセットに少なくとも 8 つの列が含まれる場合、次のいずれかを貼り付けることで、連続しない複数の列を返すことができます。 

+ `8,1-4,6`
+ `1,3-8`
+ `1,3-6,4` 

最後のサンプルはエラーになりませんが、列 `4` というインスタンスが 1 つ返されます。



### <a name="change-order-of-columns"></a>列の順序を変更する

**[Allow duplicates and preserve column order in selection]\(選択で重複を許可し、列の順序を維持する\)** オプションの場合、空の一覧から始まり、ユーザーが名前または索引で指定した列が追加されます。 常に列を "自然な順序" で返す他のオプションとは異なり、このオプションでは、ユーザーが指定またはリストアップした順序で列が出力されます。 

たとえば、Col1、Col2、Col3、Col4 という列が含まれるデータセットでは、次のいずれかを指定することで、列の順序を逆にし、列 2 を除外できます。

+ `Col4, Col3, Col1`
+ `4,3,1`


## <a name="next-steps"></a>次のステップ

Azure Machine Learning で[使用できる一連のコンポーネント](component-reference.md)を参照してください。 