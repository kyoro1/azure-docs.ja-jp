---
title: マイクロ エージェントのセキュリティ アラート (プレビュー)
description: Defender for IoT デバイスの機能とサービスを使用したセキュリティ アラートと推奨される修復について説明します。
ms.topic: conceptual
ms.date: 11/09/2021
ms.openlocfilehash: 2a5a33b2ad7fd32fafc9a3c7998a21769426f858
ms.sourcegitcommit: 677e8acc9a2e8b842e4aef4472599f9264e989e7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/11/2021
ms.locfileid: "132286623"
---
# <a name="micro-agent-security-alerts-preview"></a>マイクロ エージェントのセキュリティ アラート (プレビュー)

Defender for IoT では、高度な分析と脅威インテリジェンスを使用して IoT ソリューションを継続的に分析し、悪意のあるアクティビティに関するアラートを受け取ることができます。
さらに、期待されるデバイスの動作の知識に基づいて、カスタム アラートを作成できます。
アラートは侵害のリスクのインジケーターとして機能し、調査して修復する必要があります。

この記事では、IoT デバイスでトリガーできる組み込みアラートの一覧を示します。
組み込みアラートのほかに、Defender for IoT を使用すると、IoT Hub やデバイスの予想される動作に基づいてカスタム アラートを定義することもできます。

詳細については、<bpt id="p1">[</bpt>カスタマイズ可能なアラート<ept id="p1">](concept-customizable-security-alerts.md)</ept>に関する記事を参照してください。

## <a name="security-alerts"></a>セキュリティのアラート

### <a name="high-severity"></a>重要度レベル<bpt id="p1">**</bpt>高<ept id="p1">**</ept>

| 名前 | 重大度 | Data Source | 説明 | 推奨される修復手順 | アラートの種類 |
|--|--|--|--|--|--|
| バイナリ コマンド ライン | 高 | Defender for IoT マイクロ エージェント | コマンド ラインからの LA Linux バイナリの呼び出しまたは実行が検出されました。 このプロセスは正当なアクティビティである場合もあれば、デバイスのセキュリティが侵害されたことを示している可能性もあります。 | コマンドについて、それを実行したユーザーに確認し、そのデバイス上での実行が見込まれる正当な行為であるかどうかを確認します。 そうではない場合、情報セキュリティ チームにアラートをエスカレートしてください。 | IoT_BinaryCommandLine |
| ファイアウォールの無効化 | 高 | Defender for IoT マイクロ エージェント | ホスト上のファイアウォールに対して操作が実行されている可能性が検出されました。 データの抜き取りを試みる悪意のあるアクターによって、ホスト上のファイアウォールが無効にされることは少なくありません。 | コマンドを実行したユーザーに、それがデバイス上で見込まれる正当なアクティビティであったかどうかを確認してください。 そうではない場合、情報セキュリティ チームにアラートをエスカレートしてください。 | IoT_DisableFirewall |
| ポート フォワーディングの検出 | 高 | Defender for IoT マイクロ エージェント | 外部 IP アドレスへのポート フォワーディングの開始が検出されました。 | コマンドを実行したユーザーに、それがデバイス上で見込まれる正当なアクティビティであったかどうかを確認してください。 そうではない場合、情報セキュリティ チームにアラートをエスカレートしてください。 | IoT_PortForwarding |
| Auditd ログ記録を無効にする試みが行われている可能性があることが検出されました | 高 | Defender for IoT マイクロ エージェント | Linux Auditd システムは、システムに関するセキュリティ関連情報を追跡する手段を提供しています。 このシステムは、自分のシステムで発生しているイベントについて、可能な限り多くの情報を記録します。 この情報は、ミッション クリティカルな環境でセキュリティ ポリシーの違反者を特定し、違反者が実行するアクションを把握するうえで非常に重要です。 Auditd ログ記録を無効にすると、システムで使用されているセキュリティ ポリシーの違反を検出できなくなる可能性があります。 | それがビジネス上の理由から正当なアクティビティであったかどうかをデバイスの所有者に確認してください。 そうではなかった場合、このイベントは、悪意のあるアクターによる隠蔽のアクティビティである可能性があります。 情報セキュリティ チームに直ちにインシデントをエスカレートしてください。 | IoT_DisableAuditdLogging |
| リバース シェル | 高 | Defender for IoT マイクロ エージェント | デバイス上のホスト データの分析で、リバース シェルの可能性が検出されました。 リバース シェルは、セキュリティが侵害されたマシンに、悪意のあるアクターが制御するマシンをコール バックさせる目的で使用されることが少なくありません。 | コマンドを実行したユーザーに、それがデバイス上で見込まれる正当なアクティビティであったかどうかを確認してください。 そうではない場合、情報セキュリティ チームにアラートをエスカレートしてください。 | IoT_ReverseShell |
| ローカル ログインの成功 | 高 | Defender for IoT マイクロ エージェント | デバイスへのローカル サインインが成功したことが検出されました | サインイン ユーザーが承認済みのパーティーであることを確認してください。 | IoT_SucessfulLocalLogin |
| Web シェル | 高 | Defender for IoT マイクロ エージェント | Web シェルが使用されている可能性があることが検出されました。 一般に、悪意のあるアクターは、セキュリティを侵害したマシンに Web シェルをアップロードして、持続性を獲得したり、さらに悪用したりします。 | コマンドを実行したユーザーに、それがデバイス上で見込まれる正当なアクティビティであったかどうかを確認してください。 そうではない場合、情報セキュリティ チームにアラートをエスカレートしてください。 | IoT_WebShell |
| ランサムウェア検出に似た動作が検出されました | 高 | Defender for IoT マイクロ エージェント | ユーザーが自分のシステムや個人用ファイルにアクセスできないようにしたり、再びアクセスできるようにする代わりに身代金の支払いを要求したりする可能性のある既知のランサムウェアに似たファイルが実行されました。 | コマンドを実行したユーザーに、それがデバイス上で見込まれる正当なアクティビティであったかどうかを確認してください。 そうではない場合、情報セキュリティ チームにアラートをエスカレートしてください。 | IoT_Ransomware |
| 暗号コイン マイナーのイメージ | 高 | Defender for IoT マイクロ エージェント | 通常はデジタル通貨マイニングに関連するプロセスの実行が検出されました。 | コマンドを実行したユーザーに、それがデバイス上の正当なアクティビティであったかどうかを確認してください。 そうではない場合、情報セキュリティ チームにアラートをエスカレートしてください。 | IoT_CryptoMiner |

