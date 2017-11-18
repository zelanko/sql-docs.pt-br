---
title: "Driver ODBC no Linux e macOS - alta disponibilidade e recuperação de desastres | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fa656c5b-a935-40bf-bc20-e517ca5cd0ba
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d7b6c72d350b718a7676bffd72c261b7cfa72667
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-driver-on-linux-and-macos-support-for-high-availability-and-disaster-recovery"></a>Driver ODBC no Linux e macOS suporte para alta disponibilidade e recuperação de desastres
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Os drivers ODBC para Linux e macOS suporte [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]. Para obter mais informações sobre [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)], consulte:  
  
-   [Ouvintes do grupo de disponibilidade, conectividade de cliente e Failover de aplicativo (SQL Server)](http://msdn.microsoft.com/library/hh213417.aspx)  
  
-   [Criação e configuração de grupos de disponibilidade (SQL Server)](http://msdn.microsoft.com/library/ff878265.aspx)  
  
-   [Clustering de failover e grupos de disponibilidade do AlwaysOn (SQL Server)](http://msdn.microsoft.com/library/ff929171.aspx)  
  
-   [Secundárias ativas: Réplicas secundárias legíveis (grupos de disponibilidade AlwaysOn)](http://msdn.microsoft.com/library/ff878253.aspx)  
  
Você pode especificar o ouvinte de um determinado grupo de disponibilidade na cadeia de conexão. Se um aplicativo ODBC no Linux ou macOS estiver conectado a um banco de dados em um grupo de disponibilidade faz failover, a conexão original será interrompida e o aplicativo deverá abrir uma nova conexão para continuar o trabalho após o failover.

Os drivers ODBC no Linux e macOS sequencialmente iterar por todos os endereços IP associados a um nome de host DNS se você não estiver se conectando a um ouvinte de grupo de disponibilidade e vários endereços IP estão associados com o nome do host.

Se o primeiro endereço IP retornado do servidor DNS não é conectável, essas iterações podem ser demoradas. Ao se conectar a um ouvinte de grupo de disponibilidade, o driver tenta estabelecer conexões com todos os endereços IP em paralelo. Se uma tentativa de conexão obtiver êxito, o driver descartará as tentativas de conexão pendentes.

> [!NOTE]  
> Como uma conexão pode falhar devido a um failover do grupo de disponibilidade, implemente a lógica de repetição de conexão; Repita uma conexão com falha até se reconectar. Aumentar o tempo limite de conexão e implementar a lógica de repetição de conexão aumentará a probabilidade de se conectar a um grupo de disponibilidade.

## <a name="connecting-with-multisubnetfailover"></a>Conectando-se ao MultiSubnetFailover

Sempre especifique **MultiSubnetFailover = Yes** (ou **= True**) ao se conectar a um [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)] ouvinte do grupo de disponibilidade ou [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)] instância de Cluster de Failover. **MultiSubnetFailover** permite failover mais rápido para todos os grupos de disponibilidade e instância de cluster de failover no [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)]. **MultiSubnetFailover** também reduz significativamente o tempo de failover para topologias AlwaysOn únicas e de várias sub-redes. Durante um failover de várias sub-redes, o cliente tentará conexões em paralelo. Durante um failover de sub-rede, o driver agressivamente a conexão TCP.

A propriedade de conexão **MultiSubnetFailover** indica que o aplicativo está sendo implantado em um grupo de disponibilidade ou instância de cluster de failover. O driver tenta se conectar ao banco de dados primário [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] instância tentando se conectar a todos os IPs de endereços. Ao se conectar com **MultiSubnetFailover = Yes**, o cliente repete as tentativas de conexão TCP mais rápido do que os intervalos de retransmissão de TCP do sistema operacional padrão. **MultiSubnetFailover = Yes** permite uma reconexão mais rápida após o failover de um grupo de disponibilidade AlwaysOn ou uma instância de cluster de failover AlwaysOn. **MultiSubnetFailover = Yes** aplica-se ao sub-redes único e vários grupos de disponibilidade e instâncias de Cluster de Failover.  

Use **MultiSubnetFailover=Yes** ao se conectar a um ouvinte do grupo de disponibilidade ou a uma instância de cluster de failover. Caso contrário, o desempenho do aplicativo pode ser afetado negativamente.

Ao se conectar a um servidor em um grupo de disponibilidade ou instância de Cluster de Failover, observe o seguinte:
  
-   Especifique **MultiSubnetFailover = Yes** para melhorar o desempenho ao se conectar a uma única sub-rede ou um grupo de disponibilidade de várias sub-redes.

-   Especifique o ouvinte do grupo de disponibilidade do grupo de disponibilidade como o servidor em sua cadeia de conexão.
  
-   Você não pode se conectar a um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] instância configurada com mais de 64 endereços IP.

-   Ambos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] autenticação ou a autenticação Kerberos pode ser usada com **MultiSubnetFailover = Yes** sem afetar o comportamento do aplicativo.

