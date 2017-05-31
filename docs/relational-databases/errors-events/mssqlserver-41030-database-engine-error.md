---
title: MSSQLSERVER_41030 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 41030 (Database Engine error)
ms.assetid: c85341ae-0fbf-42ae-9275-4cfe678238f0
caps.latest.revision: 6
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e246ec2e406f4bcfb9083875c7111421e967762c
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver41030"></a>MSSQLSERVER_41030
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|41030|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|OPEN_CLUSTER_SUB_KEY|  
|Texto da mensagem|Falha ao abrir a subchave do Registro '%.*ls' do Windows Server Failover Clustering (código de erro %d).  A chave pai é a chave raiz do cluster.  O serviço WSFC não pode estar em execução ou não pode estar acessível em seu estado atual; do contrário, os argumentos especificados não serão válidos. Se o grupo de disponibilidade correspondente foi removido, esse erro será provável. Para obter informações sobre esse código de erro, consulte "Códigos de erro do sistema" na documentação do Windows Development.|  
  
## <a name="explanation"></a>Explicação  
Se um cluster WSFC for destruído, ele removerá todas as chaves do Registro relacionadas a [!INCLUDE[ssHADR](../../includes/sshadr-md.md)].  
  
## <a name="user-action"></a>Ação do usuário  
Após recriar um cluster WSFC, desabilite e habilite novamente o AlwaysOn em cada nó de cluster no qual uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está habilitada para AlwaysOn. Você pode usar o Gerenciador de Configuração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para essa tarefa.  
  
## <a name="see-also"></a>Consulte também  
[Habilitar e desabilitar grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)  
[WSFC &#40;Windows Server Failover Clustering&#41; com o SQL Server](~/sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)  
  

