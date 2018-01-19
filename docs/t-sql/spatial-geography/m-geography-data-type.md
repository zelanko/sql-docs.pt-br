---
title: M (tipo de dados geography) | Microsoft Docs
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
- M (geography Data Type)
- M_TSQL
dev_langs: TSQL
helpviewer_keywords: M method
ms.assetid: cdba04f0-4e17-48f6-bafb-b1f918c5a501
caps.latest.revision: "14"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c4041419bb4e0dd0c662fa120a9c8c68d8c32286
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="m-geography-data-type"></a>M (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  O **M** (medida) valor da **geografia** instância. As semânticas do valor de medida são definidas pelo usuário mas, geralmente, descrevem a distância ao longo de um linestring. Por exemplo, o valor de medida poderia ser usado para monitorar as placas de quilometragem ao longo de uma estrada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.M  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo: **float**  
  
 Tipo CLR: **SqlDouble**  
  
## <a name="remarks"></a>Remarks  
 O valor dessa propriedade é null se o **geografia** instância não é um **ponto**, bem como para qualquer **ponto** instância para que ele não está definido.  
  
 Esta propriedade é somente leitura.  
  
 Os valores de M não são usados nos cálculos feitos pela biblioteca e não serão executados em qualquer cálculo de biblioteca.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância `Point` com valores Z (elevação) e M (medida) e usa `M` para buscar o valor `M` da instância.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100 10.3 12)', 4326);  
SELECT @g.M;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos estendidos em instâncias de Geografia](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [Z &#40; tipo de dados geography &#41;](../../t-sql/spatial-geography/z-geography-data-type.md)  
  
  
