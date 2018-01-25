---
title: "HasM (DataType Geométrico) | Microsoft Docs"
ms.custom: 
ms.date: 05/05/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords: HasM geometry
ms.assetid: 15540837-c4bf-4d18-b380-13ae31f3226f
caps.latest.revision: "6"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cb449a098a60e253204b4d37e5dc22fd05c8f50b
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="hasm-geometry-datatype"></a>HasM (DataType geométrico)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Retorna 1 (true) se pelo menos um objeto espacial contiver pelo menos um valor M; caso contrário, retorna 0 (false).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.HasM  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **bits**  
  
 Tipo de retorno CLR: **booliano**  
  
## <a name="remarks"></a>Remarks  
  
## <a name="examples"></a>Exemplos  
  
```sql  
DECLARE @p GEOMETRY = 'Point(1 1 1 1)'  
SELECT @p.HasM   
--Returns: 1 (true)  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos estendidos em instâncias de geometria](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [M &#40; tipo de dados geometry &#41;](../../t-sql/spatial-geometry/m-geometry-data-type.md)  
  
  
