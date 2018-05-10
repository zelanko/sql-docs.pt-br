---
title: M (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- M (geography Data Type)
- M_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- M method
ms.assetid: cdba04f0-4e17-48f6-bafb-b1f918c5a501
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f74b83dbfda4b9896009e1dde99e7786b8357766
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="m-geography-data-type"></a>M (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  O valor **M** (medida) da instância de **geography**. As semânticas do valor de medida são definidas pelo usuário mas, geralmente, descrevem a distância ao longo de um linestring. Por exemplo, o valor de medida poderia ser usado para monitorar as placas de quilometragem ao longo de uma estrada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.M  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **float**  
  
 Tipo do CLR: **SqlDouble**  
  
## <a name="remarks"></a>Remarks  
 O valor dessa propriedade será nulo se a instância de **geography** não for um **Point** e também será nulo para as instâncias de **Point** para as quais ele não for definido.  
  
 Esta propriedade é somente leitura.  
  
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
  
  
