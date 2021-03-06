---
title: IPv6 のルーティング
ms.date: 03/30/2017
ms.assetid: c98731b4-b542-46a2-9947-1cea63c186b2
author: mcleblanc
ms.author: markl
manager: markl
ms.openlocfilehash: c3e2662eb444c70d2376a05e44ac84f472f27384
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
ms.locfileid: "33397807"
---
# <a name="ipv6-routing"></a>IPv6 のルーティング
柔軟なルーティング メカニズムは、IPv6 の利点です。 IPv4 ネットワーク ID が割り当てられた方法のために、インターネット バックボーン上にあるルーターは大規模なルーティング テーブルを保持する必要があります。 これらのルーターは、インターネット上の任意のノードに送られる可能性のあるパケットを転送するために、すべてのルートを知る必要があります。 アドレスを集計する機能により、IPv6 では、柔軟なアドレス指定が可能であり、ルーティング テーブルのサイズを大幅に縮小することができます。 この新しいアドレス指定アーキテクチャでは、中間のルーターは、ネットワークのローカル部分だけを追跡すれば、メッセージを適切に転送できます。  
  
## <a name="neighbor-discovery"></a>近隣探索  
 近隣探索によって次の機能が提供されます。  
  
-   ルーター探索。 これにより、ホストがローカル ルーターを識別できます。  
  
-   アドレス解決。 これにより、ノードが対応する次ホップ アドレスのリンク層アドレス (アドレス解決プロトコル (ARP) の代替) を解決することができます。  
  
-   アドレスの自動構成。 これにより、ホストが、サイト ローカル アドレスおよびグローバル アドレスを自動的に構成することができます。  
  
 近隣探索では、次のものを含む IPv6 のインターネット制御メッセージ プロトコル (ICMPv6) メッセージを使用します。  
  
-   ルーター アドバタイズ。 擬似定期的にまたはルーター要請に応じてルーターによって送信されます。 IPv6 ルーターは、ルーター アドバタイズを使用して、その可用性、アドレス プレフィックス、およびその他のパラメーターをアドバタイズします。  
  
-   ルーター要請。 ホストによって送信され、リンク上のルーターがルーター アドバタイズをすぐに送信することを要求します。  
  
-   近隣要請。 アドレス解決、重複アドレスの検出、または近隣ノードが到達可能であることを確認するためにノードによって送信されます。  
  
-   近隣アドバタイズ。 近隣要請に応答するかまたはリンク層アドレスの変更を近隣ノードに通知するために、ノードによって送信されます。  
  
-   リダイレクト。 送信元ノード向けに特定の宛先へのより良い次ホップ アドレスを示すために、ルーターによって送信されます。  
  
## <a name="see-also"></a>参照  
 [インターネット プロトコル バージョン 6](../../../docs/framework/network-programming/internet-protocol-version-6.md)  
 [ソケット](../../../docs/framework/network-programming/sockets.md)
