---
title: Recuperar-se de uma falha na instância do cluster de failover | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- clusters [SQL Server], recovery from failure
- failover clustering [SQL Server], recovery from failure
- hardware failures [SQL Server]
- recovering failover cluster failures [SQL Server]
ms.assetid: 3d151d0c-e841-4325-8606-c094de37d7d1
caps.latest.revision: 30
author: rothja
ms.author: jroth
manager: jhubbard
ms.openlocfilehash: 41c6bb87ad53000ebd7e24e38beb641b4dc54c3d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36121636"
---
# <a name="recover-from-failover-cluster-instance-failure"></a>Recuperar-se de uma falha na instância do cluster de failover
  Este tópico descreve como se recuperar de falhas de cluster usando o snap-in Gerenciador de Cluster de Failover após a ocorrência de um failover no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. O snap-in Gerenciador de Cluster de Failover é o aplicativo de gerenciamento de cluster do serviço WSFC (Windows Server Failover Clustering).  
  
-   [Recuperar de uma falha irreparável](#Scenario1)  
  
-   [Recuperar de uma falha de software](#Scenario2)  
  
##  <a name="Scenario1"></a> Recuperar de uma falha irreparável  
 Use as seguintes etapas para recuperar-se de uma falha irreparável. A falha pode ser causada, por exemplo, por uma falha em um controlador de disco ou no sistema operacional. Nesse caso, a falha é gerada por um problema de hardware no Nó 1 de um cluster de dois nós.  
  
1.  Após a falha no Nó 1, a FCI do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] executa failover no Nó 2.  
  
2.  Remova o Nó 1 da FCI. Para fazer isso, do Nó 2, abra o snap-in Gerenciador de Cluster de Failover, clique com o botão direito do mouse no Nó 1, clique em **Mover Ações**e em **Remover Nó**.  
  
3.  Verifique se o Nó 1 foi removido da definição de cluster.  
  
4.  Instale o novo hardware que substituirá o hardware com falha no Nó 1.  
  
5.  Usando o snap-in Gerenciador de Cluster de Failover, adicione o Nó 1 ao cluster existente. Para obter mais informações sobre como configurar o MS DTC, consulte [Antes de instalar o clustering de failover](../install/before-installing-failover-clustering.md).  
  
6.  Verifique se as contas de administradoras são as mesmas em todos os nós do cluster.  
  
7.  Execute a Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para adicionar o Nó 1 à FCI. Para obter mais informações, consulte [Adicionar ou remover nós em um cluster de failover do SQL Server &#40;Instalação&#41;](../install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md).  
  
##  <a name="Scenario2"></a> Recuperar-se de uma falha reparável  
 Execute as seguintes etapas ara recuperar-se de uma falha reparável. Nesse caso, a falha é causada porque o Nó 1 está desativado ou offline, mas não irreparavelmente danificado. Ela pode ser causada por uma falha do sistema operacional, falha de hardware ou falha na própria instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
1.  Após a falha no Nó 1, a FCI executa failover no Nó 2.  
  
2.  Resolva o problema no Nó 1.  
  
3.  Verifique se todos os nós estão online e se o serviço WSFC está funcionando.  
  
4.  Execute failover no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no nó recuperado.  
  
  