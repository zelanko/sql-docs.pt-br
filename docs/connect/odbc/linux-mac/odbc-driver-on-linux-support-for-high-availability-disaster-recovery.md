---
title: Driver ODBC no Linux e no macOS – alta disponibilidade e recuperação de desastre | Microsoft Docs
ms.custom: ''
ms.date: 04/05/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: fa656c5b-a935-40bf-bc20-e517ca5cd0ba
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f53fc932ced3c5a4e002c9938a9af6a2b8d410e1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66798780"
---
# <a name="odbc-driver-on-linux-and-macos-support-for-high-availability-and-disaster-recovery"></a>Driver ODBC no Linux e no macOS – compatibilidade com alta disponibilidade e recuperação de desastre
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Os drivers ODBC para Linux e macOS são compatíveis com [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]. Para saber mais sobre [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)], consulte:  
  
-   [Ouvintes do grupo de disponibilidade, conectividade de cliente e failover de aplicativo (SQL Server)](https://msdn.microsoft.com/library/hh213417.aspx)  
  
-   [Criação e configuração de grupos de disponibilidade (SQL Server)](https://msdn.microsoft.com/library/ff878265.aspx)  
  
-   [Clustering de failover e Grupos de Disponibilidade AlwaysOn (SQL Server)](https://msdn.microsoft.com/library/ff929171.aspx)  
  
-   [Secundárias ativas: réplicas secundárias legíveis (Grupos de Disponibilidade AlwaysOn)](https://msdn.microsoft.com/library/ff878253.aspx)  
  
Você pode especificar o ouvinte de um determinado grupo de disponibilidade na cadeia de conexão. Se um aplicativo do ODBC no Linux ou macOS estiver conectado a um banco de dados em um grupo de disponibilidade que executa failover, a conexão original será interrompida e o aplicativo deverá abrir uma nova conexão para continuar o trabalho após o failover.

Os drivers ODBC no Linux e no macOS iteram sequencialmente em todos os endereços IP associados com um nome de host DNS se você não está se conectando a um ouvinte de grupo de disponibilidade, e vários endereços IP são associados ao nome do host.

Se o primeiro endereço IP retornado do servidor DNS não for conectável, essas iterações poderão ser demoradas. Ao se conectar a um ouvinte do grupo de disponibilidade, o driver tenta estabelecer conexões com todos os endereços IP em paralelo. Se uma tentativa de conexão obtiver êxito, o driver descartará as tentativas de conexão pendentes.

> [!NOTE]  
> Como uma conexão pode falhar devido a um failover de grupo de disponibilidade, implemente a lógica de repetição de conexão; tente novamente uma conexão com falha até se reconectar. Aumentar o tempo limite de conexão e implementar a lógica de repetição de conexão aumentará a probabilidade de se conectar a um grupo de disponibilidade.

## <a name="connecting-with-multisubnetfailover"></a>Conectando-se ao MultiSubnetFailover

Sempre especifique **MultiSubnetFailover=Yes** ao se conectar a um ouvinte do grupo de disponibilidade do [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] ou a uma instância de cluster de failover do [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]. O **MultiSubnetFailover** permite failover mais rápido para todos os grupos de disponibilidade a instância de cluster de failover no [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]. O **MultiSubnetFailover** também reduz significativamente o tempo de failover para topologias AlwaysOn únicas e com várias sub-redes. Durante um failover de várias sub-redes, o cliente tentará conexões em paralelo. Durante um failover de sub-rede, o driver repete agressivamente a conexão TCP.

A propriedade de conexão **MultiSubnetFailover** indica que o aplicativo está sendo implantado em um grupo de disponibilidade ou instância de cluster de failover. O driver tenta se conectar ao banco de dados na instância primária do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] experimentando todos os endereços IP. Ao se conectar com **MultiSubnetFailover=Yes**, o cliente repete as tentativas de conexão TCP mais rápido do que os intervalos de retransmissão TCP padrão do sistema operacional. **MultiSubnetFailover = Yes** permite uma reconexão mais rápida após o failover de um grupo de disponibilidade AlwaysOn ou uma instância de cluster de failover AlwaysOn. **MultiSubnetFailover=Yes** se aplica tanto a grupos de disponibilidade e instâncias de cluster de failover únicos quanto de várias sub-redes.  

Use **MultiSubnetFailover=Yes** ao se conectar a um ouvinte do grupo de disponibilidade ou a uma instância de cluster de failover. Caso contrário, o desempenho de seu aplicativo pode ser afetado negativamente.

Lembre-se do seguinte ao se conectar com um servidor em um grupo de disponibilidade ou Instância de Cluster de Failover:
  
-   Especifique **MultiSubnetFailover=Yes** para melhorar o desempenho ao se conectar a uma sub-rede única ou a um Grupo de Disponibilidade de várias sub-redes.

-   Especifique o ouvinte do grupo de disponibilidade como o servidor em sua cadeia de conexão.
  
-   Não é permitido se conectar a uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] configurada com mais de 64 endereços IP.

-   É possível usar tanto Autenticação [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quanto Autenticação Kerberos com **MultiSubnetFailover=Yes** sem afetar o comportamento do aplicativo.

-   Você pode aumentar o valor de **loginTimeout** para acomodar o tempo de failover e reduzir as tentativas de repetição de conexão do aplicativo.

-   Não há suporte a transações distribuídas.  
  
Se o roteamento somente leitura não estiver em efeito, conectar-se a um local de réplica secundário em um grupo de disponibilidade apresentará falha nas seguintes situações:  
  
1.  Se o local de réplica secundário não for configurado para aceitar conexões.  
  
2.  Se um aplicativo usar **ApplicationIntent=ReadWrite** e o local de réplica secundário estiver configurado para acesso somente leitura.  
  
Uma conexão falhará se uma réplica primária estiver configurada para rejeitar cargas de trabalho somente leitura e a cadeia de conexão contiver **ApplicationIntent=ReadOnly**.  


[!INCLUDE[specify-application-intent_read-only-routing](~/includes/paragraph-content/specify-application-intent-read-only-routing.md)]


## <a name="odbc-syntax"></a>Sintaxe do ODBC

Duas palavras-chave da cadeia de conexão do ODBC são compatíveis com o [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]:  
  
-   **ApplicationIntent**  
  
-   **MultiSubnetFailover**  
  
Para saber mais sobre essas palavras-chave de cadeia de conexão do ODBC, veja [Usando palavras-chave da cadeia de conexão com o SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
Os atributos de conexão equivalentes são:
  
-   **SQL_COPT_SS_APPLICATION_INTENT**  
  
-   **SQL_COPT_SS_MULTISUBNET_FAILOVER**  
  
Para saber mais sobre as propriedades de conexão do ODBC, consulte [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md).  
  
Um aplicativo no driver ODBC que use os [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)] pode usar uma dessas duas funções para fazer a conexão:  
  
|Função|Descrição|  
|------------|---------------|  
|[Função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|O **SQLConnect** é compatível com **ApplicationIntent** e **MultiSubnetFailover** por meio de um DSN (nome de fonte de dados) ou atributo de conexão.|  
|[Função SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|O **SQLDriverConnect** é compatível com **ApplicationIntent** e **MultiSubnetFailover** por meio de palavras-chave de cadeia de conexão, atributo de conexão ou DSN.|
  
## <a name="see-also"></a>Consulte Também  

[Palavras-chave de cadeia de conexão e nomes de fontes de dados (DSNs)](../../../connect/odbc/linux-mac/connection-string-keywords-and-data-source-names-dsns.md)

[Diretrizes de programação](../../../connect/odbc/linux-mac/programming-guidelines.md)

[Notas de versão](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)  
