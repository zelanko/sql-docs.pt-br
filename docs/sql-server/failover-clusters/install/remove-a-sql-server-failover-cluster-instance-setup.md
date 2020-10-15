---
title: Remover instância de cluster de failover
description: Use esse procedimento para desinstalar uma instância de cluster de failover do Always On. Este artigo inclui considerações importantes para você fazer antes de continuar.
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: how-to
helpviewer_keywords:
- clusters [SQL Server], removing failover cluster instance
- failover clustering [SQL Server], removing failover cluster instance
- uninstalling failover cluster instances
- removing failover cluster instances
ms.assetid: bf63353b-69cf-4c5c-98ea-7b151e36537f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3b523b792889c21a0b1d00ea3ab3ea3ac6fbf2aa
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988380"
---
# <a name="remove-a-failover-cluster-instance-setup"></a>Remover uma instância de cluster de failover (instalação)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

Use esse procedimento para desinstalar uma instância de cluster de failover Always On do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Para atualizar ou remover um cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], você deve ter privilégios de administrador local com permissão para fazer logon como um serviço em todos os nós do cluster de failover do Windows Server.  
  
 **Antes de começar**  
  
 Considere os seguintes pontos importantes antes de desinstalar uma instância de cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:  
  
-   Se o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client for desinstalado por acidente, os recursos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não poderão ser iniciados. Para reinstalar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, execute o programa de instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para instalar os pré-requisitos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   Se você desinstalar um cluster de failover com mais de um recurso de cluster de IP do SQL, deverá remover os recursos de IP adicionais do SQL usando o Gerenciador de Cluster de Failover ou o PowerShell.  
  
 Para obter informações sobre a sintaxe de prompt de comando, veja [Instalar o SQL Server 2016 por meio do Prompt de Comando](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).  
  
### <a name="to-uninstall-a-ssnoversion-failover-cluster-instance"></a>Para desinstalar uma instância de cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]
  
1.  Para desinstalar um cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , use a função Remover Nó fornecida na instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para remover cada nó individualmente. Confira mais informações em [Adicionar ou remover nós em um cluster de failover do Always On &#40;Instalação&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir e ler arquivos de log da Instalação do SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
