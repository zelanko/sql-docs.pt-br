---
title: "Consultar dados espaciais do vizinho mais próximo | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-spatial
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7af4ad5d-484e-45b4-aa16-83c33b358bb6
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8cac116f89d0cf1fde83a00dfd42c02e1fc5e2f0
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="query-spatial-data-for-nearest-neighbor"></a>Consultar dados espaciais de vizinho mais próximo
  Uma consulta comum usada com dados espaciais é a consulta de Vizinho Mais Próximo. As consultas de Vizinho Mais Próximo são usadas para localizar os objetos espaciais mais próximos a um objeto espacial específico. Por exemplo, um localizador de lojas para um site geralmente deve localizar os locais de loja mais próximos ao local de um cliente.  
  
 Uma consulta de Vizinho Mais Próximo pode ser escrita em uma variedade de formatos de consulta válidos, mas, para que a consulta de Vizinho Mais Próximo use um índice espacial, a sintaxe a seguir deve ser usada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
SELECT TOP ( number )  
        [ WITH TIES ]  
        [ * | expression ]   
        [, ...]  
    FROM spatial_table_reference, ...   
        [ WITH   
            (   
                [ INDEX ( index_ref ) ]   
                [ , SPATIAL_WINDOW_MAX_CELLS = <value>]   
                [ ,... ]   
            )   
        ]  
    WHERE   
        column_ref.STDistance ( @spatial_ object )   
            {   
                [ IS NOT NULL ] | [ < const ] | [ > const ]   
                | [ <= const ] | [ >= const ] | [ <> const ] ]   
            }  
            [ AND { other_predicate } ]   
    }  
    ORDER BY column_ref.STDistance ( @spatial_ object ) [ ,...n ]  
[ ; ]  
  
```  
  
## <a name="nearest-neighbor-query-and-spatial-indexes"></a>Consulta de Vizinho Mais Próximo e índices espaciais  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], as cláusulas **TOP** e **ORDER BY** são usadas para realizar uma consulta de Vizinho Mais Próximo em colunas de dados espaciais. A cláusula **ORDER BY** contém uma chamada ao método `STDistance()` para o tipo de dados de coluna espacial. A cláusula **TOP** indica o número de objetos a ser retornado para a consulta.  
  
 Os requisitos a seguir devem ser satisfeitos para uma consulta de Vizinho Mais Próximo para usar um índice espacial:  
  
1.  Um índice espacial deve estar presente em uma das colunas espaciais e o método `STDistance()` deve usar essa coluna nas cláusulas **WHERE** e **ORDER BY** .  
  
2.  A cláusula **TOP** não pode conter uma instrução **PERCENT** .  
  
3.  A cláusula **WHERE** deve conter um método `STDistance()` .  
  
4.  Se houver vários predicados na cláusula **WHERE** , o predicado que contém o método `STDistance()` deverá ser conectado por uma conjunção **AND** aos outros predicados. O método `STDistance()` não pode estar em uma parte opcional da cláusula **WHERE** .  
  
5.  A primeira expressão na cláusula **ORDER BY** deve usar o método `STDistance()` .  
  
6.  A ordem de classificação para a primeira expressão `STDistance()` na cláusula **ORDER BY** deve ser **ASC**.  
  
7.  Todas as linhas para as quais `STDistance` retorna **NULL** devem ser filtradas.  
  
> [!WARNING]  
>  Os métodos que usam **geography** ou tipos de dados **geometry** como argumentos retornarão **NULL** se as SRIDs não forem as mesmas dos tipos.  
  
 É recomendado que os novos mosaicos de índice espaciais sejam usados para índices usados em consultas de Vizinhos Mais Próximos. Para obter mais informações sobre mosaicos de índice espacial, veja [Dados espaciais &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir mostra para uma consulta de Vizinho Mais Próximo que pode usar um índice espacial. O exemplo usa a tabela `Person.Address` no banco de dados `AdventureWorks2012` .  
  
```tsql  
USE AdventureWorks2012  
GO  
DECLARE @g geography = 'POINT(-121.626 47.8315)';  
SELECT TOP(7) SpatialLocation.ToString(), City FROM Person.Address  
WHERE SpatialLocation.STDistance(@g) IS NOT NULL  
ORDER BY SpatialLocation.STDistance(@g);  
  
```  
  
 Crie um índice espacial na coluna SpatialLocation para ver como uma consulta de Vizinho Mais Próximo usa um índice espacial. Para obter mais informações sobre como criar índices espaciais, consulte [Create, Modify, and Drop Spatial Indexes](../../relational-databases/spatial/create-modify-and-drop-spatial-indexes.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir mostra para uma consulta de Vizinho Mais Próximo que não pode usar um índice espacial.  
  
```tsql  
USE AdventureWorks2012  
GO  
DECLARE @g geography = 'POINT(-121.626 47.8315)';  
SELECT TOP(7) SpatialLocation.ToString(), City FROM Person.Address  
ORDER BY SpatialLocation.STDistance(@g);  
  
```  
  
 A consulta não tem uma cláusula **WHERE** que usa `STDistance()` em uma forma especificada na seção de sintaxe; portanto, a consulta não pode usar um índice espacial.  
  
## <a name="see-also"></a>Consulte também  
 [Dados espaciais &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  

