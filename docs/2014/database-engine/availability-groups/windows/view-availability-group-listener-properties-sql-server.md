---
title: Exibir propriedades do ouvinte do grupo de disponibilidade (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygrouplistenerproperties.general.f1
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
ms.assetid: aca0d016-3228-40b8-bdc3-285ed6d9b280
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ef7fe316394a030350ceb12a0d1b8e2d48ee1d34
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936198"
---
# <a name="view-availability-group-listener-properties-sql-server"></a>Exibir propriedades do ouvinte do grupo de disponibilidade (SQL Server)
  Este tópico descreve como exibir as propriedades de um *ouvinte de grupo de disponibilidade* AlwaysOn usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)] no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
-   **Para exibir as propriedades do ouvinte, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para exibir as propriedades do ouvinte**  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância de servidor que hospeda qualquer réplica de disponibilidade do grupo de disponibilidade cujo ouvinte você deseja exibir. Clique no nome do servidor para expandir a arvore de servidores.  
  
2.  Expanda os nós **Alta Disponibilidade AlwaysOn** e **Grupos de Disponibilidade** .  
  
3.  Expanda o nó do grupo de disponibilidade e expanda o nó **Ouvintes de Grupos de Disponibilidade** .  
  
4.  Clique com o botão direito do mouse no ouvinte que você deseja exibir e selecione o comando **Propriedades** .  
  
5.  Isso abre a caixa de diálogo **Propriedades do Ouvinte do Grupo de Disponibilidade** . Para obter mais informações, veja [Propriedades do Ouvinte do Grupo de Disponibilidade (caixa de diálogo)](#AgListenerPropertiesDialog), mais adiante neste tópico.  
  
###  <a name="availability-group-listener-properties-dialog-box"></a><a name="AgListenerPropertiesDialog"></a> Propriedades do Ouvinte do Grupo de Disponibilidade (caixa de diálogo)  
 **Nome DNS do Ouvinte**  
 O nome da rede do ouvinte do grupo de disponibilidade.  
  
 **Porta**  
 A porta TCP usada pelo ouvinte.  
  
> [!NOTE]  
>  Se você estiver conectado com a réplica primária, poderá usar esse campo para modificar o número da porta do ouvinte. Isso exige a permissão ALTER AVAILABILITY GROUP no grupo de disponibilidade, a permissão CONTROL AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.  
  
 **Modo de Rede**  
 Indica o protocolo TCP usado pelo ouvinte, pode ser:  
  
 **DHCP**  
 O ouvinte usa um endereço IP dinâmico que é atribuído por um servidor que executa o Protocolo DHCP.  
  
 **IP Estático**  
 O ouvinte usa um ou mais endereços IP estáticos. Para acessar diferentes sub-redes, um ouvinte de grupo de disponibilidade deve usar endereços IP estáticos.  
  
 A grade exibe cada uma das sub-redes nas quais o ouvinte escuta, e o endereço IP associado àquela sub-rede.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para exibir as propriedades do ouvinte**  
  
 Para monitorar os ouvintes de disponibilidade, use as seguintes exibições:  
  
 [sys.availability_group_listener_ip_addresses](/sql/relational-databases/system-catalog-views/sys-availability-group-listener-ip-addresses-transact-sql)  
 Retorna uma linha para cada endereço IP virtual compatível que está online atualmente para um ouvinte de grupo de disponibilidade.  
  
 **Nomes de colunas:** listener_id, ip_address, ip_subnet_mask, is_dhcp, network_subnet_ip, network_subnet_prefix_length, network_subnet_ipv4_mask, state, state_desc  
  
 [sys.availability_group_listeners](/sql/relational-databases/system-catalog-views/sys-availability-group-listeners-transact-sql)  
 Para um determinado grupo de disponibilidade, retorna zero linhas indicando que nenhum nome de rede está associado ao grupo de disponibilidade ou retorna uma linha para cada configuração de ouvinte de grupo de disponibilidade no cluster do WSFC.  
  
 **Nomes de colunas:** group_id, listener_id, dns_name, port, is_conformant, ip_configuration_string_from_cluster  
  
 [sys.dm_tcp_listener_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-tcp-listener-states-transact-sql)  
 Retorna uma linha que contém informações de estado dinâmico para cada ouvinte de TCP.  
  
 **Nomes de colunas:** listener_id, ip_address, is_ipv4, port, type, type_desc, state, state_desc, start_time  
  
> [!NOTE]  
>  Para obter mais informações sobre como usar o [!INCLUDE[tsql](../../../includes/tsql-md.md)] para monitorar seu ambiente do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] , veja [Monitorar grupos de disponibilidade &#40;Transact-SQL&#41;](monitor-availability-groups-transact-sql.md).  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [Remover um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](remove-an-availability-group-listener-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Ouvintes do grupo de disponibilidade, conectividade de cliente e failover de aplicativo &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)   
 [Monitorar grupos de disponibilidade &#40;Transact-SQL&#41;](monitor-availability-groups-transact-sql.md)  
  
  
