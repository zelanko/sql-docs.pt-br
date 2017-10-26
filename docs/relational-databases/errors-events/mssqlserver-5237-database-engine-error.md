---
title: MSSQLSERVER_5237 | Microsoft Docs
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
- 5237 (Database Engine error)
ms.assetid: 9ff28935-d1eb-47ee-99b3-1a65cb948ce7
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3aa478d036226af0d5a7565da8b4588f2cef83c1
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver5237"></a>MSSQLSERVER_5237
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|5237|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC4_INDEXED_VIEW_CHECK_QUERY_FAILED_NO_ERRORCODE|  
|Texto da mensagem|Falha na verificação entre conjuntos de linhas DBCC do objeto 'NAME' (ID de objeto O_ID) devido a um erro de consulta interno.|  
  
## <a name="explanation"></a>Explicação  
Um erro interno fez com que DBCC não conseguisse executar a consulta para verificar exibições indexadas.  
  
## <a name="user-action"></a>Ação do usuário  
Execute o comando DBCC novamente.  
  

