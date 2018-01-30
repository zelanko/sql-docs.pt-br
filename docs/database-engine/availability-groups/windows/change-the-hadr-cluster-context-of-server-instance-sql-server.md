---
title: "Alterar o contexto do cluster HADR da instância de servidor (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], WSFC clusters
- Availability replicas [SQL Server], change WSFC cluster context
ms.assetid: ecd99f91-b9a2-4737-994e-507065a12f80
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e6d67df05f5cd24b3c5b1f02273708633263f1d0
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="change-the-hadr-cluster-context-of-server-instance-sql-server"></a>Alterar o contexto do cluster HADR da instância de servidor (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Este tópico descreve como mudar o contexto do cluster HADR de uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando [!INCLUDE[tsql](../../../includes/tsql-md.md)] no [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] e em versões posteriores. O *contexto do cluster HADR* determina qual cluster do WSFC (Clustering de Failover de Windows Server) gerencia os metadados das réplicas de disponibilidade hospedadas pela instância de servidor.  
  
 Alterne o contexto do cluster HADR somente durante uma migração entre clusters de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] para uma instância do [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] em um novo cluster WSFC. A migração entre clusters de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] oferece suporte à atualização do sistema operacional para o [!INCLUDE[win8](../../../includes/win8-md.md)] ou o [!INCLUDE[win8srv](../../../includes/win8srv-md.md)] com tempo de inatividade mínimo de grupos de disponibilidade. Para obter mais informações, veja [Migração entre clusters de grupos de disponibilidade AlwaysOn para atualização do sistema operacional](http://msdn.microsoft.com/library/jj873730.aspx).  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Pré-requisitos](#Prerequisites)  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para mudar o contexto do cluster de uma réplica de disponibilidade, usando:**  [Transact-SQL](#TsqlProcedure)  
  
-   **Acompanhamento:**  [após a troca do contexto do cluster de uma réplica de disponibilidade](#FollowUp)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
-   [Conteúdo relacionado](#RelatedContent)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
> [!CAUTION]  
>  Alterne o contexto do cluster HADR somente durante a migração entre clusters das implantações de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] .  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Só é possível alternar o contexto do cluster HADR do cluster WSFC local para um cluster remoto e, depois, do cluster remoto para o cluster local. Você não pode alternar o contexto do cluster HADR de um cluster remoto para outro cluster remoto.  
  
-   O contexto do cluster HADR pode ser alternado para um cluster remoto somente quando a instância do SQL Server não está hospedando réplicas de disponibilidade.  
  
-   Um contexto do cluster HADR remoto pode ser alternado novamente para o cluster local a qualquer momento. Entretanto, o contexto não poderá ser alternado novamente enquanto a instância de servidor estiver hospedando réplicas de disponibilidade.  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
  
-   A instância de servidor na qual você altera o contexto do cluster HADR deve executar o [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] ou posterior (edição Enterprise ou superior).  
  
-   A instância de servidor deve estar habilitada para AlwaysOn. Para obter mais informações, consulte [Habilitar e desabilitar Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md).  
  
-   Para qualificar-se para ser alternada do contexto de cluster local para um cluster remoto, uma instância de servidor não pode hospedar réplicas de disponibilidade. A exibição de catálogo [sys.availability_replicas](../../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md) não deve retornar linhas.  
  
     Se existirem réplicas de disponibilidade na instância do servidor, antes de alterar o contexto do cluster HADR, faça o seguinte:  
  
    |Função da réplica|Ação|Link|  
    |------------------|------------|----------|  
    |Primária|Colocar o grupo de disponibilidade offline.|[Colocar um grupo de disponibilidade offline &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/take-an-availability-group-offline-sql-server.md)|  
    |Secundário|Remover a réplica de seu grupo de disponibilidade|[Remover uma réplica secundária de um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server.md)|  
  
-   Antes de alternar de um cluster remoto para o cluster local, verifique se todas as réplicas de confirmação síncrona foram sincronizadas (SYNCHRONIZED).  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   É recomendável especificar o nome de domínio completo. Isso é necessário porque, para localizar o endereço IP de destino de um nome curto, ALTER SERVER CONFIGURATION usa a resolução DNS. Em algumas situações, dependendo da ordem de pesquisa de DNS, o uso de um nome curto pode gerar confusão. Por exemplo, considere o comando a seguir, que é executado em um nó no domínio `abc` , (`node1.abc.com`). O cluster de destino pretendido é o cluster `CLUS01` no domínio `xyz` (`clus01.xyz.com`). No entanto, o domínio local também hospeda um cluster denominado `CLUS01` (`clus01.abc.com`).  
  
     Se o nome curto do cluster de destino, `CLUS01`, foi especificado, a resolução de nome DNS pode retornar o endereço IP do cluster incorreto, `clus01.abc.com`. Para evitar essa confusão, especifique o nome completo do cluster de destino, como no seguinte exemplo:  
  
    ```  
    ALTER SERVER CONFIGURATION SET HADR CLUSTER CONTEXT = 'clus01.xyz.com'  
    ```  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
  
-   **logon do SQL Server**  
  
     Requer a permissão CONTROL SERVER.  
  
-   **Conta do serviço SQL Server**  
  
     A conta do serviço [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] da instância de servidor deve ter:  
  
    -   Permissão para abrir o cluster WSFC de destino.  
  
    -   Acesso de leitura/gravação no WSFC remoto.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para alterar o contexto do cluster WSFC de uma réplica de disponibilidade**  
  
1.  Conecte-se à instância de servidor que hospeda a réplica primária ou uma réplica secundária do grupo de disponibilidade.  
  
2.  Use a cláusula SET HADR CLUSTER CONTEXT da instrução [ALTER SERVER CONFIGURATION](../../../t-sql/statements/alter-server-configuration-transact-sql.md) , da seguinte forma:  
  
     ALTER SERVER CONFIGURATION SET HADR CLUSTER CONTEXT **=** { **'***windows_cluster***'** | LOCAL }  
  
     onde:  
  
     *cluster_windows*  
     O CON (nome do objeto de cluster) de um cluster WSFC. Você pode especificar o nome curto ou o nome de domínio completo. É recomendável especificar o nome de domínio completo. Para obter mais informações, consulte [Recomendações](#Recommendations)anteriormente neste tópico.  
  
     LOCAL  
     O cluster WSFC local.  
  
### <a name="examples"></a>Exemplos  
 O exemplo a seguir altera o contexto do cluster HADR para um cluster diferente. Para identificar o cluster WSFC de destino, `clus01`, o exemplo especifica o nome de objeto completo do cluster, `clus01.xyz.com`.  
  
```  
ALTER SERVER CONFIGURATION SET HADR CLUSTER CONTEXT = 'clus01.xyz.com';  
```  
  
 O exemplo a seguir altera o contexto do cluster HADR para o cluster WSFC local.  
  
```  
ALTER SERVER CONFIGURATION SET HADR CLUSTER CONTEXT = LOCAL;  
```  
  
##  <a name="FollowUp"></a> Acompanhamento: depois de alternar o contexto do cluster de uma réplica de disponibilidade  
 O novo contexto do cluster HADR tem efeito imediatamente, sem a reinicialização da instância de servidor. A configuração de contexto do cluster HADR é uma configuração persistente em nível de instância que permanece inalterada se a instância de servidor é reiniciada.  
  
 Confirme o novo contexto do cluster HADR consultando a exibição de gerenciamento dinâmico [sys.dm_hadr_cluster](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-transact-sql.md) , da seguinte forma:  
  
```  
SELECT cluster_name FROM sys.dm_hadr_cluster  
```  
  
 Essa consulta deve retornar o nome do cluster para o qual você define o contexto do cluster HADR.  
  
 Quando o contexto do cluster HADR é alternado para um novo cluster:  
  
-   Os metadados são limpos para todas as réplicas de disponibilidade hospedadas no momento pela instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Todos os bancos de dados que antes pertenciam a uma réplica de disponibilidade agora se encontram no estado RESTORING.  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Remover um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-an-availability-group-listener-sql-server.md)  
  
-   [Colocar um grupo de disponibilidade offline &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/take-an-availability-group-offline-sql-server.md)  
  
-   [Adicionar uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Remover uma réplica secundária de um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server.md)  
  
-   [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [Unir um banco de dados secundário a um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
##  <a name="RelatedContent"></a> Conteúdo relacionado  
  
-   [Artigos técnicos do SQL Server 2012](http://msdn.microsoft.com/library/bb418445\(SQL.10\).aspx)  
  
-   [Blog da equipe do AlwaysOn do SQL Server: o blog oficial da equipe do AlwaysOn do SQL Server](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
## <a name="see-also"></a>Consulte Também  
 [Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [WSFC &#40;Windows Server Failover Clustering&#41; com o SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)   
 [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-server-configuration-transact-sql.md)  
  
  
