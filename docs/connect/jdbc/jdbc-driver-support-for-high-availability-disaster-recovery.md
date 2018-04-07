---
title: Suporte a Driver JDBC para alta disponibilidade, recuperação de desastres | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 62de4be6-b027-427d-a7e5-352960e42877
caps.latest.revision: 40
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 1e41503e9b319d1e4372d93d835c4791563fd2da
ms.sourcegitcommit: 094c46e7fa6de44735ed0040c65a40ec3d951b75
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
# <a name="jdbc-driver-support-for-high-availability-disaster-recovery"></a>Suporte a JDBC driver para alta disponibilidade e recuperação de desastre
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Este tópico discute [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] suporte para alta disponibilidade, recuperação de desastres – [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]. Para obter mais informações sobre o [!INCLUDE[ssHADR](../../includes/sshadr_md.md)], consulte os Manuais Online do [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] .  
  
 Começando na versão 4.0 do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], você pode especificar o ouvinte do grupo de disponibilidade de uma (alta disponibilidade, recuperação de desastres) o grupo de disponibilidade (AG) na propriedade de conexão. Se um [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] aplicativo está conectado ao banco de dados AlwaysOn que efetua failover, a conexão original será interrompida e o aplicativo deverá abrir uma nova conexão para continuar o trabalho após o failover. O seguinte [propriedades de conexão](../../connect/jdbc/setting-the-connection-properties.md) foram adicionados em [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]:  
  
-   **multiSubnetFailover**  
  
-   **applicationIntent**
 
Especifique multiSubnetFailover = true, ao conectar-se ao ouvinte de grupo de disponibilidade de um grupo de disponibilidade ou uma instância de Cluster de Failover. Observe que **multiSubnetFailover** é false por padrão. Use **applicationIntent** para declarar o tipo de carga de trabalho do aplicativo. Consulte as seções a seguir para obter mais detalhes.
 
Começando na versão 6.0 do Microsoft JDBC Driver para SQL Server, uma nova propriedade de conexão **transparentNetworkIPResolution** (TNIR) é adicionada para conexão transparente para grupos de disponibilidade AlwaysOn ou para um servidor que tem vários endereços IP associados. Quando **transparentNetworkIPResolution** for true, o driver tentará conectar-se para o primeiro endereço IP disponível. Se a primeira tentativa falhar, o driver tenta se conectar a todos os endereços IP em paralelo, até que o tempo limite expirar, descartando as tentativas de conexão pendentes quando uma delas é bem-sucedida.   

Observe que:
* transparentNetworkIPResolution é verdadeiro por padrão
* transparentNetworkIPResolution será ignorado se multiSubnetFailover for verdadeiro
* transparentNetworkIPResolution será ignorado se o espelhamento de banco de dados é usado
* transparentNetworkIPResolution será ignorado se houver mais de 64 endereços IP
* Quando o transparentNetworkIPResolution for true, a primeira tentativa de conexão usa um valor de tempo limite de 500 ms. O restante das tentativas de conexão seguem a mesma lógica como o recurso de multiSubnetFailover. 

> [!NOTE]  
Se você estiver usando o Microsoft JDBC Driver 4.2 (ou inferior) para o SQL Server e se **multiSubnetFailover** for false, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] tenta se conectar ao primeiro endereço IP. Se o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] não é possível estabelecer uma conexão com o primeiro endereço IP, a conexão falhará. O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] não tentará se conectar a qualquer endereço IP subsequente associado ao servidor. 

  
> [!NOTE]  
>  O aumento do tempo limite de conexão e a implementação de lógica de repetição de conexão aumentarão a probabilidade de um aplicativo se conectar a um grupo de disponibilidade. Além disso, como uma conexão pode falhar devido a um failover de grupo de disponibilidade, você deve implementar lógica de repetição de conexão, repetindo uma conexão com falha até se reconectar.  
  
 
  
