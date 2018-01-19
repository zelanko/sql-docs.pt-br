---
title: Reduzir (tipo de dados geography) | Microsoft Docs
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
- Reduce_TSQL
- Reduce
dev_langs: TSQL
helpviewer_keywords: Reduce method
ms.assetid: c5dfa8c1-6764-41d8-9150-f3cb30633d3e
caps.latest.revision: "14"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e1932373b11b10724bbbb4e05863428012eb23eb
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="reduce-geography-data-type-"></a>Reduce (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna uma aproximação do determinado **geografia** instância produzido pela execução do algoritmo de Douglas-Peucker na instância com a tolerância especificada.  
  
 Isso **geografia** método dá suporte ao tipo de dados **FullGlobe** instâncias ou a instâncias espaciais maiores que um hemisfério.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.Reduce ( tolerance )  
```  
  
## <a name="arguments"></a>Argumentos  
  
|||  
|-|-|  
|Termo|Definição|  
|*tolerance*|É um valor do tipo **float**. *tolerância* é a tolerância de entrada para o algoritmo de Douglas-Peucker. *tolerância* deve ser um número positivo.|  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geografia**  
  
 Tipo de retorno CLR: **SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 Para tipos de coleção, esse algoritmo funciona independentemente em cada **geografia** contidos na instância. Esse algoritmo não modifica **ponto** instâncias.  
  
 Esse método tentará preservar os pontos de extremidade de **LineString** instâncias, mas pode falhar ao fazer isso para preservar um resultado válido.  
  
 Se `Reduce()` é chamado com um valor negativo, esse método gerará uma **ArgumentException**. As tolerâncias usadas em `Reduce()` devem ser números positivos.  
  
 O algoritmo de Douglas-Peucker funciona em cada curva ou anel no **geografia** instância, removendo todos os pontos, exceto o ponto inicial e o ponto de extremidade. Cada ponto removido é adicionado novamente, começando com o ponto mais externo, até que nenhum ponto seja mais de *tolerância* do resultado. O resultado é então validado, se necessário, pois um resultado válido é garantido.  
  
 Em [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], esse método foi estendido para **FullGlobe** instâncias.  
  
 Esse método não é preciso.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância `LineString` e usa `Reduce()` para simplificar a instância.  
  
```  
DECLARE @g geography = 'LineString(120 45, 120.1 45.1, 199.9 45.2, 120 46)'  
SELECT @g.Reduce(10000).ToString()  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos estendidos em instâncias geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
