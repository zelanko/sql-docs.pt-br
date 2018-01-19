---
title: Z (tipo de dados geography) | Microsoft Docs
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
f1_keywords:
- Z (geography Data Type)
- Z_(geography_Data_Type)_TSQL
dev_langs: TSQL
helpviewer_keywords: Z method
ms.assetid: 9abc79c5-43c9-4cc2-b37f-d2ecdec7c234
caps.latest.revision: "15"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: af88586a78cf9d77c21566f9ee1dd60a62be1f11
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="z-geography-data-type"></a>Z (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  O valor Z (elevação) da instância. A semântica do valor de elevação é definida pelo usuário.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.Z  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo: **float**  
  
 Tipo CLR: **SqlDouble**  
  
## <a name="remarks"></a>Remarks  
 O valor dessa propriedade é null se o **geografia** instância não é um ponto para qualquer **ponto** instância para que ele não está definido.  
  
 Esta propriedade é somente leitura.  
  
 As coordenadas Z não são usadas nos cálculos feitos pela biblioteca e não serão executadas em nenhum cálculo de biblioteca.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância `Point` com valores Z (elevação) e M (medida) e usa `Z` para buscar o valor Z da instância.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100 10.3 12)', 4326);  
SELECT @g.Z;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos estendidos em instâncias de Geografia](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [M &#40; tipo de dados geography &#41;](../../t-sql/spatial-geography/m-geography-data-type.md)   
 [AsTextZM &#40;tipo de dados geography&#41;](../../t-sql/spatial-geography/astextzm-geography-data-type.md)  
  
  
