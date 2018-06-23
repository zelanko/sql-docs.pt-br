---
title: MSSQLSERVER_10001 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 10001 (Database Engine error)
ms.assetid: f8fd2d8d-a4af-4b6a-ba51-9123b7e4c9bf
caps.latest.revision: 16
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 08bbafd03c8db19e605dca8e985d351cfc4dbf0b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117225"
---
# <a name="mssqlserver10001"></a>MSSQLSERVER_10001
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|10001|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|HR_E_UNEXPECTED|  
|Texto da mensagem|O provedor reportou uma falha catastrófica inesperada.|  
  
## <a name="explanation"></a>Explicação  
 O processamento de consulta distribuído encontrou um erro genérico ao chamar no provedor OLE DB.  
  
## <a name="user-action"></a>Ação do usuário  
 Colete eventos de rastreamento OLE DB usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] e forneça esses dados ao suporte ao produto do provedor OLE DB.  
  
## <a name="see-also"></a>Consulte também  
 [Modelos e permissões do SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  