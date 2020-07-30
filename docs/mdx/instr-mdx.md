---
title: InStr (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7d7da3f994ed0741ef7ca6bcbe4d6003eea981c7
ms.sourcegitcommit: 99f61724de5edf6640efd99916d464172eb23f92
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87363406"
---
# <a name="instr-mdx"></a>Instr (MDX)


  Retorna a posição da primeira ocorrência de uma cadeia de caracteres em outra.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
InStr([start, ]searched_string, search_string[, compare])  
```  
  
## <a name="arguments"></a>Argumentos  
 *start*  
 (Opcional) Uma expressão numérica que define a posição inicial de cada pesquisa. Se esse valor for omitido, a pesquisa começará na primeira posição de caractere. Se o início for nulo, o valor de retorno da função será indefinido.  
  
 *searched_string*  
 A expressão da cadeia de caracteres a ser pesquisada.  
  
 *search_string*  
 A expressão da cadeia de caracteres na qual pesquisar.  
  
 *Comparar*  
 (opcional) Um valor inteiro. Esse argumento é sempre ignorado. Ele é definido para compatibilidade com outras funções **InStr** em outras linguagens.  
  
## <a name="return-value"></a>Valor retornado  
 Um valor inteiro com a posição inicial de *seqüência2* em *seqüência1*.  
  
 Além disso, a função **InStr** retorna os valores listados na tabela a seguir, dependendo da condição:  
  
|Condição|Valor retornado|  
|---------------|------------------|  
|String1 tem comprimento zero|zero (0)|  
|String1 é nula|não definido|  
|String2 tem comprimento zero|start|  
|String2 é nula|não definido|  
|String2 não foi localizada|zero (0)|  
|start é maior que Len (String2)|zero (0)|  
  
## <a name="remarks"></a>Comentários  
  
> [!WARNING]  
>  **InStr** sempre executa uma comparação que não diferencia maiúsculas de minúsculas.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra o uso da função **InStr** e mostra diferentes cenários de resultado.  
  
```  
with   
    member [Date].[Date].[Results] as "Results"  
    member measures.[lowercase found in lowercase string] as InStr( "abcdefghijklmnñopqrstuvwxyz", "o")  
    member measures.[uppercase found in lowercase string] as InStr( "abcdefghijklmnñopqrstuvwxyz", "O")  
    member measures.[searched string is empty]            as InStr( "", "o")  
    member measures.[searched string is null]             as iif(IsError(InStr( null, "o")), "Is Error", iif(IsNull(InStr( null, "o")), "Is Null","Is undefined"))  
    member measures.[search string is empty]              as InStr( "abcdefghijklmnñopqrstuvwxyz", "")  
    member measures.[search string is empty start 10]     as InStr(10, "abcdefghijklmnñopqrstuvwxyz", "")  
    member measures.[search string is null]               as iif(IsError(InStr( null, "o")), "Is Error", iif(IsNull(InStr( null, "o")), "Is Null","Is undefined"))  
    member measures.[found from start 10]                 as InStr( 10, "abcdefghijklmnñopqrstuvwxyz", "o")  
    member measures.[NOT found from start 17]             as InStr( 17, "abcdefghijklmnñopqrstuvwxyz", "o")  
    member measures.[NULL start]                          as iif(IsError(InStr( null, "abcdefghijklmnñopqrstuvwxyz", "o")), "Is Error", iif(IsNull(InStr( null, "abcdefghijklmnñopqrstuvwxyz", "o")), "Is Null","Is undefined"))  
    member measures.[start greater than searched length]  as InStr( 170, "abcdefghijklmnñopqrstuvwxyz", "o")  
  
select  [Results] on columns,  
       { measures.[lowercase found in lowercase string]  
       , measures.[uppercase found in lowercase string]  
       , measures.[searched string is empty]  
       , measures.[searched string is null]  
       , measures.[search string is empty]  
       , measures.[search string is empty start 10]  
       , measures.[search string is null]  
       , measures.[found from start 10]  
       , measures.[NOT found from start 17]  
       , measures.[NULL start]   
       , measures.[start greater than searched length]  
       } on rows  
  
from [Adventure Works]  
```  
  
 A tabela a seguir mostra os resultados obtidos.  
  
|Campo em medidas|Resultados|  
|-|-|  
|minúsculas encontradas em cadeia de caracteres em minúsculas.|16|  
|maiúsculas encontradas em cadeia de caracteres em minúsculas.|16|  
|a cadeia de caracteres pesquisada está vazia|0|  
|a cadeia de caracteres pesquisada é nula|É indefinido|  
|a cadeia de caracteres de pesquisa está vazia|1|  
|a cadeia de caracteres de pesquisa está vazia a partir do 10|10|  
|a cadeia de caracteres de pesquisa é nula|É indefinido|  
|encontrado a partir do 10|16|  
|NÃO encontrado a partir do 17|0|  
|Início NULO|É indefinido|  
|início maior que inicie maior que o comprimento da pesquisa|0|  
  
  
