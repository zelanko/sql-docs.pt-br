---
title: Suporte de alta disponibilidade | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 2e0f6d3f-0536-46d9-8630-835e199515bf
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f9f38dcf89eaa5741edd537647553223c93ad5ae
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47771498"
---
# <a name="high-availability-support"></a>Suporte de alta disponibilidade
  O Serviço CDC para Oracle é criado para alta disponibilidade. Os recursos a seguir fornecem parte do suporte de alta disponibilidade:  
  
-   O Serviço CDC para Oracle não usa nenhum recurso de arquivo (local ou não). Seu estado inteiro é armazenado na instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino. Isto facilita iniciar o serviço em um computador diferente que usa a mesma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se o computador em que o serviço é executado falhar. Para reduzir o tempo de recuperação, as transações Oracle longas ou de longa duração são mantidas em uma tabela de preparação no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de destino, impedindo a necessidade para reexaminar muitos logs de transação do Oracle após uma falha (ou reinicialização do serviço).  
  
-   O Serviço CDC para Oracle pode usar instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] clusterizadas para que possa se recuperar depois que a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realizar failover para outro nó de cluster. O Administrador do computador do Serviço Oracle CDC somente precisa especificar as informações de conexão para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] clusterizada ao criar um Serviço Oracle CDC.  
  
-   O Serviço CDC para Oracle pode usar o recurso de espelhamento de banco de dados [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]**Always On** . Este suporte exige que o MSXDBCDC e todos os bancos de dados CDC estejam no mesmo grupo de disponibilidade. Ele também exige que o Administrador de Computador do Serviço Oracle CDC especifique as informações de conexão do **Always On** apropriadas para o grupo de disponibilidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (por exemplo, as propriedades de conexão `Failover_Partner and Network=dbmssocn`). Isso permite que o serviço CDC retome automaticamente o processamento em uma replicação secundária dos bancos de dados após um failover.  
  
-   O Serviço CDC para Oracle pode ser configurado como um recurso de serviço genérico em um cluster de failover do Windows (junto com, ou separado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]), simplificando o failover e revertendo o processamento do CDC com o cluster. Para configurar o Serviço CDC para Oracle como um recurso em um cluster de failover, o administrador do sistema deve definir o Serviço CDC para Oracle como um Recurso de Serviço Genérico em cada nó no cluster de failover.  
  
-   O Serviço CDC para Oracle dá suporte ao Oracle RAC, que permite que ele se comunique com o banco de dados Oracle e processe logs mesmo quando um dos nós do Oracle RAC falhar.  
  
  
