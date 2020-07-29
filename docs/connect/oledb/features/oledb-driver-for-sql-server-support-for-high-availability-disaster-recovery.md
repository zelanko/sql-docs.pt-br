---
title: Compatibilidade do Driver do OLE DB para SQL Server para alta disponibilidade e recuperação de desastre | Microsoft Docs
description: Compatibilidade do Driver do OLE DB para SQL Server para alta disponibilidade e recuperação de desastre
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 26c340a10118f115db87c742e570831edc8b65f6
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86006913"
---
# <a name="ole-db-driver-for-sql-server-support-for-high-availability-disaster-recovery"></a>Suporte ao Driver do OLE DB para SQL Server para alta disponibilidade e recuperação de desastre
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Este artigo discute o suporte do *Driver do OLE DB para SQL Server* para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Para obter mais informações sobre [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [Ouvintes do Grupo de Disponibilidade, Conectividade do Cliente e Failover do Aplicativo &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md), [Criação e Configuração de Grupos de Disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md), [Clustering de Failover e Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md) e [Secundárias Ativas: Réplicas Secundárias Legíveis&#40;Grupos de Disponibilidade AlwaysOn&#41;](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md).  
  
 Você pode especificar o ouvinte de um determinado grupo de disponibilidade na cadeia de conexão. Se um aplicativo do Driver do OLE DB para SQL Server estiver conectado com um banco de dados em um grupo de disponibilidade que executa failover, a conexão original será interrompida e o aplicativo deverá abrir uma nova conexão para continuar o trabalho após o failover.  
  
 Se você não estiver se conectando a um ouvinte do grupo de disponibilidade e se vários endereços IP forem associados com um nome de host, o Driver do OLE DB para SQL Server iterará em sequência por todos os endereços IP associados à entrada DNS. Isso pode demorar muito se o primeiro endereço IP retornado pelo servidor DNS não estiver associado a nenhuma NIC (placa de interface de rede). Ao conectar-se a um ouvinte de grupo de disponibilidade, o Driver do OLE DB para SQL Server tenta estabelecer conexões com todos os endereços IP paralelamente e, se uma conexão tentar continuar, o driver descartará qualquer tentativa de conexão pendente.  
  
> [!NOTE]  
> O aumento do tempo limite de conexão e a implementação de lógica de repetição de conexão aumentarão a probabilidade de um aplicativo se conectar a um grupo de disponibilidade. Além disso, como uma conexão pode falhar devido a um failover de grupo de disponibilidade, você deve implementar lógica de repetição de conexão, repetindo uma conexão com falha até se reconectar.  
  
## <a name="connecting-with-multisubnetfailover"></a>Conectando-se ao MultiSubnetFailover  
 Sempre especifique **MultiSubnetFailover=Yes** quando for se conectar a um ouvinte do grupo de disponibilidade Always On do SQL Server ou uma instância de cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O **MultiSubnetFailover** permite o failover mais rápido para todos os Grupos de Disponibilidade AlwaysOn e instâncias de cluster de failover no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e reduzirá significativamente o tempo de failover para topologias Always On de uma ou várias sub-redes. Durante um failover de várias sub-redes, o cliente tentará conexões em paralelo. Durante um failover de sub-rede, o Driver do OLE DB para SQL Server tentará novamente a conexão TCP.  
  
 A propriedade de conexão **MultiSubnetFailover** indica que o aplicativo está sendo implantado em um grupo de disponibilidade ou instância de cluster de failover e que o Driver do OLE DB para SQL Server tentará se conectar ao banco de dados na instância primária do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tentando se conectar a todos os endereços IP do grupo de disponibilidade. Quando **MultiSubnetFailover=Yes** é especificado para uma conexão, o cliente repete as tentativas de conexão TCP mais rápido do que os intervalos de retransmissão TCP padrão do sistema operacional. Isso permite uma reconexão mais rápida depois de failover de um Grupos de Disponibilidade Always On ou uma Instância de Cluster de Failover e é aplicável a grupos de disponibilidade únicos e de várias sub-redes e Instâncias de Cluster de Failover.  
  
 Para saber mais sobre palavras-chave da cadeia de conexão, confira [Usando palavras-chave da cadeia de conexão com o OLE DB Driver para SQL Server](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md).  
  
 A especificação de **MultiSubnetFailover=Yes** durante a conexão a algo que não seja um ouvinte de grupo de disponibilidade ou uma Instância de Cluster de Failover pode resultar em um impacto de desempenho negativo e não há suporte para isso.  
  
 Use as diretrizes a seguir para conectar-se a um servidor em um grupo de disponibilidade ou Instância de Cluster de Failover:  
  
-   Use a propriedade de conexão **MultiSubnetFailover** quando estiver se conectando a uma ou várias sub-redes; isso melhorará o desempenho em ambos os casos.  
  
-   Para conectar-se a um grupo de disponibilidade, especifique o ouvinte do grupo de disponibilidade como o servidor em sua cadeia de conexão.  
  
-   Conectar-se a uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] configurada com mais de 64 endereços IP causará uma falha de conexão.  
  
-   O comportamento de um aplicativo que usa a propriedade de conexão **MultiSubnetFailover** não é afetado com base no tipo de autenticação: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Autenticação, Autenticação Kerberos ou Autenticação do Windows.  
  
-   Você pode aumentar o valor de **loginTimeout** para acomodar o tempo de failover e reduzir as tentativas de repetição de conexão do aplicativo.  
  
-   Não há suporte para transações distribuídas.  
  
Se o roteamento somente leitura não estiver em ação, conectar-se a um local de réplica secundária em um grupo de disponibilidade apresentará falha nas seguintes situações:  
  
1.  Se o local de réplica secundário não for configurado para aceitar conexões.  
  
2.  Se um aplicativo usar **ApplicationIntent=ReadWrite** (discutido abaixo) e o local de réplica secundária estiver configurado para acesso somente leitura.  
  
Uma conexão falhará se uma réplica primária for configurada para rejeitar cargas de trabalho somente leitura e a cadeia de conexão contiver **ApplicationIntent=ReadOnly**.  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>Atualizando para usar clusters de várias sub-redes a partir do espelhamento de banco de dados  
Um erro de conexão ocorrerá se as palavras-chave de conexão **MultiSubnetFailover** e **Failover_Partner** estiverem presentes na cadeia de conexão. Um erro também ocorrerá se a palavra-chave **MultiSubnetFailover** for usada e o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] retornar uma resposta de parceiro de failover indicando que ela faz parte de um par de espelhamento de banco de dados.  
  
