---
title: Z (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Z (geometry Data Type)
- Z_(geometry_Data_Type)_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Z (geometry Data Type)
ms.assetid: a62ed736-44df-4591-9109-ce90e1df9bd3
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 40afdb720e125899e8a4c3b7df942496b7d0ae44
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85762067"
---
# <a name="z-geometry-data-type"></a>Z (tipo de dados geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

O valor Z (elevação) da instância. A semântica do valor de elevação é definida pelo usuário.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.Z  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **float**  
  
 Tipo do CLR: **SqlDouble**  
  
## <a name="remarks"></a>Comentários  
 O valor dessa propriedade será nulo se a instância de geometria não for um ponto, como também para qualquer instância de **Point** para a qual ele não foi definido.  
  
 Essa propriedade é somente leitura.  
  
 As coordenadas Z não são usadas nos cálculos feitos pela biblioteca e não estão presentes em nenhum cálculo de biblioteca.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância `Point` com valores Z (elevação) e M (medida) e usa `Z` para buscar o valor Z da instância.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(1 2 3 4)', 0);  
SELECT @g.Z;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [M &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/m-geometry-data-type.md)   
 [AsTextZM &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/astextzm-geometry-data-type.md)   
 [Métodos estendidos em instâncias geometry](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

