---
title: Suporte de alta disponibilidade | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 2e0f6d3f-0536-46d9-8630-835e199515bf
caps.latest.revision: 4
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1ebf240434df77c1f860e31952f12ec3eb0d13a2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37271322"
---
# <a name="high-availability-support"></a>Suporte de alta disponibilidade
  O Serviço CDC para Oracle é criado para alta disponibilidade. Os recursos a seguir fornecem parte do suporte de alta disponibilidade:  
  
-   O Serviço CDC para Oracle não usa nenhum recurso de arquivo (local ou não). Seu estado inteiro é armazenado na instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino. Isto facilita iniciar o serviço em um computador diferente que usa a mesma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se o computador em que o serviço é executado falhar. Para reduzir o tempo de recuperação, as transações Oracle longas ou de longa duração são mantidas em uma tabela de preparação no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de destino, impedindo a necessidade para reexaminar muitos logs de transação do Oracle após uma falha (ou reinicialização do serviço).  
  
-   O Serviço CDC para Oracle pode usar instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] clusterizadas para que possa se recuperar depois que a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realizar failover para outro nó de cluster. O Administrador do computador do Serviço Oracle CDC somente precisa especificar as informações de conexão para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] clusterizada ao criar um Serviço Oracle CDC.  
  
-   O serviço CDC para Oracle pode usar o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] **AlwaysOn** recurso de espelhamento de banco de dados. Este suporte exige que o MSXDBCDC e todos os bancos de dados CDC estejam no mesmo grupo de disponibilidade. Ele também requer que o administrador de computador de serviço Oracle CDC para especificar a devida **AlwaysOn** informações de conexão para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] grupo de disponibilidade (por exemplo, as propriedades de conexão `Failover_Partner and Network=dbmssocn`). Isso permite que o serviço CDC retome automaticamente o processamento em uma replicação secundária dos bancos de dados após um failover.  
  
-   O Serviço CDC para Oracle pode ser configurado como um recurso de serviço genérico em um cluster de failover do Windows (junto com, ou separado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]), simplificando o failover e revertendo o processamento do CDC com o cluster. Para configurar o Serviço CDC para Oracle como um recurso em um cluster de failover, o administrador do sistema deve definir o Serviço CDC para Oracle como um Recurso de Serviço Genérico em cada nó no cluster de failover.  
  
-   O Serviço CDC para Oracle dá suporte ao Oracle RAC, que permite que ele se comunique com o banco de dados Oracle e processe logs mesmo quando um dos nós do Oracle RAC falhar.  
  
  
