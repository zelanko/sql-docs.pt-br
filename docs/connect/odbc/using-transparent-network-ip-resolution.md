---
title: "Usando a resolução IP de rede transparente | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d255208f-d486-4ad3-8080-61c6e0261825
caps.latest.revision: 2
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cc3b7595b836544f3f7bcfd94f2bab83fac24b36
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="using-transparent-network-ip-resolution"></a>Usando a resolução IP de rede transparente
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

TransparentNetworkIPResolution é uma versão do recurso MultiSubnetFailover existente, disponível no Microsoft ODBC Driver 13.1 para SQL Server, o que afeta a sequência de conexão do driver no caso em que o primeiro IP resolvido do nome do host não responder e há vários IPs associados com o nome do host. Ele interage com MultiSubnetFailover para fornecer sequências de conexão de três a seguir:

* 0: uma tentativa de IP, seguido por todos os IPs em paralelo
* 1: tentativa de todos os IPs em paralelo
* 2: tentativa de todos os IPs após o outro

|TransparentNetworkIPResolution|MultiSubnetFailover|Comportamento|
|:-:|:-:|:-:|
|(padrão)|(padrão)|0|
|(padrão)|Ativado|1|
|(padrão)|Desabilitado|0|
|Ativado|(padrão)|0|
|Ativado|Ativado|1|
|Ativado|Desabilitado|0|
|Desabilitado|(padrão)|2|
|Desabilitado|Ativado|1|
|Desabilitado|Desabilitado|2|

O `TransparentNetworkIPResolution` cadeia de caracteres de conexão e DSN palavra-chave controla essa configuração no nível de cadeia de caracteres de conexão. O padrão é ativado.

Palavra-chave|Valores|Default
-|-|-
`TransparentNetworkIPResolution`|`Yes`, `No`|`Yes`

O `SQL_COPT_SS_TNIR` atributo da conexão permite que um aplicativo controlar essa configuração por meio de programação:

Atributo de Conexão|   Tipo de tamanho /|  Default| Valor| Description
-|-|-|-|-
`SQL_COPT_SS_TNIR` (1249)| `SQL_IS_INTEGER`ou`SQL_IS_UINTEGER`| `SQL_IS_ON`(1), `SQL_IS_OFF`(0)|`SQL_IS_ON`|Habilita ou desabilita TNIR.

<a name="for-more-information-about-multisubnetfailover-see-odbc-driver-on-linux-and-macos---high-availability-and-disaster-recoveryconnectodbclinux-macodbc-driver-on-linux-support-for-high-availability-disaster-recoverymd"></a>Para obter mais informações sobre MultiSubnetFailover, consulte [Driver ODBC no Linux e macOS - alta disponibilidade e recuperação de desastres](../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)
--------------------------------------------------
## <a name="see-also"></a>Consulte também  
* [Microsoft ODBC Driver for SQL Server no Windows](../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)
* [SQL Server Clustering de várias sub-redes (SQL Server)](https://msdn.microsoft.com/library/ff878716.aspx#RelatedContent)

