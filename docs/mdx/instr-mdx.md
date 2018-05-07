---
title: InStr (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 5638c358-47da-40ad-b988-1a5214c05492
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 1e98798452a475c6ee8d71d3e68a44ad9118aef4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="instr-mdx"></a>Instr (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna a posição da primeira ocorrência de uma cadeia de caracteres em outra.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
InStr([start, ]searched_string, search_string[, compare])  
```  
  
## <a name="arguments"></a>Argumentos  
 *Início*  
 (Opcional) Uma expressão numérica que define a posição inicial de cada pesquisa. Se esse valor for omitido, a pesquisa começará na primeira posição de caractere. Se o início for nulo, o valor de retorno da função será indefinido.  
  
 *searched_string*  
 A expressão da cadeia de caracteres a ser pesquisada.  
  
 *search_string*  
 A expressão da cadeia de caracteres na qual pesquisar.  
  
 *Comparar*  
 (opcional) Um valor inteiro. Esse argumento é sempre ignorado. Ele é definido para compatibilidade com outros **Instr** funções em outros idiomas.  
  
## <a name="return-value"></a>Valor de retorno  
 Um valor inteiro com a posição inicial de *String2* na *String1*.  
  
 Além disso, **InStr** função retorna os valores listados na tabela a seguir, dependendo da condição:  
  
|Condição|Valor retornado|  
|---------------|------------------|  
|String1 tem comprimento zero|zero (0)|  
|String1 é nula|não definido|  
|String2 tem comprimento zero|start|  
|String2 é nula|não definido|  
|String2 não foi localizada|zero (0)|  
|start é maior que Len (String2)|zero (0)|  
  
## <a name="remarks"></a>Remarks  
  
> [!WARNING]  
>  **InStr** sempre executa uma comparação que diferencia maiusculas de minúsculas.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra o uso de **Instr** função e mostra diferentes cenários de resultados.  
  
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
  
|||  
|-|-|  
||Resultados|  
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
  
  
