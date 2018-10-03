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
manager: craigg
ms.openlocfilehash: 767e3e17b67a36bca93bd8a85704d50338fdfd58
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47610734"
---
# <a name="using-transparent-network-ip-resolution"></a>Como usar a resolução IP de rede transparente
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

TransparentNetworkIPResolution é uma revisão de recurso MultiSubnetFailover existente, disponível no Microsoft ODBC Driver 13.1 para SQL Server, o que afeta a sequência de conexão do driver no caso onde o primeiro IP resolvido do nome do host não responder e há vários IPs associados com o nome do host. Ele interage com MultiSubnetFailover para fornecer as sequências de conexão de três a seguir:

* 0: uma tentativa de IP, seguido por todos os IPs em paralelo
* 1: todos os IPs são tentadas em paralelo
* 2: todos os IPs são tentadas após o outro

|transparentNetworkIPResolution|MultiSubnetFailover|Comportamento|
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

O `TransparentNetworkIPResolution` cadeia de caracteres de conexão e o DSN de palavra-chave controla essa configuração no nível de cadeia de caracteres de conexão. O padrão é ativado.

Palavra-chave|Valores|Padrão
-|-|-
`TransparentNetworkIPResolution`|`Yes`, `No`|`Yes`

O `SQL_COPT_SS_TNIR` atributo da conexão permite que um aplicativo controlar essa configuração por meio de programação:

Atributo de conexão|   Tamanho/tipo|  Padrão| Valor| Descrição
-|-|-|-|-
`SQL_COPT_SS_TNIR` (1249)| `SQL_IS_INTEGER` ou `SQL_IS_UINTEGER`| `SQL_IS_ON`(1), `SQL_IS_OFF`(0)|`SQL_IS_ON`|Habilita ou desabilita TNIR.

<a name="for-more-information-about-multisubnetfailover-see-odbc-driver-on-linux-and-macos---high-availability-and-disaster-recoveryconnectodbclinux-macodbc-driver-on-linux-support-for-high-availability-disaster-recoverymd"></a>Para obter mais informações sobre MultiSubnetFailover, consulte [Driver ODBC no Linux e macOS – alta disponibilidade e recuperação de desastres](../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)
--------------------------------------------------
## <a name="see-also"></a>Consulte Também  
* [Microsoft ODBC Driver for SQL Server no Windows](../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)
* [Clustering de várias sub-redes do SQL Server (SQL Server)](https://msdn.microsoft.com/library/ff878716.aspx#RelatedContent)
