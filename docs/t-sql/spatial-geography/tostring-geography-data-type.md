---
title: ToString (tipo de dados geography) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: ToString (geography Data Type)
dev_langs: TSQL
helpviewer_keywords: ToString method
ms.assetid: 045c12fa-8fc6-441a-9500-7021cb4ff13e
caps.latest.revision: "18"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5f69036b448772e102f05ba657aa15f73c86c5c5
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="tostring-geography-data-type"></a>ToString (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna a representação de texto do Open Geospatial Consortium (OGC) conhecido (WKT) de um **geografia** instância aumentada com qualquer valor Z (elevação) e m (medida) transportados pela instância.  
  
 Esses dados de Geografia digite método dá suporte a **FullGlobe** instâncias ou a instâncias espaciais maiores que um hemisfério.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.ToString ()  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **nvarchar (max)**  
  
 Tipo de retorno CLR: **SqlString**  
  
## <a name="remarks"></a>Remarks  
 Esse método retorna a cadeia de caracteres "Null" quando chamado em instâncias nulas. Em [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], o conjunto de resultados possíveis no servidor foi estendido para **FullGlobe** instâncias. Esse método retornará o mesmo valor que `AsTextZM()`.  
  
 Esse método não é preciso.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria um `LineString` instância e usa `ToString()` para retornar a descrição de texto da instância.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos estendidos em instâncias de Geografia](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [AsTextZM &#40;tipo de dados geography&#41;](../../t-sql/spatial-geography/astextzm-geography-data-type.md)  
  
  
