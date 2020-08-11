---
title: Como usar a resolução IP de rede transparente
description: Saiba mais sobre a resolução de IP de rede transparente no ODBC Driver for SQL Server e como ela afeta o recurso MultiSubnetFailover.
ms.custom: ''
ms.date: 05/06/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d255208f-d486-4ad3-8080-61c6e0261825
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 12a8a151902bd4f191fbc79f165f936e991a0226
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87244995"
---
# <a name="using-transparent-network-ip-resolution-with-the-odbc-driver"></a>Usando a Resolução de IP de Rede Transparente com o driver do ODBC
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

A TransparentNetworkIPResolution é uma revisão do recurso MultiSubnetFailover existente, disponível no Microsoft ODBC Driver 13.1 for SQL Server, que afeta a sequência de conexão do driver no caso em que o primeiro IP resolvido do nome do host não responde e há vários IPs associados ao nome do host. Ele interage com MultiSubnetFailover para fornecer as três seguintes sequências de conexão:

* 0: um IP é tentado, seguido por todos os IPs em paralelo
* 1: todos os IPs são tentados em paralelo
* 2: todos os IPs são tentados um após o outro

|TransparentNetworkIPResolution|MultiSubnetFailover|Comportamento|
|:-:|:-:|:-:|
|(padrão)|(padrão)|0|
|(padrão)|habilitado|1|
|(padrão)|Desabilitado|0|
|habilitado|(padrão)|0|
|habilitado|habilitado|1|
|habilitado|Desabilitado|0|
|Desabilitado|(padrão)|2|
|Desabilitado|habilitado|1|
|Desabilitado|Desabilitado|2|

A cadeia de conexão `TransparentNetworkIPResolution` e a palavra-chave de DSN controlam essa configuração no nível da cadeia de conexão. O padrão é habilitado.

Palavra-chave|Valores|Padrão
-|-|-
`TransparentNetworkIPResolution`|`Yes`, `No`|`Yes`

O atributo de pré-conexão `SQL_COPT_SS_TNIR` permite que um aplicativo controle essa configuração programaticamente:

Atributo de conexão|   Tamanho/tipo|  Padrão| Valor| Descrição
-|-|-|-|-
`SQL_COPT_SS_TNIR` (1249)| `SQL_IS_INTEGER` ou `SQL_IS_UINTEGER`| `SQL_IS_ON`(1), `SQL_IS_OFF`(0)|`SQL_IS_ON`|Habilita ou desabilita o TNIR.

<a name="for-more-information-about-multisubnetfailover-see-odbc-driver-on-linux-and-macos---high-availability-and-disaster-recovery"></a>Para saber mais sobre MultiSubnetFailover, confira [ODBC Driver no Linux e macOS – alta disponibilidade e recuperação de desastre](linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)
--------------------------------------------------
## <a name="see-also"></a>Consulte Também  
* [Microsoft ODBC Driver for SQL Server no Windows](windows/microsoft-odbc-driver-for-sql-server-on-windows.md)
* [Clustering de várias sub-redes do SQL Server (SQL Server)](../../sql-server/failover-clusters/windows/sql-server-multi-subnet-clustering-sql-server.md)
