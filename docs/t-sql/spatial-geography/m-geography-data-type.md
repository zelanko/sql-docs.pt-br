---
description: M (tipo de dados geography)
title: M (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- M (geography Data Type)
- M_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- M method
ms.assetid: cdba04f0-4e17-48f6-bafb-b1f918c5a501
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 77a79972671854e7e8538de7b943545955f61e89
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88422420"
---
# <a name="m-geography-data-type"></a>M (tipo de dados geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  O valor **M** (medida) da instância de **geography**. As semânticas do valor de medida são definidas pelo usuário mas, geralmente, descrevem a distância ao longo de um linestring. Por exemplo, o valor de medida poderia ser usado para monitorar as placas de quilometragem ao longo de uma estrada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.M  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de retorno
 Tipo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **float**  
  
 Tipo CLR: **SqlDouble**  
  
## <a name="remarks"></a>Comentários  
 O valor dessa propriedade será nulo se a instância de **geography** não for um **Point** e também será nulo para as instâncias de **Point** para as quais ele não for definido.  
  
 Esta propriedade é somente para leitura.  
  
 Os valores de M não são usados nos cálculos feitos pela biblioteca e não serão usados em nenhum cálculo de biblioteca.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância `Point` com valores Z (elevação) e M (medida) e usa `M` para buscar o valor `M` da instância.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100 10.3 12)', 4326);  
SELECT @g.M;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos estendidos em instâncias de geografia](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [Z &#40;Tipo de dados de geografia&#41;](../../t-sql/spatial-geography/z-geography-data-type.md)  
  
  
