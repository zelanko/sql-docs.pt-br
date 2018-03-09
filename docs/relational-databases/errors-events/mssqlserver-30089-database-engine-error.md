---
title: MSSQLSERVER_30089 | Microsoft Docs
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
- 9992 (Database Engine error)
ms.assetid: 188e5bde-6865-4740-a2b2-582be8f55c77
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 256f5841b7cf3b5c6045ea81133bdcc37e5e3c46
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver30089"></a>MSSQLSERVER_30089
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|30089|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|IFTS_FDHOST_TERMINATEDABNORMAL|  
|Texto da mensagem|O processo FDHost (host do daemon de filtro de texto completo) foi interrompido de maneira anormal. Isso poderá ocorrer se um componente linguístico configurado incorretamente ou que não está funcionando bem, como um separador de palavras, lematizador ou filtro, gerou um erro irrecuperável durante a indexação de texto completo ou no processamento de uma consulta. O processo será reiniciado automaticamente.|  
  
## <a name="explanation"></a>Explicação  
O host do daemon de filtro de texto completo encontrou um problema que forçou seu encerramento de maneira anormal. A causa do problema pode ser um documento malformatado, um bug no filtro ou no separador de palavras ou um problema no daemon de filtro.  
  
## <a name="user-action"></a>Ação do usuário  
Normalmente, o daemon se recupera do erro. Se ele apresentar falhas constantes, será necessário diagnosticar e solucionar o problema. Tente fazer o seguinte para isolar o problema:  
  
1.  Se um novo componente linguístico foi instalado recentemente, remova-o do sistema.  
  
2.  Consulte o log de rastreamento para identificar qualquer documento novo cuja indexação de texto completo tenha falhado e remova esse documento.  
  
## <a name="see-also"></a>Consulte também  
[sp_help_fulltext_system_components &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md)  
[Configurar e gerenciar separadores de palavras e lematizadores de pesquisa](~/relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)  
[Configurar e gerenciar filtros de pesquisa](~/relational-databases/search/configure-and-manage-filters-for-search.md)  
  