## <a name="connecting-with-multisubnetfailover"></a>Conectando-se ao MultiSubnetFailover  
 Sempre especifique **multiSubnetFailover = true** ao se conectar ao ouvinte do grupo de disponibilidade de um [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] o grupo de disponibilidade ou uma [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] instância de Cluster de Failover. **multiSubnetFailover** permite failover mais rápido para todos os grupos de disponibilidade e instâncias de cluster de failover no [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] e reduzirá significativamente o tempo de failover para topologias AlwaysOn únicas e de várias sub-redes. Durante um failover de várias sub-redes, o cliente tentará conexões em paralelo. Durante um failover de sub-rede, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] repetirá agressivamente a conexão TCP.  
  
 O **multiSubnetFailover** propriedade de conexão indica que o aplicativo está sendo implantado em um grupo de disponibilidade ou instância de Cluster de Failover e que o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] tentará se conectar ao banco de dados na réplica primária [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] instância tentando se conectar a todos os IPs de endereços. Quando **MultiSubnetFailover = true** é especificado para uma conexão, o cliente repete as tentativas de conexão TCP mais rápido do que os intervalos de retransmissão de TCP do sistema operacional padrão. Isto permite uma reconexão mais rápida depois de failover de um Grupo de disponibilidade AlwaysOn ou uma Instância de Cluster de Failover AlwaysOn e é aplicável a Grupos de disponibilidade único e de várias sub-redes e Instâncias de Cluster de Failover.  
  
 Para obter mais informações sobre palavras-chave de cadeia de caracteres de conexão no [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], consulte [definindo as propriedades de Conexão](../../connect/jdbc/setting-the-connection-properties.md).  
  
 Especificando **multiSubnetFailover = true** ao conectar-se a algo que não seja um ouvinte de grupo de disponibilidade ou instância de Cluster de Failover pode resultar em um impacto negativo no desempenho e não é suportado.  
  
 Se o gerenciador de segurança não for instalado, a Máquina Virtual Java armazenará VIPs (endereços IP virtuais) em cache por um período determinado, por padrão, definido pela implementação JDK e as propriedades Java networkaddress.cache.ttl e networkaddress.cache.negative.ttl. Se o gerenciador de segurança JDK for instalado, a Máquina Virtual Java armazenará VIPs em cache e não atualizará o cache, por padrão. Você deve definir a "vida útil" (networkaddress.cache.ttl) para um dia no cache da Máquina Virtual Java. Se você não alterar o valor padrão para um dia (ou valor parecido), o valor antigo não será limpo no cache da Máquina Virtual Java quando um VIP for adicionado ou atualizado. Para obter mais informações sobre networkaddress.cache.ttl e networkaddress.cache.negative.ttl, consulte [ http://download.oracle.com/javase/6/docs/technotes/guides/net/properties.html ](http://download.oracle.com/javase/6/docs/technotes/guides/net/properties.html).  
  
 Use as diretrizes a seguir para conectar-se a um servidor em um grupo de disponibilidade ou Instância de Cluster de Failover:  
  
-   O driver gerará um erro se o **instanceName** propriedade de conexão é usada na mesma cadeia de conexão como o **multiSubnetFailover** propriedade de conexão. Isso acontece porque o Navegador SQL não é usado em um grupo de disponibilidade. No entanto, se o **portNumber** propriedade de conexão também for especificada, o driver ignorará **instanceName** e usar **portNumber**.  
  
-   Use o **multiSubnetFailover** propriedade de conexão ao se conectar a uma única ou várias sub-redes, melhorará o desempenho de ambos.  
  
-   Para conectar-se a um grupo de disponibilidade, especifique o ouvinte do grupo de disponibilidade como o servidor em sua cadeia de conexão. Por exemplo, jdbc:sqlserver://VNN1.  
  
-   Conectar-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] configurada com mais de 64 endereços IP causará uma falha de conexão.  
  
-   Comportamento de um aplicativo que usa o **multiSubnetFailover** propriedade de conexão não é afetada com base no tipo de autenticação: [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] autenticação, a autenticação Kerberos ou autenticação do Windows.  
  
-   Aumente o valor de **loginTimeout** para acomodar o tempo de failover e reduzir as tentativas de repetição de conexão do aplicativo.  
  
