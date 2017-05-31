---
title: "Resumo de recursos com controle de versão do PolyBase | Microsoft Docs"
ms.custom: 
ms.date: 04/13/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6591994d-6109-4285-9c5b-ecb355f8a111
caps.latest.revision: 10
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 2da0c759864e746414f8bf17388463c9a4bfdf88
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="polybase-versioned-feature-summary"></a>Resumo de recursos com controle de versão do PolyBase
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Resumo dos recursos do PolyBase disponíveis para serviços e produtos do SQL Server.  
  
## <a name="feature-summary-for-product-releases"></a>Resumo de recursos para versões do produto  
 Esta tabela resume os principais recursos para o PolyBase e os produtos nos quais eles estão disponíveis.  
  
### [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
 Esses recursos se aplicam ao [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] em execução local ou em uma máquina virtual do Azure.  O PolyBase não está disponível no SQL Server 2014 e em versões anteriores.  
  
|||  
|-|-|  
|**Recurso**|**Disponibilidade**|  
|Consultar dados do Hadoop com [!INCLUDE[tsql](../../includes/tsql-md.md)]|sim|  
|Consultar o armazenamento de blobs do Azure com [!INCLUDE[tsql](../../includes/tsql-md.md)]|sim|  
|Importar dados do Hadoop|sim|  
|Importar dados do armazenamento de blobs do Azure|Sim| 
|Importar dados do Azure Data Lake Store|não|   
|Exportar dados para o Hadoop|sim|  
|Exportar dados para o armazenamento de blobs do Azure|Sim|  
|Exportar dados do Azure Data Lake Store|não|
|Executar consultas do PolyBase nas ferramentas de BI da Microsoft|sim|  
|Enviar cálculos de consulta por push ao Hadoop|sim|  
  
### [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]  
 Esses recursos se aplicam ao [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
  
|||  
|-|-|  
|**Recurso**|**Disponibilidade**|  
|Consultar dados do Hadoop com [!INCLUDE[tsql](../../includes/tsql-md.md)]|não|  
|Consultar o armazenamento de blobs do Azure com [!INCLUDE[tsql](../../includes/tsql-md.md)]|sim|  
|Importar dados do Hadoop|não|  
|Importar dados do armazenamento de blobs do Azure|Sim|
|Importar dados do Azure Data Lake Store|Sim|     
|Exportar dados para o Hadoop|não|  
|Exportar dados para o armazenamento de blobs do Azure|Sim|  
|Exportar dados para o Azure Data Lake Store|Sim|
|Executar consultas do PolyBase nas ferramentas de BI da Microsoft|sim|  
|Enviar cálculos de consulta por push ao Hadoop|não|  
  
### [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Esses recursos se aplicam ao [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
|||  
|-|-|  
|**Recurso**|**Disponibilidade**|  
|Consultar dados do Hadoop com [!INCLUDE[tsql](../../includes/tsql-md.md)]|sim|  
|Consultar o armazenamento de blobs do Azure com [!INCLUDE[tsql](../../includes/tsql-md.md)]|sim|  
|Importar dados do Hadoop|sim|  
|Importar dados do armazenamento de blobs do Azure|Sim|  
|Importar dados do Azure Data Lake Store|não|   
|Exportar dados para o Hadoop|sim|  
|Exportar dados para o armazenamento de blobs do Azure|Sim|  
|Exportar dados para o Azure Data Lake Store|não|
|Executar consultas do PolyBase nas ferramentas de BI da Microsoft|sim|  
|Enviar cálculos de consulta por push ao Hadoop|sim|  
  
## <a name="see-also"></a>Consulte também  
 [Guia do PolyBase](../../relational-databases/polybase/polybase-guide.md)  
  
  

