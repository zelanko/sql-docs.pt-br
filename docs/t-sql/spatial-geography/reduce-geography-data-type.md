---
title: Reduce (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- Reduce_TSQL
- Reduce
dev_langs:
- TSQL
helpviewer_keywords:
- Reduce method
ms.assetid: c5dfa8c1-6764-41d8-9150-f3cb30633d3e
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7af59f67c332850128e2822bdd026b014f01055d
ms.sourcegitcommit: a6596c62f607041c4402f7d5b41a232fca257c14
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36255798"
---
# <a name="reduce-geography-data-type-"></a>Reduce (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna uma aproximação da instância de **geography** fornecida produzida pela execução do algoritmo de Douglas-Peucker na instância com a tolerância indicada.  
  
 Esse método de tipo de dados de **geography** é compatível com instâncias **FullGlobe** ou instâncias espaciais maiores que um hemisfério.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.Reduce ( tolerance )  
```  
  
## <a name="arguments"></a>Argumentos  
  
|||  
|-|-|  
|Termo|Definição|  
|*tolerance*|É um valor do tipo **float**. *tolerance* é a tolerância de entrada para o algoritmo de Douglas-Peucker. *tolerance* precisa ser um número positivo.|  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de retorno do CLR: **SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 Para tipos de coleção, esse algoritmo funciona de forma independente em cada **geografia** contida na instância. Esse algoritmo não modifica as instâncias de **Point**.  
  
 Esse método tentará preservar os pontos de extremidade das instâncias de **LineString**, mas talvez não consiga fazer isso para assegurar que o resultado seja válido.  
  
 Se `Reduce()` for chamado com um valor negativo, esse método gerará uma **ArgumentException**. As tolerâncias usadas em `Reduce()` devem ser números positivos.  
  
 O algoritmo de Douglas-Peucker funciona em cada curva ou anel na instância de **geography**, removendo todos os pontos, exceto o ponto inicial e o ponto de final. Cada ponto removido é adicionado novamente, começando com o ponto mais distante, até que nenhum ponto esteja a mais do que a *tolerância* do resultado. O resultado é então validado, se necessário, pois um resultado válido é garantido.  
  
 No [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], esse método foi estendido para as instâncias de **FullGlobe**.  
  
 Esse método não é preciso.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância `LineString` e usa `Reduce()` para simplificar a instância.  
  
```  
DECLARE @g geography = 'LineString(120 45, 120.1 45.1, 199.9 45.2, 120 46)'  
SELECT @g.Reduce(10000).ToString()  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos estendidos em instâncias geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
