---
title: Consultar dados espaciais do vizinho mais próximo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-spatial
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7af4ad5d-484e-45b4-aa16-83c33b358bb6
caps.latest.revision: 12
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 46d2c75b69d283d6122255ec9ac4a41c4ccdbc28
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120749"
---
# <a name="query-spatial-data-for-nearest-neighbor"></a>Consultar dados espaciais de vizinho mais próximo
  Uma consulta comum usada com dados espaciais é a consulta de Vizinho Mais Próximo. As consultas de Vizinho Mais Próximo são usadas para localizar os objetos espaciais mais próximos a um objeto espacial específico. Por exemplo, um localizador de lojas para um site geralmente deve localizar os locais de loja mais próximos ao local de um cliente.  
  
 Uma consulta de Vizinho Mais Próximo pode ser escrita em uma variedade de formatos de consulta válidos, mas, para que a consulta de Vizinho Mais Próximo use um índice espacial, a sintaxe a seguir deve ser usada.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
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
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], as cláusulas `TOP` e `ORDER BY` são usadas para realizar uma consulta de Vizinho Mais Próximo em colunas de dados espaciais. O `ORDER BY` cláusula contém uma chamada para o `STDistance()` método para o tipo de dados da coluna espacial. O `TOP` cláusula indica o número de objetos para retornar para a consulta.  
  
 Os requisitos a seguir devem ser satisfeitos para uma consulta de Vizinho Mais Próximo para usar um índice espacial:  
  
1.  Um índice espacial deve estar presente em uma das colunas espaciais e o método `STDistance()` deve usar essa coluna nas cláusulas `WHERE` e `ORDER BY`.  
  
2.  A cláusula `TOP` não pode conter uma instrução `PERCENT`.  
  
3.  A cláusula `WHERE` deve conter um método `STDistance()`.  
  
4.  Se houver vários predicados na cláusula `WHERE`, o predicado que contém o método `STDistance()` deve ser conectado por uma conjunção `AND` aos outros predicados. O `STDistance()` método não pode estar em uma parte opcional do `WHERE` cláusula.  
  
5.  A primeira expressão na cláusula `ORDER BY` deve usar o método `STDistance()`.  
  
6.  A ordem de classificação para a primeira expressão `STDistance()` na cláusula `ORDER BY` deve ser `ASC`.  
  
7.  Todas as linhas para as quais `STDistance` retorna `NULL` devem ser filtradas.  
  
> [!WARNING]  
>  Os métodos que levam `geography` ou tipos de dados `geometry` como argumentos retornarão `NULL` se o SRIDs não forem o mesmo para os tipos.  
  
 É recomendado que os novos mosaicos de índice espaciais sejam usados para índices usados em consultas de Vizinhos Mais Próximos. Para obter mais informações sobre mosaicos de índice espacial, veja [Dados espaciais &#40;SQL Server&#41;](spatial-data-sql-server.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir mostra para uma consulta de Vizinho Mais Próximo que pode usar um índice espacial. O exemplo usa a tabela `Person.Address` no banco de dados `AdventureWorks2012` .  
  
```  
USE AdventureWorks2012  
GO  
DECLARE @g geography = 'POINT(-121.626 47.8315)';  
SELECT TOP(7) SpatialLocation.ToString(), City FROM Person.Address  
WHERE SpatialLocation.STDistance(@g) IS NOT NULL  
ORDER BY SpatialLocation.STDistance(@g);  
  
```  
  
 Crie um índice espacial na coluna SpatialLocation para ver como uma consulta de Vizinho Mais Próximo usa um índice espacial. Para obter mais informações sobre como criar índices espaciais, consulte [Create, Modify, and Drop Spatial Indexes](create-modify-and-drop-spatial-indexes.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir mostra para uma consulta de Vizinho Mais Próximo que não pode usar um índice espacial.  
  
```  
USE AdventureWorks2012  
GO  
DECLARE @g geography = 'POINT(-121.626 47.8315)';  
SELECT TOP(7) SpatialLocation.ToString(), City FROM Person.Address  
ORDER BY SpatialLocation.STDistance(@g);  
  
```  
  
 A consulta não tem um `WHERE` cláusula usa `STDistance()` em um formulário especificado na seção de sintaxe para a consulta não pode usar um índice espacial.  
  
## <a name="see-also"></a>Consulte também  
 [Dados espaciais &#40;SQL Server&#41;](spatial-data-sql-server.md)  
  
  