---
title: Espelhamento de banco de dados e instâncias de cluster de failover do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- failover clustering [SQL Server], database mirroring
- database mirroring [SQL Server], failover
- high-availability mode [SQL Server]
ms.assetid: f1dd6a79-698b-4e31-b923-6bfc3ea0b617
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e7c3a3094309d2d1d32a840d4eee933555daa66a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62755576"
---
# <a name="database-mirroring-and-sql-server-failover-cluster-instances"></a>Espelhamento de banco de dados e instâncias de cluster de failover do SQL Server
  Um cluster de failover é uma combinação de um ou mais discos físicos em um grupo de clusters do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Cluster Service (MSCS), conhecido como um grupo de recursos, que são nós participantes do cluster. O grupo de recursos é configurado como uma instância clusterizada de failover que hospeda uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Uma instância clusterizada de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aparece na rede como se fosse um único computador, mas tem funções que fornecerão failover de um nó para outro se um nó se tornar disponível. Para obter mais informações, consulte [Instâncias do Cluster de Failover do AlwaysOn (SQL Server)](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md).  
  
 Os clusters de failover fornecem suporte de alta disponibilidade para toda uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , em contrapartida ao espelhamento de banco de dados, que fornece suporte de alta disponibilidade para um banco de dados individual. O espelhamento de banco de dados funciona entre clusters de failover e também entre um cluster de failover e um host não clusterizado.  
  
> [!NOTE]  
>  Para obter uma introdução ao espelhamento de banco de dados, consulte [Espelhamento de banco de dados &#40;SQL Server&#41;](database-mirroring-sql-server.md).  
  
## <a name="mirroring-and-clustering"></a>Espelhamento e clusterização  
 Em geral, quando o espelhamento é usado com clustering, o servidor principal e o servidor espelho residem em clusters, sendo que o servidor principal é executado na instância clusterizada de failover de um cluster e o servidor espelho é executado na instância clusterizada de failover de um cluster diferente. No entanto, você pode estabelecer uma sessão de espelhamento na qual um parceiro reside na instância clusterizada de failover e o outro reside em um computador separado não clusterizado.  
  
 Se um failover de cluster tornar um servidor principal temporariamente indisponível, as conexões de clientes serão desconectadas do banco de dados. Após a conclusão do failover de cluster, os clientes podem se reconectar ao servidor principal no mesmo cluster ou em outro cluster ou em um computador não clusterizado, dependendo do [modo operacional](database-mirroring-operating-modes.md). Portanto, quando você decide como configurar o espelhamento de banco de dados em um ambiente clusterizado, o modo operacional utilizado para o espelhamento é importante.  
  
### <a name="high-safety-mode-session-with-automatic-failover"></a>Sessão de modo de alta segurança com failover automático  
 Se você pretende espelhar um banco de dados no modo de alta segurança com failover automático, uma configuração de dois clusters é recomendável para os parceiros. Essa configuração fornece o máximo de disponibilidade. A testemunha ou pode residir em um terceiro cluster ou em um computador não clusterizado.  
  
 Se o nó executando o servidor principal atual falhar, o failover automático do banco de dados começará em alguns segundos, enquanto o cluster ainda estiver executando o failover para outro nó. A sessão de espelhamento de banco de dados executará o failover para o servidor espelho no outro cluster ou no computador não clusterizado, e o servidor espelho anterior se tornará o servidor principal. O novo servidor principal encaminha sua cópia do banco de dados o mais rápido possível e a coloca online como o banco de dados principal. Após a conclusão do failover de cluster, que geralmente leva alguns minutos, a instância clusterizada de failover que anteriormente era o servidor principal se torna o servidor espelho.  
  
 A ilustração a seguir mostra um failover automático entre clusters em uma sessão de espelhamento executada no modo de alta segurança com uma testemunha (que dá suporte ao failover automático).  
  
 ![Um failover em um cluster](../media/dbm-and-failover-clustering.gif "A failover on a cluster")  
  
 As três instâncias do servidor na sessão de espelhamento residem em três clusters distintos: **Cluster_A**, **Cluster_B**, e **Cluster_C**. Em cada cluster, uma instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executada como uma instância clusterizada de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Quando a sessão de espelhamento é iniciada, a instância clusterizada de failover no **Cluster_A** é o servidor principal, a instância clusterizada de failover no **Cluster_B** é o servidor espelho e a instância clusterizada de failover no **Cluster_C** é a testemunha na sessão de espelhamento. Por fim, o nó ativo no **Cluster_A** falhará, o que fará com que o servidor principal fique indisponível.  
  
 Antes de o cluster ter tempo para o failover, a perda do servidor principal será detectada pelo servidor espelho, com a ajuda da testemunha. O servidor espelho encaminha seu banco de dados principal e o coloca online como o novo banco de dados de entidade o mais rápido possível. Quando o **Cluster_A** conclui o failover, o servidor principal anterior agora é o servidor espelho e sincroniza seu banco de dados com o banco de dados principal de entidade atual no **Cluster_B**.  
  
### <a name="high-safety-mode-session-without-automatic-failover"></a>Sessão de modo de alta segurança sem failover automático  
 Se você estiver espelhando um banco de dados no modo de alta segurança sem failover automático, outro nó no cluster atuará como o servidor principal se o nó executando o servidor principal atual falhar. Observe que enquanto o cluster está indisponível, o banco de dados está indisponível.  
  
### <a name="high-performance-mode-session"></a>Sessão de modo de alto desempenho  
 Se você pretende espelhar um banco de dados no modo de alto desempenho, considere colocar o servidor principal na instância clusterizada de failover de um cluster e colocar o servidor espelho em um servidor não clusterizado em um local remoto. Se o cluster executar o failover para outro nó, a instância clusterizada de failover continuará como o servidor principal na sessão de espelhamento. Se todo o cluster tiver problemas, você poderá forçar serviço no servidor espelho.  
  
 **Para configurar um novo cluster de failover do SQL Server**  
  
-   [Criar um novo cluster de failover do SQL Server &#40;Instalação&#41;](../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)  
  
 **Para configurar o espelhamento de banco de dados**  
  
-   [Configurando o espelhamento de banco de dados &#40;SQL Server&#41;](setting-up-database-mirroring-sql-server.md)  
  
-   [Estabelecer uma sessão de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)  
  
## <a name="see-also"></a>Consulte também  
 [Espelhamento de banco de dados &#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [Modos de operação de espelhamento de banco de dados](database-mirroring-operating-modes.md)   
 [Instâncias de Cluster de Failover do AlwaysOn (SQL Server)](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md) 
  
  
