---
title: MSSQLSERVER_1461 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 1461 (Database Engine error)
ms.assetid: fce10907-4753-441b-b624-f28e00ed7520
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 47dcf5e0a055e6decd359ffc9479387194776428
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver1461"></a>MSSQLSERVER_1461
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|1461|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBM_SAFETY_MISMATCH|  
|Texto da mensagem|Foram detectados níveis de segurança diferentes no espelhamento de banco de dados entre servidores para o banco de dados "%.*ls". O nível de segurança FULL será usado.|  
  
## <a name="explanation"></a>Explicação  
As conexões de espelhamento foram perdidas quando o nível de segurança da transação foi modificado porque as configurações de segurança da transação eram inconsistentes nos bancos de dados principal e espelho. A configuração de segurança padrão da segurança da transação completa será usada. A sessão será executada em modo de segurança alta.  
  
## <a name="user-action"></a>Ação do usuário  
Para desativar a segurança da transação, execute novamente a instrução ALTER DATABASE *database_name* SET PARTNER SAFETY OFF no banco de dados de entidade.  
  
