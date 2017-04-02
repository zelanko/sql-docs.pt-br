---
title: "Remover uma inst&#226;ncia de cluster de failover do SQL Server (instala&#231;&#227;o) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "clusters [SQL Server], removendo instância clusterizada de failover"
  - "clustering de failover [SQL Server], removendo instância clusterizada de failover"
  - "desinstalando instâncias clusterizadas de failover"
  - "removendo instâncias clusterizadas de failover"
ms.assetid: bf63353b-69cf-4c5c-98ea-7b151e36537f
caps.latest.revision: 38
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 38
---
# Remover uma inst&#226;ncia de cluster de failover do SQL Server (instala&#231;&#227;o)
  Use esse procedimento para desinstalar uma instância clusterizada de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Para atualizar ou remover um cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], você deve ter privilégios de administrador local com permissão para efetuar logon como um serviço em todos os nós do cluster de failover.  
  
 **Antes de começar**  
  
 Considere os seguintes pontos importantes antes de desinstalar um cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:  
  
-   Se o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client for desinstalado por acidente, os recursos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não poderão ser iniciados. Para reinstalar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, execute o programa de instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para instalar os pré-requisitos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Se você optar por desinstalar um cluster de failover que tenha mais de um recurso de cluster IP do SQL, deverá remover os recursos IP adicionais do SQL usando o administrador de cluster.  
  
 Para obter informações sobre a sintaxe de prompt de comando, veja [Instalar o SQL Server 2016 por meio do Prompt de Comando](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).  
  
### Para desinstalar um cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
1.  Para desinstalar um cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], use a função Remover Nó fornecida na instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para remover cada nó individualmente. Para obter mais informações, consulte [Adicionar ou remover nós em um cluster de failover do SQL Server &#40;Instalação&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md).  
  
## Consulte também  
 [Exibir e ler arquivos de log da Instalação do SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  