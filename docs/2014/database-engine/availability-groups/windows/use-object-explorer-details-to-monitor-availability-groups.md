---
title: Use os detalhes do Pesquisador de objeto para monitorar grupos de disponibilidade (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygroup.OEdetails.f1
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], databases
- Availability Groups [SQL Server]
ms.assetid: 84affc47-40e0-43d9-855e-468967068c35
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5545b36aba250a04744b66abad5434f8573c053e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62788319"
---
# <a name="use-the-object-explorer-details-to-monitor-availability-groups-sql-server-management-studio"></a>Usar os detalhes do Pesquisador de Objetos para monitorar grupos de disponibilidade (SQL Server Management Studio)
  Este tópico descreve como usar o painel **Detalhes do Pesquisador de Objetos** do [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] para monitorar e gerenciar grupos de disponibilidade AlwaysOn, réplicas de disponibilidade e bancos de dados de disponibilidade existentes.  
  
> [!NOTE]  
>  Para obter informações sobre como usar o painel de detalhes do Pesquisador de objetos, veja [Painel de detalhes do Pesquisador de Objetos](../../../ssms/object/object-explorer-details-pane.md).  
  
-   **Antes de começar:**  [Pré-requisitos](#Prerequisites)  
  
-   **Para monitorar um grupo de disponibilidade usando:**  [SQL Server Management Studio](#SSMSProcedure)  
  
-   **Detalhes do Pesquisador de Objetos:**  
  
     [Detalhes do grupo de disponibilidade](#AvGroupsDetails)  
  
     [Detalhes da réplica de disponibilidade](#AvReplicaDetails)  
  
     [Detalhes do banco de dados de disponibilidade](#AvDbDetails)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 Conecte-se à instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (instância de servidor) que hospeda a réplica primária ou uma réplica secundária.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para monitorar os grupos de disponibilidade, as réplicas de disponibilidade e os bancos de dados de disponibilidade**  
  
1.  No menu Exibir, clique em **Detalhes do Pesquisador de Objetos**ou pressione a tecla **F7** .  
  
2.  No Pesquisador de Objetos, conecte-se à instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na qual você deseja monitorar um grupo de disponibilidade e clique no nome do servidor para expandir a árvore de servidores.  
  
3.  Expanda os nós **Alta Disponibilidade AlwaysOn** e **Grupos de Disponibilidade** .  
  
4.  O painel **Detalhes do Pesquisador de Objetos** exibe todos os grupos de disponibilidade para os quais a instância do servidor hospeda uma réplica. Para cada grupo de disponibilidade, a coluna **Instância do Servidor (Primária)** exibe o nome da instância do servidor que está hospedando a réplica primária.  Para exibir mais informações sobre um determinado grupo de disponibilidade, selecione-o no Pesquisador de Objetos.  
  
5.  O painel **Detalhes do Pesquisador de Objetos** exibe os nós **Réplicas de Disponibilidade** e **Bancos de Dados de Disponibilidade** desse grupo de disponibilidade:  
  
    -   Quando você expande o nó **Grupo de Disponibilidade** no Pesquisador de Objetos e seleciona o nó **Réplicas de Disponibilidade** , o painel **Detalhes do Pesquisador de Objetos** exibe informações sobre cada uma das réplicas de disponibilidade do grupo. Para obter mais informações, consulte [Detalhes da réplica de disponibilidade](#AvReplicaDetails)posteriormente neste tópico.  
  
         Para executar operações em várias réplicas de disponibilidade, selecione-as e clique com o botão direito do mouse para abrir um menu de contexto que lista os comandos disponíveis.  
  
    -   Quando você expande o nó **Grupo de Disponibilidade** no Pesquisador de Objetos e seleciona o nó **Bancos de Dados de Disponibilidade** , o painel **Detalhes do Pesquisador de Objetos** exibe informações sobre cada um dos bancos de dados de disponibilidade do grupo. Para obter mais informações, consulte [Detalhes do bancos de dados de disponibilidade](#AvDbDetails)posteriormente neste tópico.  
  
         Para executar operações em vários bancos de dados de disponibilidade, selecione-as e clique com o botão direito do mouse para abrir um menu de contexto que lista os comandos disponíveis.  
  
##  <a name="AvGroupsDetails"></a> Detalhes dos grupos de disponibilidade  
 A tela de detalhes **Grupos de Disponibilidade** exibe as seguintes colunas:  
  
 **Nome**  
 Lista as pastas de Ouvintes **Réplicas de Disponibilidade**, **Bancos de Dados de Disponibilidade**e **Grupo de Disponibilidade** do grupo de disponibilidade selecionado.  
  
##  <a name="AvReplicaDetails"></a> Detalhes da réplica de disponibilidade  
 A tela de detalhes **Replica de Disponibilidade** exibe as seguintes colunas:  
  
 **Instância do Servidor**  
 Exibe o nome da instância do servidor que hospeda a réplica de disponibilidade, junto com um ícone que indica o estado de conexão atual da instância do servidor para a instância do servidor local.  
  
 **Função**  
 Indica a função atual da réplica de disponibilidade, **Primária** ou **Secundária**. Para obter informações sobre as funções do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md).  
  
 **Modo de Conexão na Função Secundária**  
 Indica se os bancos de dados de uma determinada réplica de disponibilidade que está executando a função primária (isto é, está atuando como uma réplica secundária) podem aceitar conexões de clientes.  
  
 Os valores possíveis são os seguintes:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Não Permitir Conexões**|Nenhuma conexão direta é permitida para os bancos de dados de disponibilidade quando essa réplica de disponibilidade está agindo como uma réplica secundária. Os bancos de dados secundários não estão disponíveis para acesso de leitura.|  
|**Permitir Somente Conexões de Intenção de Leitura**|Apenas conexões diretas somente leitura são permitidas quando essa réplica está agindo como uma réplica secundária. Todos os bancos de dados na réplica estão disponíveis para acesso de leitura.|  
|**Permitir Todas as Conexões**|Todas as conexões são permitidas para estes bancos de dados para acesso somente leitura quando essa réplica está atuando como uma réplica secundária.|  
  
 **Estado da Conexão**  
 Indica se uma réplica secundária está conectada atualmente à réplica primária. Os valores possíveis são os seguintes:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Desconectado**|Para uma réplica de disponibilidade remota, indica que ela está desconectada da réplica de disponibilidade local. A resposta da réplica local ao estado Desconectado depende de sua função, da seguinte forma:<br /><br /> na réplica primária, se uma réplica secundária estiver desconectada, os bancos de dados secundários serão marcados como **Não Sincronizado** na réplica primária, e a réplica primária esperará que a secundária seja reconectada.<br /><br /> Na réplica secundária, ao detectar que está desconectada, a réplica secundária tentará reconectar-se à réplica primária.|  
|**Conectado**|Uma réplica de disponibilidade remota que está conectada atualmente à réplica local.|  
|**NULL**|Se a réplica local for uma réplica secundária, esse valor será NULL para outras réplicas secundárias.|  
  
 **Estado da Sincronização**  
 Indica se uma réplica secundária está sincronizada no momento com a réplica primária. Os valores possíveis são os seguintes:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Não Sincronizado**|O banco de dados não está sincronizado ou ainda não foi unido ao grupo de disponibilidade.|  
|**Sincronizado**|O banco de dados está sincronizado com o banco de dados primário na réplica primária atual, se houver, ou na réplica primária mais recente.<br /><br /> Observação: No modo de desempenho, o banco de dados nunca está no estado Synchronized.|  
|**NULL**|Estado desconhecido. Este valor ocorre quando a instância do servidor local não pode se comunicar com o cluster de failover do WSFC (isto é, o nó local não faz parte do quorum do WSFC).|  
  
> [!NOTE]  
>  Para obter informações sobre contadores de desempenho para réplicas de disponibilidade, veja [SQL Server, Réplica de Disponibilidade](../../../relational-databases/performance-monitor/sql-server-availability-replica.md).  
  
##  <a name="AvDbDetails"></a> Detalhes do banco de dados de disponibilidade  
 A tela de detalhes **Banco de Dados de Disponibilidade** exibe as seguintes propriedades dos bancos de dados de disponibilidade em um determinado grupo de disponibilidade:  
  
 **Nome**  
 O nome do banco de dados de disponibilidade.  
  
 **Estado da Sincronização**  
 Indica se um banco de dados de disponibilidade está sincronizado no momento com a réplica primária.  
  
 Os estados de sincronização possíveis são:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|Sincronizando|O banco de dados secundário recebeu os registros do log de transações do banco de dados primário que ainda não estão gravados no disco (protegidos).<br /><br /> Observação: No modo de confirmação assíncrona, o estado de sincronização é sempre **Synchronizing**.|  
  
 **Suspenso**  
 Indica se o banco de dados de disponibilidade está online no momento. Os valores possíveis são os seguintes:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Suspenso**|Esse estado indica que o banco de dados está suspenso localmente e precisa ser retomado manualmente.<br /><br /> Na réplica primária, o valor não é confiável para um banco de dados secundário. Para determinar com confiança se um banco de dados secundário está suspenso, consulte-o na réplica secundária que hospeda o banco de dados.|  
|**Não Unido**|Indica que o banco de dados secundário não foi unido ao grupo de disponibilidade ou foi removido do grupo.|  
|**Online**|Indica que o banco de dados não está suspenso na réplica de disponibilidade local e que o banco de dados está conectado.|  
|**Não Conectado**|Indica que a réplica secundária não pode conectar-se à réplica primária.|  
  
> [!NOTE]  
>  Para obter informações sobre contadores de desempenho para bancos de dados de disponibilidade, veja [SQL Server, Réplica de banco de dados](../../../relational-databases/performance-monitor/sql-server-database-replica.md).  
  
## <a name="see-also"></a>Consulte também  
 [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql)   
 [Use o painel AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)   
 [Exibir propriedades do grupo de disponibilidade &#40;SQL Server&#41;](view-availability-group-properties-sql-server.md)   
 [Exibir as propriedades da réplica de disponibilidade &#40;SQL Server&#41;](view-availability-replica-properties-sql-server.md)  
  
  
