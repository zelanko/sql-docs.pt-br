---
title: EnvelopeAggregate (tipo de dados geography) | Microsoft Docs
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- EnvelopeAggregate_TSQL
- EnvelopeAggregate
dev_langs:
- TSQL
helpviewer_keywords:
- EnvelopeAggregate method (geography)
ms.assetid: 4947797f-edb8-490f-beca-37df9ec06954
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e9d50e15f644a5662af2eead65d29447af8493a9
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="envelopeaggregate-geography-data-type"></a>EnvelopeAggregate (tipo de dados de geografia)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Retorna um objeto delimitador para um determinado conjunto de **geografia** objetos. Resultante **geografia** objeto contém vários segmentos de arco circular.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
EnvelopeAggregate ( geography_operand )  
```  
  
## <a name="arguments"></a>Argumentos  
 *geography_operand*  
 É um **geografia** coluna de tipo de tabela que contém o conjunto de **geografia** objetos na qual executar o envelope de um operação de agregação.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geografia**  
  
## <a name="remarks"></a>Comentários  
 Um **FullGlobe** objeto é retornado quando o objeto delimitador resultante é maior do que um hemisfério. Esse método não é preciso.  
  
 Método retornará **nulo** se a entrada tiver SRIDs diferentes. Consulte [Spatial Reference Identifiers &#40; SRIDs &#41; ](../../relational-databases/spatial/spatial-reference-identifiers-srids.md).  
  
 Método ignora **nulo** entradas.  
  
> [!NOTE]  
>  Método retornará **nulo** se todos os valores inseridos forem **nulo**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir executa um `EnvelopeAggregate` em um conjunto de **geografia** pontos local dentro de uma cidade.  
  
 ```
 USE AdventureWorks2012  
 GO  
 SELECT City,  
 geography::EnvelopeAggregate(SpatialLocation) AS SpatialLocation  
 FROM Person.Address  
 WHERE PostalCode LIKE('981%')  
 GROUP BY City;
 ```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos de Geografia estática estendidos](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  

