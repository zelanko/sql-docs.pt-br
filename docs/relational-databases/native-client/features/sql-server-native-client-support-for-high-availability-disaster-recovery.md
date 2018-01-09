---
title: "Suporte para alta disponibilidade, recuperação de desastres do SQL Server Native Client | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|features
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 2b06186b-4090-4728-b96b-90d6ebd9f66f
caps.latest.revision: "35"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 1940375cc3d822d994c673d965e1fb7e23385596
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="sql-server-native-client-support-for-high-availability-disaster-recovery"></a>Suporte do SQL Server Native Client à alta disponibilidade e recuperação de desastre
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Este tópico discute o suporte do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (adicionado no [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]) para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Para obter mais informações sobre [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [Ouvintes do Grupo de Disponibilidade, Conectividade do Cliente e Failover do Aplicativo &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md), [Criação e Configuração de Grupos de Disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md), [Clustering de Failover e Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md) e [Secundárias Ativas: Réplicas Secundárias Legíveis&#40;Grupos de Disponibilidade AlwaysOn&#41;](~/database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md).  
  
 Você pode especificar o ouvinte de um determinado grupo de disponibilidade na cadeia de conexão. Se um aplicativo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client estiver conectado a um banco de dados em um grupo de disponibilidade que executa failover, a conexão original será interrompida e o aplicativo deverá abrir uma nova conexão para continuar o trabalho após o failover.  
  
 Se você não estiver se conectando a um ouvinte de grupo de disponibilidade, e se vários endereços IP forem associados com um nome de host, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client irá iterar em sequência por todos os endereços IP associados à entrada DNS. Isso pode demorar muito se o primeiro endereço IP retornado pelo servidor DNS não estiver associado a nenhuma NIC (placa de interface de rede). Ao se conectar a um ouvinte de grupo de disponibilidade, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client tenta estabelecer conexões com todos os endereços IP em paralelo e, se uma tentativa de conexão for bem-sucedida, o driver descartará as tentativas de conexão pendentes.  
  
> [!NOTE]  
>  O aumento do tempo limite de conexão e a implementação de lógica de repetição de conexão aumentarão a probabilidade de um aplicativo se conectar a um grupo de disponibilidade. Além disso, como uma conexão pode falhar devido a um failover de grupo de disponibilidade, você deve implementar lógica de repetição de conexão, repetindo uma conexão com falha até se reconectar.  
  
## <a name="connecting-with-multisubnetfailover"></a>Conectando-se ao MultiSubnetFailover  
 Sempre especifique **MultiSubnetFailover=Yes** quando for se conectar a um ouvinte de grupo de disponibilidade do SQL Server 2012 ou uma instância de cluster de failover do SQL Server 2012. **MultiSubnetFailover** permite failover mais rápido para todos os grupos de disponibilidade e o cluster de failover da instância do SQL Server 2012 e reduzirá significativamente o tempo de failover de único e de várias sub-redes topologias AlwaysOn. Durante um failover de várias sub-redes, o cliente tentará conexões em paralelo. Durante um failover de sub-rede, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client tentará novamente a conexão TCP de forma agressiva.  
  
 A propriedade de conexão **MultiSubnetFailover** indica que o aplicativo está sendo implantado em um grupo de disponibilidade ou instância de cluster de failover e que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client tentará se conectar ao banco de dados na instância primária do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tentando se conectar a todos os endereços IP do grupo de disponibilidade. Quando **MultiSubnetFailover=Yes** é especificado para uma conexão, o cliente repete as tentativas de conexão TCP mais rápido do que os intervalos de retransmissão TCP padrão do sistema operacional. Isso permite uma reconexão mais rápida após o failover de um grupo de disponibilidade AlwaysOn ou um sempre na instância de Cluster Failover e é aplicável a sub-redes único e vários grupos de disponibilidade e instâncias de Cluster de Failover.  
  
 Para obter mais informações sobre palavras-chave de cadeia de conexão, consulte [Usando palavras-chave da cadeia de conexão com o SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 A especificação de **MultiSubnetFailover=Yes** durante a conexão a algo que não seja um ouvinte de grupo de disponibilidade ou uma Instância de Cluster de Failover pode resultar em um impacto de desempenho negativo e não há suporte para isso.  
  
 Use as diretrizes a seguir para conectar-se a um servidor em um grupo de disponibilidade ou Instância de Cluster de Failover:  
  
-   Use a propriedade de conexão **MultiSubnetFailover** quando estiver se conectando a uma ou várias sub-redes; isso melhorará o desempenho em ambos os casos.  
  
-   Para conectar-se a um grupo de disponibilidade, especifique o ouvinte do grupo de disponibilidade como o servidor em sua cadeia de conexão.  
  
-   Conectar-se a uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] configurada com mais de 64 endereços IP causará uma falha de conexão.  
  
-   O comportamento de um aplicativo que usa a propriedade de conexão **MultiSubnetFailover** não é afetado com base no tipo de autenticação: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Autenticação, Autenticação Kerberos ou Autenticação do Windows.  
  
-   Você pode aumentar o valor de **loginTimeout** para acomodar o tempo de failover e reduzir as tentativas de repetição de conexão do aplicativo.  
  
-   Não há suporte a transações distribuídas.  
  
 Se o roteamento somente leitura não estiver em ação, conectar-se a um local de réplica secundária em um grupo de disponibilidade apresentará falha nas seguintes situações:  
  
1.  Se o local de réplica secundário não for configurado para aceitar conexões.  
  
2.  Se um aplicativo usar **ApplicationIntent=ReadWrite** (discutido abaixo) e o local de réplica secundária estiver configurado para acesso somente leitura.  
  
 Uma conexão falhará se uma réplica primária for configurada para rejeitar cargas de trabalho somente leitura e a cadeia de conexão contiver **ApplicationIntent=ReadOnly**.  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>Atualizando para usar clusters de várias sub-redes a partir do espelhamento de banco de dados  
 Um erro de conexão ocorrerá se as palavras-chave de conexão **MultiSubnetFailover** e **Failover_Partner** estiverem presentes na cadeia de conexão. Um erro também ocorrerá se a palavra-chave **MultiSubnetFailover** for usada e o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] retornar uma resposta de parceiro de failover indicando que ela faz parte de um par de espelhamento de banco de dados.  
  
 Se você atualizar um aplicativo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client que atualmente usa o espelhamento de banco de dados em um cenário de várias sub-redes, deverá remover a propriedade de conexão **Failover_Partner** e substituí-la por **MultiSubnetFailover** definido como **Yes** e substituir o nome do servidor da cadeia de conexão por um ouvinte de grupo de disponibilidade. Se uma cadeia de conexão usa **Failover_Partner** e **MultiSubnetFailover=Yes**, o driver gerará um erro. No entanto, se uma cadeia de conexão usar **Failover_Partner** e **MultiSubnetFailover=No** (ou **ApplicationIntent=ReadWrite**), o aplicativo usará o espelhamento de banco de dados.  
  
 O driver retornará um erro se o espelhamento de banco de dados for usado no banco de dados primário no AG e se **MultiSubnetFailover=Yes** for usado na cadeia de conexão que se conecta a um banco de dados primário, em vez de ao ouvinte de um grupo de disponibilidade.  
  
## <a name="specifying-application-intent"></a>Especificando a intenção do aplicativo  
 Quando **ApplicationIntent = ReadOnly**, o cliente solicita uma carga de trabalho de leitura ao se conectar a um banco de dados do Always On habilitado. O servidor irá impor a intenção no momento da conexão e durante uma instrução USE de banco de dados, mas somente para um banco de dados habilitado para AlwaysOn.  
  
 A palavra-chave **ApplicationIntent** não funciona com bancos de dados herdados somente leitura.  
  
 Um banco de dados pode permitir ou impedir que cargas de trabalho de leitura no banco de dados de sempre no destino. (Isso é feito com a cláusula **ALLOW_CONNECTIONS** das instruções **PRIMARY_ROLE** e **SECONDARY_ROLE**[!INCLUDE[tsql](../../../includes/tsql-md.md)].)  
  
 A palavra-chave **ApplicationIntent** é usada para habilitar o roteamento somente leitura.  
  
## <a name="read-only-routing"></a>Roteamento somente leitura  
 O roteamento somente leitura é um recurso que pode assegurar a disponibilidade de uma réplica somente leitura de um banco de dados. Para habilitar roteamento somente leitura:  
  
1.  Você deve conectar-se a um ouvinte de grupo de disponibilidade AlwaysOn.  
  
2.  A palavra-chave de cadeia de conexão **ApplicationIntent** deve ser definida como **ReadOnly**.  
  
3.  O grupo de disponibilidade deve ser configurado pelo administrador de banco de dados para permitir o roteamento somente leitura.  
  
 É possível que nem todas as várias conexões que usam roteamento somente leitura se conectem à mesma réplica somente leitura. Alterações na sincronização de banco de dados ou alterações na configuração de roteamento de servidor podem resultar em conexões de cliente com réplicas somente leitura diferentes. Para garantir que todas as solicitações somente leitura conectem-se à mesma réplica somente leitura, não transmita um ouvinte de grupo de disponibilidade à palavra-chave de cadeia de conexão **Server**. Em vez disso, especifique o nome da instância somente leitura.  
  
 O roteamento somente leitura pode demorar mais tempo do que a conexão ao primário porque o roteamento somente leitura conecta-se primeiramente ao primário e depois procura o melhor secundário legível disponível. Por isso, você deve aumentar seu tempo limite de logon.  
  
## <a name="odbc"></a>ODBC  
 Duas palavras-chave de cadeia de conexão ODBC foram adicionadas para oferecer suporte ao [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client:  
  
-   **ApplicationIntent**  
  
-   **MultiSubnetFailover**  
  
 Para obter mais informações sobre essas palavras-chave de cadeia de conexão do ODBC no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, consulte [Usando palavras-chave da cadeia de conexão com o SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 As propriedades de conexão equivalentes são:  
  
-   **SQL_COPT_SS_APPLICATION_INTENT**  
  
-   **SQL_COPT_SS_MULTISUBNET_FAILOVER**  
  
 Para obter mais informações sobre as propriedades de conexão ODBC no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, consulte [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md).  
  
 A funcionalidade das palavras-chave **ApplicationIntent** e **MultiSubnetFailover** será exposta no Administrador de Fonte de Dados ODBC para DSNs que usam o driver do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, no [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].  
  
 Um aplicativo ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client pode usar uma das três funções para estabelecer a conexão:  
  
|Função|Description|  
|--------------|-----------------|  
|[SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md)|A lista de servidores retornada por **SQLBrowseConnect** não incluirá VNNs. Você consultará apenas uma lista de servidores sem nenhuma indicação se o servidor for autônomo, ou um servidor primário ou secundário em um cluster WSFC (Windows Server Failover Clustering) que contenha duas ou mais instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] habilitadas para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Se você se conectar a um servidor e obtiver uma falha, talvez isso aconteça porque você se conectou a um servidor e a configuração de **ApplicationIntent** não é compatível com a configuração de servidor.<br /><br /> Como **SQLBrowseConnect** não reconhece servidores em um cluster WSFC (Windows Server Failover Clustering) que contém duas ou mais instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] habilitadas para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], o **SQLBrowseConnect** ignora a palavra-chave de cadeia de conexão **MultiSubnetFailover**.|  
|[SQLConnect](../../../relational-databases/native-client-odbc-api/sqlconnect.md)|O**SQLConnect** oferece suporte a **ApplicationIntent** e **MultiSubnetFailover** por meio de um nome de fonte de dados (DSN) ou propriedades da conexão.|  
|[SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md)|O**SQLDriverConnect** oferece suporte a **ApplicationIntent** e **MultiSubnetFailover** por meio de palavras-chave de cadeia de conexão, propriedades de conexão ou DSN.|  
  
