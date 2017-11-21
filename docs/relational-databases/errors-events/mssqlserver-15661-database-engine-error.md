---
title: MSSQLSERVER_15661 | Microsoft Docs
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
- 15661 (Database Engine error)
ms.assetid: 88b01bfb-74ce-4aa0-aec0-7885261c7ef3
caps.latest.revision: 11
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 93bd2efde15065f2d7285912a72a10a7ba77d817
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver15661"></a>MSSQLSERVER_15661
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|15661|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SQLErrorNum15661|  
|Texto da mensagem|O procedimento armazenado sp_estimate_data_compression_savings não pode ser usado para tabelas temporárias.|  
  
## <a name="explanation"></a>Explicação  
Uma tabela temporária foi usada como um argumento para o procedimento armazenado sp_estimate_data_compression_savings. Embora a compactação de tabelas temporárias tenha suporte, não é possível usar sp_estimate_data_compression_savings para calcular as economias de compactação.  
  
## <a name="user-action"></a>Ação do usuário  
Remova a tabela temporária como um argumento para sp_estimate_data_compression_savings.  
  

