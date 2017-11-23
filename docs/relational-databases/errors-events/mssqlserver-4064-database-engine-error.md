---
title: MSSQLSERVER_4064 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 4064 (Database Engine error)
ms.assetid: 32112b90-0a2f-4834-a027-756811732be7
caps.latest.revision: "19"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8908c1075c0df7cb60d5e8b79c9d9067c03876ee
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver4064"></a>MSSQLSERVER_4064
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|4064|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DB_UFAIL_FATAL|  
|Texto da mensagem|Não é possível abrir o banco de dados padrão do usuário. Falha no logon.|  
  
## <a name="explanation"></a>Explicação  
O logon do SQL Server não pôde se conectar devido a um problema com o banco de dados padrão. O próprio banco de dados é inválido ou o logon não tem a permissão CONNECT no banco de dados.  
  
## <a name="user-action"></a>Ação do usuário  
Use ALTER LOGIN para alterar o banco de dados padrão do logon. Conceda a permissão CONNECT para o logon.  
  