Se você atualizar um aplicativo do OLE DB Driver para SQL Server que atualmente usa o espelhamento de banco de dados em um cenário de várias sub-redes, deverá remover a propriedade de conexão **Failover_Partner** e substituí-la por **MultiSubnetFailover** definido como **Yes** e substituir o nome do servidor da cadeia de conexão por um ouvinte de grupo de disponibilidade. Se uma cadeia de conexão usa **Failover_Partner** e **MultiSubnetFailover=Yes**, o driver gerará um erro. No entanto, se uma cadeia de conexão usar **Failover_Partner** e **MultiSubnetFailover=No** (ou **ApplicationIntent=ReadWrite**), o aplicativo usará o espelhamento de banco de dados.  
  
O driver retornará um erro se o espelhamento de banco de dados for usado no banco de dados primário no AG e se **MultiSubnetFailover=Yes** for usado na cadeia de conexão que se conecta a um banco de dados primário, em vez de ao ouvinte de um grupo de disponibilidade.  


[!INCLUDE[specify-application-intent_read-only-routing](~/includes/paragraph-content/specify-application-intent-read-only-routing.md)]


## <a name="ole-db"></a>OLE DB  
O Driver do OLE DB para SQL Server dá suporte às palavras-chave **ApplicationIntent** e **MultiSubnetFailover**.   
  
As duas palavras-chave do OLE DB da cadeia de conexão foram adicionadas para dar suporte a [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] no Driver do OLE DB para SQL Server:  
  
-   **ApplicationIntent** 
-   **MultiSubnetFailover**  
  
 Para saber mais sobre palavras-chave da cadeia de conexão no OLE DB Driver para SQL Server, confira [Usando palavras-chave da cadeia de conexão com o OLE DB Driver para SQL Server](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md).  

### <a name="application-intent"></a>Tentativa de aplicativo 

As propriedades de conexão equivalentes são:  
  
-   **SSPROP_INIT_APPLICATIONINTENT**  
  
-   **DBPROP_INIT_PROVIDERSTRING**  
  