### <a name="medium-severity"></a>重要度レベル<bpt id="p1">**</bpt>中<ept id="p1">**</ept>

| 名前 | 重大度 | Data Source | 説明 | 推奨される修復手順 | アラートの種類 |
|--|--|--|--|--|--|
| 一般的な Linux ボットに似た動作が検出されました | Medium | Defender for IoT マイクロ エージェント | 一般的な Linux ボットネットに関連付けられたプロセスの実行が検出されました。 | コマンドを実行したユーザーに、それがデバイス上で見込まれる正当なアクティビティであったかどうかを確認してください。 そうではない場合、情報セキュリティ チームにアラートをエスカレートしてください。 | IoT_CommonBots |
| Fairware ランサムウェアに似た動作が検出されました | Medium | Defender for IoT マイクロ エージェント | 不審な場所に適用された rm -rf コマンドの実行が、ホスト データの分析を使用して検出されました。 rm rf は再帰的にファイルを削除するものであるため、通常は個別のフォルダーでしか使用されません。 このケースでは、大量のデータが削除される可能性のある場所で使用されています。 Fairware ランサムウェアは、このフォルダーで rm -rf コマンドを実行することが知られています。 | コマンドを実行したユーザーに、それがデバイス上で見込まれる正当なアクティビティであったことを確認してください。 そうではない場合、情報セキュリティ チームにアラートをエスカレートしてください。 | IoT_FairwareMalware |
| 暗号コイン マイナーのコンテナー イメージが検出されました | Medium | Defender for IoT マイクロ エージェント | 既知のデジタル通貨マイニング イメージを実行するコンテナーが検出されました。 | 1.意図した動作ではない場合、関連するコンテナー イメージを削除してください。 <br> 2.安全でない TCP ソケット経由では Docker デーモンにアクセスできないことを確認してください。 <br> 3.情報セキュリティ チームにアラートをエスカレートしてください。 | IoT_CryptoMinerContainer |
| nohup コマンドの疑わしい使用が検出されました | Medium | Defender for IoT マイクロ エージェント | ホスト上で nohup コマンドの不審な使用が検出されました。 一般に、悪意のあるアクターは、一時ディレクトリから nohup コマンドを実行して、その実行可能ファイルをバックグラウンドで効果的に実行できるようにします。 一時ディレクトリにあるファイルに対してこのコマンドが実行されることはあり得ないか、通常の動作ではありません。 | コマンドを実行したユーザーに、それがデバイス上で見込まれる正当なアクティビティであったかどうかを確認してください。 そうではない場合、情報セキュリティ チームにアラートをエスカレートしてください。 | IoT_SuspiciousNohup |
| useradd コマンドの疑わしい使用が検出されました | Medium | Defender for IoT マイクロ エージェント | useradd コマンドの不審な使用がデバイスで検出されました。 | コマンドを実行したユーザーに、それがデバイス上で見込まれる正当なアクティビティであったかどうかを確認してください。 そうではない場合、情報セキュリティ チームにアラートをエスカレートしてください。 | IoT_SuspiciousUseradd |
| TCP ソケットによる公開 Docker デーモン | Medium | Defender for IoT マイクロ エージェント | マシンのログは、Docker デーモン (dockerd) が TCP ソケットを公開していることを示します。 既定では、Docker の構成は、TCP ソケットが有効である場合には暗号化または認証は使用しません。 既定の Docker 構成では、該当するポートへのアクセス権さえ持っていればだれでも、Docker デーモンへのフル アクセスが可能です。 | コマンドを実行したユーザーに、それがデバイス上で見込まれる正当なアクティビティであったかどうかを確認してください。 そうではない場合、情報セキュリティ チームにアラートをエスカレートしてください。 | IoT_ExposedDocker |
| ローカル ログインに失敗しました | Medium | Defender for IoT マイクロ エージェント | デバイスへのローカル ログインの試行の失敗が検出されました。 | デバイスへの物理的なアクセス権がない第三者がいないことを確認してください。 | IoT_FailedLocalLogin |
| 悪意のあるソースからファイルのダウンロードが検出されました | Medium | Defender for IoT マイクロ エージェント | 既知のマルウェア ソースからのファイルのダウンロードが検出されました。 | コマンドを実行したユーザーに、それがデバイス上で見込まれる正当なアクティビティであったかどうかを確認してください。 そうではない場合、情報セキュリティ チームにアラートをエスカレートしてください。 | IoT_PossibleMalware |
| htaccess ファイルへのアクセスが検出されました | Medium | Defender for IoT マイクロ エージェント | ホスト データの分析で、htaccess ファイルが操作された可能性が検出されました。 htaccess は、基本的なリダイレクト機能や、基本パスワード保護をはじめとするさらに高度な機能など、Apache Web ソフトウェアを実行する Web サーバーに複数の変更を加えることができる強力な構成ファイルです。 悪意のあるアクターは持続性を獲得するために、セキュリティを侵害したマシン上の htaccess ファイルに変更を加えることがよくあります。 | それがホスト上で見込まれる正当なアクティビティであることを確認してください。 そうではない場合、情報セキュリティ チームにアラートをエスカレートしてください。 | IoT_AccessingHtaccessFile |
| 既知の攻撃ツール | Medium | Defender for IoT マイクロ エージェント | なんらかの方法で他のマシンを攻撃する悪意のあるユーザーに関連していることの多いツールが検出されました。 | コマンドを実行したユーザーに、それがデバイス上で見込まれる正当なアクティビティであったかどうかを確認してください。 そうではない場合、情報セキュリティ チームにアラートをエスカレートしてください。 | IoT_KnownAttackTools |
| ローカル ホスト偵察が検出されました | Medium | Defender for IoT マイクロ エージェント | 通常は一般的な Linux ボット偵察に関連するコマンドの実行が検出されました。 | 不審なコマンド ラインを調査して、正当なユーザーによって実行されたものであることを確認してください。 そうではない場合、情報セキュリティ チームにアラートをエスカレートしてください。 | IoT_LinuxReconnaissance |
| スクリプト インタープリターとファイル名拡張子が一致しません | Medium | Defender for IoT マイクロ エージェント | スクリプト インタープリターと、入力として与えられたスクリプト ファイルの拡張子の間で不一致が検出されました。 一般に、このタイプの不一致は、攻撃者によるスクリプトの実行と関係があります。 | コマンドを実行したユーザーに、それがデバイス上で見込まれる正当なアクティビティであったかどうかを確認してください。 そうではない場合、情報セキュリティ チームにアラートをエスカレートしてください。 | IoT_ScriptInterpreterMismatch |
| バックドアの可能性が検出されました | Medium | Defender for IoT マイクロ エージェント | ご利用のサブスクリプション内のホストに不審なファイルがダウンロードされて実行されました。 これは一般に、バックドアのインストールに関連したタイプのアクティビティです。 | コマンドを実行したユーザーに、それがデバイス上で見込まれる正当なアクティビティであったかどうかを確認してください。 そうではない場合、情報セキュリティ チームにアラートをエスカレートしてください。 | IoT_LinuxBackdoor |
| Possible loss of data detected (データが損失した可能性があることが検出されました) | Medium | Defender for IoT マイクロ エージェント | データ エグレス条件の疑いが、ホスト データの分析を使用して検出されました。 悪意のあるアクターは、セキュリティを侵害したマシンからデータを取り出すことがよくあります。 | コマンドを実行したユーザーに、それがデバイス上で見込まれる正当なアクティビティであったかどうかを確認してください。 そうではない場合、情報セキュリティ チームにアラートをエスカレートしてください。 | IoT_EgressData |
| 特権コンテナーが検出されました | Medium | Defender for IoT マイクロ エージェント | マシンのログは、アクセス許可された Docker コンテナーが実行していることを示しています。 特権コンテナーには、ホストのリソースへのフル アクセス権があります。 セキュリティが侵害された場合、悪意のあるアクターは特権コンテナーを使用して、ホスト マシンにアクセスすることができます。 | コンテナーを特権モードで実行する必要がない場合は、コンテナーから特権を削除してください。 | IoT_PrivilegedContainer |
| システム ログ ファイルの削除が検出されました | Medium | Defender for IoT マイクロ エージェント | ホスト上のログ ファイルの不審な削除が検出されました。 | コマンドを実行したユーザーに、それがデバイス上で見込まれる正当なアクティビティであったかどうかを確認してください。 そうではない場合、情報セキュリティ チームにアラートをエスカレートしてください。 | IoT_RemovelOfSystemLogs |
| ファイル名の後のスペース | Medium | Defender for IoT マイクロ エージェント | 不審な拡張子を持ったプロセスの実行が、ホスト データの分析を使用して検出されました。 不審な拡張子は、ファイルを開いても安全であるとユーザーを欺くことがあります。また、システム上にマルウェアが存在することを示す場合があります。 | コマンドを実行したユーザーに、それがデバイス上で見込まれる正当なアクティビティであったかどうかを確認してください。 そうではない場合、情報セキュリティ チームにアラートをエスカレートしてください。 | IoT_ExecuteFileWithTrailingSpace |
| 悪意のある資格情報へのアクセスによく使用されるツールが検出されました | Medium | Defender for IoT マイクロ エージェント | 悪意を持って資格情報にアクセスしようとする行為に一般に関連するツールの使用が検出されました。 | コマンドを実行したユーザーに、それがデバイス上で見込まれる正当なアクティビティであったかどうかを確認してください。 そうではない場合、情報セキュリティ チームにアラートをエスカレートしてください。 | IoT_CredentialAccessTools |
| 不審なコンパイルが検出されました | Medium | Defender for IoT マイクロ エージェント | 不審なコンパイルが検出されました。 悪意のあるアクターは、権限を昇格させるために、セキュリティを侵害したマシンでエクスプロイトをコンパイルすることがよくあります。 | コマンドを実行したユーザーに、それがデバイス上で見込まれる正当なアクティビティであったかどうかを確認してください。 そうではない場合、情報セキュリティ チームにアラートをエスカレートしてください。 | IoT_SuspiciousCompilation |
| 不審なファイルのダウンロードと、それに続くファイルの実行アクティビティ | Medium | Defender for IoT マイクロ エージェント | ホスト データの分析で、同じコマンドでダウンロードされて実行されたファイルが検出されました。 これは、悪意のあるアクターが犠牲者のマシンに感染ファイルを送り込む際に用いる一般的な手法です。 | コマンドを実行したユーザーに、それがデバイス上で見込まれる正当なアクティビティであったかどうかを確認してください。 そうではない場合、情報セキュリティ チームにアラートをエスカレートしてください。 | IoT_DownloadFileThenRun |
| 疑わしい IP アドレスの通信 | Medium | Defender for IoT マイクロ エージェント | 不審な IP アドレスとの通信が検出されました。 | 接続が正当なものであるかどうかを確認してください。 不審な IP との通信はブロックすることを検討してください。 | IoT_TiConnection |

### <a name="low-severity"></a>重大度: 低

| 名前 | 重大度 | Data Source | 説明 | 推奨される修復手順 | アラートの種類 |
|--|--|--|--|--|--|
| Bash 履歴がクリアされました | 低 | Defender for IoT マイクロ エージェント | Bash 履歴ログがクリアされました。 一般に、悪意のあるアクターは、自身のコマンドがログに残らないよう Bash 履歴を消去します。 | コマンドを実行したユーザーにこのアラートのアクティビティを確認し、正当な管理アクティビティと見てよいかどうかを確認します。 そうではない場合、情報セキュリティ チームにアラートをエスカレートしてください。 | IoT_ClearHistoryFile |

## <a name="next-steps"></a>次のステップ

- Defender for IoT サービスの<bpt id="p1">[</bpt>概要<ept id="p1">](overview.md)</ept>
