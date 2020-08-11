---
title: Remover instância de cluster de failover
description: Use este procedimento para desinstalar uma instância de cluster de failover do SQL Server. Este artigo inclui considerações importantes para você fazer antes de continuar.
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- clusters [SQL Server], removing failover clustered instance
- failover clustering [SQL Server], removing failover clustered instance
- uninstalling failover clustered instances
- removing failover clustered instances
ms.assetid: bf63353b-69cf-4c5c-98ea-7b151e36537f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: dba18abbd7eb5938b7f2fa4d0c3caff8d5d6f567
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85897675"
---
# <a name="remove-a-sql-server-failover-cluster-instance-setup"></a>Remover uma instância de cluster de failover do SQL Server (instalação)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Use esse procedimento para desinstalar uma instância clusterizada de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
> [!IMPORTANT]  
>  Para atualizar ou remover um cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , você deve ter privilégios de administrador local com permissão para efetuar logon como um serviço em todos os nós do cluster de failover.  
  
 **Antes de começar**  
  
 Considere os seguintes pontos importantes antes de desinstalar um cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
-   Se o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client for desinstalado por acidente, os recursos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não poderão ser iniciados. Para reinstalar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, execute o programa de instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para instalar os pré-requisitos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   Se você optar por desinstalar um cluster de failover que tenha mais de um recurso de cluster IP do SQL, deverá remover os recursos IP adicionais do SQL usando o administrador de cluster.  
  
 Para obter informações sobre a sintaxe de prompt de comando, veja [Instalar o SQL Server 2016 por meio do Prompt de Comando](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).  
  
### <a name="to-uninstall-a-ssnoversion-failover-cluster"></a>Para desinstalar um cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
1.  Para desinstalar um cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , use a função Remover Nó fornecida na instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para remover cada nó individualmente. Para obter mais informações, consulte [Adicionar ou remover nós em um cluster de failover do SQL Server &#40;Instalação&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir e ler arquivos de log da Instalação do SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