Um aplicativo do Driver do OLE DB para SQL Server pode usar um dos métodos para especificar uma intenção de aplicativo:  
  
 -   **IDBInitialize::Initialize**  
 **IDBInitialize::Initialize** usa o conjunto previamente configurado de propriedades para inicializar a fonte de dados e criar o objeto de fonte de dados. Especifique a tentativa de aplicativo como uma propriedade de provedor ou como parte da cadeia de caracteres de propriedades estendidas.  
  
 -   **IDataInitialize::GetDataSource**  
 **IDataInitialize::GetDataSource** usa uma cadeia de conexão de entrada que pode conter a palavra-chave **Application Intent**.  
  
 -   **IDBProperties::SetProperties**  
 Para definir o valor da propriedade **ApplicationIntent**, chame **IDBProperties::SetProperties** passando a propriedade **SSPROP_INIT_APPLICATIONINTENT** com o valor da propriedade "**ReadWrite**" ou "**ReadOnly**" ou **DBPROP_INIT_PROVIDERSTRING** com o valor contendo "**ApplicationIntent=ReadOnly**" ou "**ApplicationIntent=ReadWrite**".  
  
Você pode especificar a tentativa de aplicativo no campo Propriedades de Tentativa de Aplicativo da guia Tudo na caixa de diálogo **Propriedades de Vínculo de Dados**.  
  
Quando forem estabelecidas conexões implícitas, a conexão implícita usará a configuração de tentativa de aplicativo da conexão pai. Da mesma forma, várias sessões criadas a partir da mesma fonte de dados herdarão a configuração de tentativa de aplicativo da fonte de dados.  
  
### <a name="multisubnetfailover"></a>MultiSubnetFailover

As propriedades de conexão equivalentes são:  
  
-   **SSPROP_INIT_MULTISUBNETFAILOVER**  
  
-   **DBPROP_INIT_PROVIDERSTRING**  

Um aplicativo do Driver do OLE DB para SQL Server pode usar um dos seguintes métodos para definir a opção MultiSubnetFailover:  

 -   **IDBInitialize::Initialize**  
 **IDBInitialize::Initialize** usa o conjunto previamente configurado de propriedades para inicializar a fonte de dados e criar o objeto de fonte de dados. Especifique a tentativa de aplicativo como uma propriedade de provedor ou como parte da cadeia de caracteres de propriedades estendidas.  
  
 -   **IDataInitialize::GetDataSource**  
 **IDataInitialize::GetDataSource** usa uma cadeia de conexão de entrada que pode conter a palavra-chave **MultiSubnetFailover**.  

-   **IDBProperties::SetProperties**  
Para definir o valor da propriedade **MultiSubnetFailover**, chame **IDBProperties::SetProperties** passando a propriedade **SSPROP_INIT_MULTISUBNETFAILOVER** com o valor **VARIANT_TRUE** ou **VARIANT_FALSE** ou a propriedade **DBPROP_INIT_PROVIDERSTRING** com um valor contendo "**MultiSubnetFailover=Yes**" ou "**MultiSubnetFailover=No**".

#### <a name="example"></a>Exemplo

```
DBPROP rgPropMultisubnet;

rgPropMultisubnet.dwPropertyID = SSPROP_INIT_MULTISUBNETFAILOVER;
rgPropMultisubnet.dwOptions = DBPROPOPTIONS_REQUIRED;
rgPropMultisubnet.dwStatus = DBPROPSTATUS_OK;
rgPropMultisubnet.colid = DB_NULLID;
V_VT(&(rgPropMultisubnet.vValue)) = VT_BOOL;
V_BOOL(&(rgPropMultisubnet.vValue)) = VARIANT_TRUE;

DBPROPSET PropSet;

PropSet.rgProperties = &rgPropMultisubnet;
PropSet.cProperties = 1;
PropSet.guidPropertySet = DBPROPSET_SQLSERVERDBINIT;
IDBProperties* pIDBProperties = NULL;
hr = pIDBInitialize->QueryInterface(IID_IDBProperties, (void **)&pIDBProperties);
pIDBProperties->SetProperties(1, &PropSet);
```

## <a name="see-also"></a>Consulte Também  
 [Recursos do OLE DB Driver for SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)    
 [Uso de palavras-chave de cadeia de conexão com o Driver do OLE DB para SQL Server](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)  
  
  