-   Você pode aumentar o valor de **loginTimeout** para acomodar o tempo de failover e reduzir as tentativas de repetição de conexão do aplicativo.

-   Não há suporte a transações distribuídas.  
  
Se o roteamento somente leitura não estiver em efeito, conectar-se a um local de réplica secundário em um grupo de disponibilidade apresentará falha nas seguintes situações:  
  
1.  Se o local de réplica secundário não for configurado para aceitar conexões.  
  
2.  Se um aplicativo usar **ApplicationIntent=ReadWrite** e o local de réplica secundário estiver configurado para acesso somente leitura.  
  
Uma conexão falhará se uma réplica primária estiver configurada para rejeitar cargas de trabalho somente leitura e a cadeia de conexão contiver **ApplicationIntent=ReadOnly**.  
  
## <a name="specifying-application-intent"></a>Especificando a intenção do aplicativo  
Quando **ApplicationIntent=ReadOnly**, o cliente solicita uma carga de trabalho de leitura ao se conectar a um banco de dados habilitado para AlwaysOn. O servidor imporá a intenção no momento de conexão e durante uma instrução de banco de dados de uso, mas somente para um banco de dados AlwaysOn habilitado.

A palavra-chave **ApplicationIntent** não funciona com bancos de dados herdados somente leitura.  

Um banco de dados pode permitir ou não cargas de trabalho de leitura no banco de dados AlwaysOn de destino. (Use o **ALLOW_CONNECTIONS** cláusula do **PRIMARY_ROLE** e **SECONDARY_ROLE** [!INCLUDE[tsql](../../../includes/tsql_md.md)] instruções.)  
  
A palavra-chave **ApplicationIntent** é usada para habilitar o roteamento somente leitura.  
  
## <a name="read-only-routing"></a>Roteamento somente leitura  
O roteamento somente leitura é um recurso que pode garantir a disponibilidade de uma réplica somente leitura de um banco de dados. Para habilitar roteamento somente leitura:  
  
1.  Conecte-se a um ouvinte de um grupo de disponibilidade AlwaysOn.  
  
2.  A palavra-chave de cadeia de conexão **ApplicationIntent** deve ser definida como **ReadOnly**.  
  
3.  O grupo de disponibilidade deve ser configurado pelo administrador de banco de dados para permitir o roteamento somente leitura.  
  
É possível que várias conexões usem o roteamento somente leitura para se conectarem a diferentes réplicas somente leitura. Alterações na sincronização de banco de dados ou alterações na configuração de roteamento de servidor podem resultar em conexões de cliente com réplicas somente leitura diferentes. Para garantir que todas as solicitações somente leitura conectem-se à mesma réplica somente leitura, não passe um ouvinte de grupo de disponibilidade para a palavra-chave de conexão **Server** . Em vez disso, especifique o nome da instância somente leitura.  
  
Espere tempos de conexão maiores com o roteamento somente leitura do que com a conexão à instância primária. Portanto, aumente o tempo limite de logon. O roteamento somente leitura se conecta primeiro à instância primária e, em seguida, procura a melhor secundária legível disponível.  
  
## <a name="odbc-syntax"></a>Sintaxe do ODBC

Suportam a palavras-chave o cadeia de caracteres de conexão ODBC dois [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]:  
  
-   **ApplicationIntent**  
  
-   **MultiSubnetFailover**  
  
Para obter mais informações sobre essas palavras-chave de conexão do ODBC, consulte [Usando palavras-chave da cadeia de conexão com o SQL Server Native Client](http://msdn.microsoft.com/library/ms130822.aspx).  
  
Os atributos de conexão equivalentes são:
  
-   **SQL_COPT_SS_APPLICATION_INTENT**  
  
-   **SQL_COPT_SS_MULTISUBNET_FAILOVER**  
  
Para obter mais informações sobre atributos de conexão ODBC, consulte [SQLSetConnectAttr](http://msdn.microsoft.com/library/ms131709.aspx).  
  
Um aplicativo ODBC que usa [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)] pode usar uma das duas funções para fazer a conexão:  
  
|Função|Description|  
|------------|---------------|  
|[Função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|**SQLConnect** dá suporte a **ApplicationIntent** e **MultiSubnetFailover** através de um nome de fonte de dados (DSN) ou o atributo de conexão.|  
|[Função SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|**SQLDriverConnect** dá suporte a **ApplicationIntent** e **MultiSubnetFailover** por meio do DSN, a palavra-chave de cadeia de caracteres de conexão ou o atributo de conexão.|
  
## <a name="see-also"></a>Consulte também  

[Palavras-chave de cadeia de conexão e nomes de fontes de dados (DSNs)](../../../connect/odbc/linux-mac/connection-string-keywords-and-data-source-names-dsns.md)

[Diretrizes de programação](../../../connect/odbc/linux-mac/programming-guidelines.md)

[Notas de versão](../../../connect/odbc/linux-mac/release-notes.md)  

