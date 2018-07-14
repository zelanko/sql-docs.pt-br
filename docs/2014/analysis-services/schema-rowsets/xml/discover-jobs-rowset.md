---
title: Conjunto de linhas DISCOVER_JOBS | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- DISCOVER_JOBS rowset
ms.assetid: b4d83bb6-aed3-4513-b516-cefadf95dad2
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6a23a3e3dae0a03bf31a7b73b8cb505e834cff27
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37246056"
---
# <a name="discoverjobs-rowset"></a>Conjunto de linhas DISCOVER_JOBS
  Oferece informações sobre os trabalhos ativos em execução no servidor. O trabalho é uma parte do comando que executa uma tarefa específica em nome desse comando.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O `DISCOVER_JOBS` linhas contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|`JOB_CREATION_TIME`|`DBTYPE_DBTIMESTAMP`||A data e a hora do servidor UTC em que o trabalho foi criado.|  
|`JOB_DESCRIPTION`|`DBTYPE_WSTR`||A descrição do trabalho atribuída pelo serviço do servidor.|  
|`JOB_EXECUTION_TIME_MS`|`DBTYPE_I8`||A hora, em milissegundos, em que o trabalho está ativo.|  
|`JOB_ID`|`DBTYPE_I4`||O identificador exclusivo do trabalho.|  
|`JOB_START_TIME`|`DBTYPE_DBTIMESTAMP`||A data e a hora do servidor UTC em que o trabalho foi iniciado.|  
|`JOB_THREADPOOL_ID`|`DBTYPE_I4`||O pool de threads do qual o trabalho atual foi iniciado.|  
|`JOB_TOTAL_TIME_MS`|`DBTYPE_I8`||A hora, em milissegundos, desde o início do trabalho.|  
|`SPID`|`DBTYPE_I4`||A ID da sessão.|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas `DISCOVER_JOBS` pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|SPID|DBTYPE_I4|Opcional.|  
|JOB_ID|DBTYPE_I4|Opcional.|  
|JOB_DESCRIPTION|DBTYPE_WSTR|Opcional.|  
|JOB_THREADPOOL_ID|DBTYPE_I4|Opcional.|  
|JOB_MIN TOTAL_TIME_MS|DBTYPE_I8|Opcional.|  
  
## <a name="see-also"></a>Consulte também  
 [Conjunto de linhas de esquema do XML](xml-for-analysis-schema-rowsets.md)  
  
  