-   Não há suporte a transações distribuídas.  
  
 Se o roteamento somente leitura não estiver em ação, conectar-se a um local de réplica secundária em um grupo de disponibilidade apresentará falha nas seguintes situações:  
  
1.  Se o local de réplica secundário não for configurado para aceitar conexões.  
  
2.  Se um aplicativo usa **applicationIntent = ReadWrite** (abordado abaixo) e o local de réplica secundária está configurado para acesso somente leitura.  
  
 Uma conexão falhará se uma réplica primária for configurada para rejeitar cargas de trabalho somente leitura e a cadeia de conexão contiver **ApplicationIntent=ReadOnly**.  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>Atualizando para usar clusters de várias sub-redes a partir do espelhamento de banco de dados  
 Se você atualizar um [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] aplicativo que usa espelhamento de banco de dados em um cenário de várias sub-redes, você deve remover o **failoverPartner** propriedade de conexão e substituí-lo por **multiSubnetFailover**  definida como **true** e substitua o nome do servidor na cadeia de conexão com um ouvinte de grupo de disponibilidade. Se uma cadeia de caracteres de conexão usa **failoverPartner** e **multiSubnetFailover = true**, o driver gerará um erro. No entanto, se uma cadeia de caracteres de conexão usa **failoverPartner** e **multiSubnetFailover = false** (ou **ApplicationIntent = ReadWrite**), o aplicativo usará o banco de dados o espelhamento.  
  
 O driver retornará um erro se o espelhamento de banco de dados é usado no banco de dados primário no AG e se **multiSubnetFailover = true** é usado na cadeia de conexão que se conecta a um banco de dados primário em vez de um grupo de disponibilidade ouvinte.  


[!INCLUDE[specify-application-intent_read-only-routing](~/includes/paragraph-content/specify-application-intent-read-only-routing.md)]


## <a name="new-methods-supporting-multisubnetfailover-and-applicationintent"></a>Novos métodos que oferecem suporte a multiSubnetFailover e applicationIntent  
 Os seguintes métodos oferecem acesso programático para o **multiSubnetFailover**, **applicationIntent** e **transparentNetworkIPResolution** cadeia de caracteres de conexão palavras-chave:  
  
-   [SQLServerDataSource.getApplicationIntent](../../connect/jdbc/reference/getapplicationintent-method-sqlserverdatasource.md)  
  
-   [SQLServerDataSource.setApplicationIntent](../../connect/jdbc/reference/setapplicationintent-method-sqlserverdatasource.md)  
  
-   [SQLServerDataSource.getMultiSubnetFailover](../../connect/jdbc/reference/getmultisubnetfailover-method-sqlserverdatasource.md)  
  
-   [SQLServerDataSource.setMultiSubnetFailover](../../connect/jdbc/reference/setmultisubnetfailover-method-sqlserverdatasource.md)  
  
-   [SQLServerDriver.getPropertyInfo](../../connect/jdbc/reference/getpropertyinfo-method-sqlserverdriver.md)  

-   SQLServerDataSource.setTransparentNetworkIPResolution

-   SQLServerDataSource.getTransparentNetworkIPResolution
  
 O **getMultiSubnetFailover**, **setMultiSubnetFailover**, **getApplicationIntent**, **setApplicationIntent**, **getTransparentNetworkIPResolution** e **setTransparentNetworkIPResolution** métodos também são adicionados à [classe SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md), [ Classe SQLServerConnectionPoolDataSource](../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md), e [classe SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md).  
  
## <a name="ssl-certificate-validation"></a>Validação do certificado SSL  
 Um grupo de disponibilidade consiste em vários servidores físicos. [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)] adicionado suporte para **nome alternativo da entidade** nos certificados SSL para vários hosts podem ser associados com o mesmo certificado. Para obter mais informações sobre o SSL, consulte [Noções básicas sobre o suporte a SSL](../../connect/jdbc/understanding-ssl-support.md).  
  
## <a name="see-also"></a>Consulte também  
 [Conectando ao SQL Server com o Driver JDBC](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)   
 [Configurando as propriedades de conexão](../../connect/jdbc/setting-the-connection-properties.md)  
  
  
