---
title: Reduce (tipo de dados geography)
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Reduce_TSQL
- Reduce
dev_langs:
- TSQL
helpviewer_keywords:
- Reduce method
ms.assetid: c5dfa8c1-6764-41d8-9150-f3cb30633d3e
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: e0745bbe895fcc26aceb197c9779f44249825083
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86556141"
---
# <a name="reduce-geography-data-type-"></a>Reduce (tipo de dados geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna uma aproximação da instância de **geography** fornecida produzida pela execução do algoritmo de Douglas-Peucker na instância com a tolerância indicada.  
  
 Esse método de tipo de dados de **geography** é compatível com instâncias **FullGlobe** ou instâncias espaciais maiores que um hemisfério.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.Reduce ( tolerance )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos

|Termo|Definição|
|----|----------|
|*tolerance*|É um valor do tipo **float**. *tolerance* é a tolerância de entrada para o algoritmo de Douglas-Peucker. *tolerance* precisa ser um número positivo.|  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de retorno do CLR: **SqlGeography**  
  
## <a name="remarks"></a>Comentários  
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
  
  