## <a name="ole-db"></a>OLE DB  
 O OLE DB no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client não oferece suporte à palavra-chave **MultiSubnetFailover**.  
  
 O OLE DB no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client oferecerá suporte à tentativa de aplicativo. A tentativa de aplicativo se comportará da mesma maneira em aplicativos OLE DB e ODBC (consulte acima).  
  
 Uma palavras-chave de cadeia de conexão OLE DB foi adicionada para oferecer suporte ao [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client:  
  
-   **Tentativa de aplicativo**  
  
 Para obter mais informações sobre essas palavras-chave de cadeia de conexão no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, consulte [Usando palavras-chave da cadeia de conexão com o SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 As propriedades de conexão equivalentes são:  
  
-   **SSPROP_INIT_APPLICATIONINTENT**  
  
-   **DBPROP_INIT_PROVIDERSTRING**  
  
 Um aplicativo OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client pode usar um dos métodos para especificar uma tentativa de aplicativo:  
  
 **IDBInitialize:: Initialize**  
 **IDBInitialize::Initialize** usa o conjunto previamente configurado de propriedades para inicializar a fonte de dados e criar o objeto de fonte de dados. Especifique a tentativa de aplicativo como uma propriedade de provedor ou como parte da cadeia de caracteres de propriedades estendidas.  
  
 **IDataInitialize:: Getdatasource**  
 **IDataInitialize::GetDataSource** usa uma cadeia de conexão de entrada que pode conter a palavra-chave **Application Intent**.  
  
 **IDBProperties::GetProperties**  
 **IDBProperties::GetProperties** recupera o valor da propriedade atualmente definida na fonte de dados.  Você pode recuperar o valor de **Application Intent** através das propriedades _INIT_PROVIDERSTRING e SSPROP_INIT_APPLICATIONINTENT.  
  
 **Idbproperties:: SetProperties**  
 Para definir o valor da propriedade **ApplicationIntent**, chame **IDBProperties::SetProperties** passando a propriedade **SSPROP_INIT_APPLICATIONINTENT** com o valor da propriedade "**ReadWrite**" ou "**ReadOnly**" ou **DBPROP_INIT_PROVIDERSTRING** com o valor contendo "**ApplicationIntent=ReadOnly**" ou "**ApplicationIntent=ReadWrite**".  
  
 Você pode especificar a tentativa de aplicativo no campo Propriedades de Tentativa de Aplicativo da guia Tudo na caixa de diálogo **Propriedades de Vínculo de Dados**.  
  
 Quando forem estabelecidas conexões implícitas, a conexão implícita usará a configuração de tentativa de aplicativo da conexão pai. Da mesma forma, várias sessões criadas a partir da mesma fonte de dados herdarão a configuração de tentativa de aplicativo da fonte de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos do SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [Usando palavras-chave da cadeia de conexão com o SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)  
  
  
