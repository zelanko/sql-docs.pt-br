---
title: Usando a resolução de IP de rede transparente | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d255208f-d486-4ad3-8080-61c6e0261825
author: MightyPen
ms.author: genemi
ms.openlocfilehash: df5b0233168c52b4f79cdc6d2d03cd7b72e16046
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008479"
---
# <a name="using-transparent-network-ip-resolution"></a>Como usar a resolução IP de rede transparente
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

TransparentNetworkIPResolution é uma revisão do recurso MultiSubnetFailover existente, disponível no Microsoft ODBC Driver 13,1 para SQL Server, que afeta a sequência de conexão do driver no caso em que o primeiro IP resolvido do nome do host não Responda e há vários IPs associados ao nome do host. Ele interage com MultiSubnetFailover para fornecer as três seguintes sequências de conexão:

* 0: um IP é tentado, seguido por todos os IPs em paralelo
* 1: todos os IPs são tentados em paralelo
* 2: todos os IPs são tentados um após o outro

|TransparentNetworkIPResolution|MultiSubnetFailover|Comportamento|
|:-:|:-:|:-:|
|(padrão)|(padrão)|0|
|(padrão)|Habilitado|1|
|(padrão)|Desabilitado|0|
|Habilitado|(padrão)|0|
|Habilitado|Habilitado|1|
|Habilitado|Desabilitado|0|
|Desabilitado|(padrão)|2|
|Desabilitado|Habilitado|1|
|Desabilitado|Desabilitado|2|

A `TransparentNetworkIPResolution` cadeia de caracteres de conexão e a palavra-chave DSN controlam essa configuração no nível da cadeia de conexão. O padrão é habilitado.

Palavra-chave|Valores|Padrão
-|-|-
`TransparentNetworkIPResolution`|`Yes`, `No`|`Yes`

O `SQL_COPT_SS_TNIR` atributo pre-Connection permite que um aplicativo controle essa configuração programaticamente:

Atributo de conexão|   Tamanho/tipo|  Padrão| Valor| Descrição
-|-|-|-|-
`SQL_COPT_SS_TNIR` (1249)| `SQL_IS_INTEGER` ou `SQL_IS_UINTEGER`| `SQL_IS_ON`(1), `SQL_IS_OFF`(0)|`SQL_IS_ON`|Habilita ou desabilita TNIR.

<a name="for-more-information-about-multisubnetfailover-see-odbc-driver-on-linux-and-macos---high-availability-and-disaster-recoveryconnectodbclinux-macodbc-driver-on-linux-support-for-high-availability-disaster-recoverymd"></a>Para obter mais informações sobre o MultiSubnetFailover, consulte [driver ODBC no Linux e MacOS – alta disponibilidade e recuperação de desastre](../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)
--------------------------------------------------
## <a name="see-also"></a>Consulte Também  
* [Microsoft ODBC Driver for SQL Server no Windows](../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)
* [Clustering de várias sub-redes do SQL Server (SQL Server)](https://msdn.microsoft.com/library/ff878716.aspx#RelatedContent)
