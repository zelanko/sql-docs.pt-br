---
title: "Administra&#231;&#227;o e manuten&#231;&#227;o da inst&#226;ncia de cluster de failover | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "contas de usuário [SQL Server], clustering de failover"
  - "clusters [SQL Server], mantendo"
  - "nós [Clustering de Failover]"
  - "clustering de failover [SQL Server], mantendo"
  - "adicionando nós"
  - "servidores virtuais [SQL Server], removendo nós"
  - "instância clusterizada do SQL Server"
  - "nós [Clustering de Failover], removendo"
  - "nós [Clustering de Failover], adicionando"
  - "contas de serviço [SQL Server]"
  - "removendo nós"
  - "servidores virtuais [SQL Server], adicionando nós"
ms.assetid: 2d5c63e9-8061-45c3-94db-8dd3100b8a91
caps.latest.revision: 35
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 35
---
# Administra&#231;&#227;o e manuten&#231;&#227;o da inst&#226;ncia de cluster de failover
  Tarefas de manutenção como adicionar ou remover nós de uma FCI (instância de cluster de failover) AlwaysOn são realizadas usando o programa de instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Outras tarefas de administração como alterar o recurso de endereço IP e recuperar de certos cenários de FCI são realizadas com o uso do snap-in Gerenciador de Cluster de Failover, que é o snap-in de gerenciamento do serviço WSFC (Windows Server Failover Clustering).  
  
## Mantendo uma instância de cluster de failover  
 Depois que você instalar uma FCI, poderá alterá-la ou repará-la usando o programa de Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Por exemplo, você também pode adicionar mais nós a uma FCI, executar uma FCI como uma instância autônoma ou remover um nó de uma configuração de FCI.  
  
### Adicionando um nó a uma instância de cluster de failover existente  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] A Instalação lhe dá a opção de manter uma FCI existente. Se você escolher esta opção, poderá adicionar outros nós à sua FCI executando a Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no computador que você deseja adicionar à FCI. Para obter mais informações, consulte [Criar um novo cluster de failover do SQL Server &#40;instalação&#41;](../../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md) e [Adicionar ou remover nós em um cluster de failover do SQL Server &#40;instalação&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md).  
  
### Removendo um nó de uma instância de cluster de failover existente  
 Você pode remover um nó de uma FCI executando a Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no computador que deseja remover da FCI. Cada nó em uma FCI é considerado um par sem dependências nos outros nós no FCI e você poderá remover qualquer nó. Um nó danificado não tem que estar disponível para ser removido, e o processo de remoção não desinstalará os binários do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] do nó não disponível. Um nó removido poderá ser adicionado novamente a uma FCI a qualquer momento. Para obter mais informações, consulte [Adicionar ou remover nós em um cluster de failover do SQL Server &#40;Instalação&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md).  
  
### Alterando as contas de serviço  
 Você não deve alterar as senhas de nenhuma das contas de serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quando um nó de FCI estiver inativo ou offline. Se você tiver que fazer isso, deverá redefinir a senha novamente usando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager quando todos os nós estiverem novamente online.  
  
 Se a conta de serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não for uma conta de administrador no seu cluster, os compartilhamentos administrativos poderão ser excluídos em qualquer nó do cluster. Os compartilhamentos administrativos devem estar disponíveis em um cluster para que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] funcione.  
  
> [!IMPORTANT]  
>  Não use a mesma conta para a conta de serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e a conta de serviço do WSFC. Se a senha for alterada para a conta de serviço do WSFC, sua instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] falhará.  
  
 No [!INCLUDE[nextref_longhorn](../../../includes/nextref-longhorn-md.md)], os SIDs de serviço são usados para as contas de serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obter mais informações, veja [Configurar contas de serviço e permissões do Windows](../../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
## Administrando uma instância de cluster de failover  
  
|Descrição da tarefa|Link do tópico|  
|----------------------|----------------|  
|Descreve como adicionar dependências a um recurso do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|[Adicionar dependências a um recurso do SQL Server](../../../sql-server/failover-clusters/windows/add-dependencies-to-a-sql-server-resource.md)|  
|Kerberos é um protocolo de autenticação de rede cuja finalidade é oferecer autenticação forte para aplicativos cliente/servidor. O Kerberos proporciona uma base para interoperabilidade e ajuda a melhorar a segurança da autenticação na rede da empresa inteira. Você pode usar a autenticação Kerberos com instâncias autônomas do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou com FCIs AlwaysOn.|[Registrar um nome da entidade de serviço para conexões de Kerberos](../../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md).|  
|Fornece links para conteúdo que descreve como habilitar a autenticação Kerberos||  
|Descreve o procedimento usado para recuperar-se de uma falha de cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|[Recuperar-se de uma falha na instância do cluster de failover](../../../sql-server/failover-clusters/windows/recover-from-failover-cluster-instance-failure.md)|  
|Descreva o procedimento usado para alterar o recurso de endereço IP para uma instância de cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|[Alterar o endereço IP de uma instância do cluster de failover](../../../sql-server/failover-clusters/windows/change-the-ip-address-of-a-failover-cluster-instance.md)|  
  
## Consulte também  
 [Definir configurações da propriedade HealthCheckTimeout](../../../sql-server/failover-clusters/windows/configure-healthchecktimeout-property-settings.md)   
 [Definir as configurações da propriedade FailureConditionLevel](../../../sql-server/failover-clusters/windows/configure-failureconditionlevel-property-settings.md)   
 [Exibir e ler o log de diagnóstico da instância do cluster de failover](../../../sql-server/failover-clusters/windows/view-and-read-failover-cluster-instance-diagnostics-log.md)  
  
  