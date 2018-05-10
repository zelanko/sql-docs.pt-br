---
title: MSSQLSERVER_21871 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 21871 (Database Engine error)
ms.assetid: d3215378-9282-444f-a18b-00b96fd0133d
caps.latest.revision: 6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 076c9a6d93a3ffba45ae741a4724d7f6561fe688
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver21871"></a>MSSQLSERVER_21871
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|21871|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SQLErrorNum21871|  
|Texto da mensagem|O publicador %s do banco de dados %s não foi redirecionado.|  
  
## <a name="explanation"></a>Explicação  
**sp_validate_replica_hosts_as_publishers** verifica a tabela MSredirected_publishers no banco de dados de distribuição em busca de uma entrada para o publicador identificado e o banco de dados publicador.  **sp_validate_replica_hosts_as_publishers** retorna o erro 21871 quando nenhuma entrada é encontrada.  
  
## <a name="user-action"></a>Ação do usuário  
**sp_validate_replica_hosts_as_publishers** só é relevante para publicadores redirecionados. Se o banco de dados publicador for membro de um grupo de disponibilidade, use o procedimento armazenado **sp_redirect_publisher** para associar o publicador e o banco de dados publicador ao Nome do Ouvinte do Grupo de Disponibilidade do grupo de disponibilidade.  
  
