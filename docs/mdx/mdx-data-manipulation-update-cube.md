---
title: Instrução UPDATE CUBE (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f52dd59b67b42ad430df9bb1e9d00dce7ad6d697
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68003533"
---
# <a name="mdx-data-manipulation---update-cube"></a>Manipulação de dados MDX – UPDATE CUBE


  A instrução UPDATE CUBE é usada para fazer write-back de dados para qualquer célula em um cubo que é agregado a seu pai usando a agregação SUM. Para obter mais explicações e exemplos, consulte "Compreendendo alocações" nesta postagem no blog: [Criando um aplicativo de write-back com o Analysis Services (blog)](https://go.microsoft.com/fwlink/?LinkId=394977).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
UPDATE [ CUBE ] Cube_Name   
   SET   
            <update clause>   
           [, <update clause> ...n ]  
  
<update clause> ::=   
      Tuple_Expression[.VALUE]= New_Value  
      [   
        USE_EQUAL_ALLOCATION   
        | USE_EQUAL_INCREMENT   
        | USE_WEIGHTED_ALLOCATION [ BY Weight_Expression]   
        | USE_WEIGHTED_INCREMENT [ BY Weight_Expression]  
      ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *Cube_Name*  
 Uma cadeia de caracteres válida que fornece o nome de um cubo.  
  
 *Tuple_Expression*  
 Uma linguagem MDX válida que retorna uma tupla.  
  
 *Novo_valor*  
 Uma expressão numérica válida.  
  
 *Weight_Expression*  
 Uma expressão numérica MDX válida que retorna um valor decimal entre 0 e 1.  
  
## <a name="remarks"></a>Comentários  
 Você pode atualizar o valor de uma célula folha ou célula não folha especificada em um cubo, alocando opcionalmente o valor para uma célula não folha especificada em células folha dependentes. A célula especificada pela expressão de tupla pode ser qualquer célula válida no espaço multidimensional (ou seja, a célula não tem de ser uma célula folha). No entanto, a célula deve ser agregada com a [soma](../mdx/sum-mdx.md) função de agregação e não deve incluir um membro calculado na tupla que é usada para identificar a célula.  
  
 Ele pode ser útil considerar a **UPDATE CUBE** instrução como uma sub-rotina que irá gerar automaticamente uma série de operações de write-back de células individuais para células de folha e não-folha que acumularão em uma determinada soma.  
  
 A seguir está uma descrição dos métodos de alocação.  
  
 **USE_EQUAL_ALLOCATION:** Toda a célula folha que contribui para a célula atualizada será atribuída um valor igual com base na expressão abaixo.  
  
```  
<leaf cell value> =   
<New Value> / Count(leaf cells that are contained in <tuple>)  
```  
  
 **USE_EQUAL_INCREMENT:** Toda a célula folha que contribui para a célula atualizada será alterada de acordo com a expressão a seguir.  
  
```  
<leaf cell value> = <leaf cell value> +   
(<New Value > - <existing value>) /  
Count(leaf cells contained in <tuple>)  
```  
  
 **USE_WEIGHTED_ALLOCATION:** Toda a célula folha que contribui para a célula atualizada será atribuída um valor igual que baseia-se a expressão a seguir.  
  
```  
<leaf cell value> = < New Value> * Weight_Expression  
```  
  
 **USE_WEIGHTED_INCREMENT:** Toda a célula folha que contribui para a célula atualizada será alterada de acordo com a expressão a seguir.  
  
```  
<leaf cell value> = <leaf cell value> +   
(<New Value> - <existing value>)  * Weight_Expression  
```  
  
 Se uma expressão de peso não for especificada, o **UPDATE CUBE** instrução usa implicitamente a expressão a seguir.  
  
```  
Weight_Expression = <leaf cell value> / <existing value>  
```  
  
 Uma expressão de peso deve ser expressa como um valor decimal entre zero (0) e 1. Esse valor especifica a razão do valor alocado que você deseja atribuir às células folha afetadas pela alocação. O programador de aplicativo cliente tem a responsabilidade de criar expressões cujos valores de rollup agregados serão iguais ao valor alocado da expressão.  
  
> [!CAUTION]  
>  O aplicativo cliente deve considerar a alocação de todas as dimensões simultaneamente a fim de evitar possíveis resultados inesperados, inclusive valores de rollup incorretos ou dados inconsistentes.  
  
 Cada **UPDATE CUBE** alocação deve ser considerada atômica para fins transacionais. Isso significa que se qualquer uma das operações de alocação falhar por alguma razão, como um erro em uma fórmula ou uma violação de segurança, toda a operação UPDATE CUBE falhará. Antes que os cálculos das operações de alocação individuais sejam processados, um instantâneo dos dados é considerado para garantir que os cálculos resultantes sejam corretos.  
  
> [!CAUTION]  
>  Quando usado em uma medida que contenha inteiros, o método USE_WEIGHTED_ALLOCATION pode produzir resultados imprecisos decorrentes de alterações de arredondamento incremental.  
  
> [!IMPORTANT]  
>  Quando células atualizadas não se sobrepõem, a propriedade de cadeia de conexão **Atualizar Nível de Isolamento** pode ser usada para aprimorar o desempenho de UPDATE CUBE.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>   
 [Instruções MDX de manipulação de dados &#40;MDX&#41;](../mdx/mdx-data-manipulation-statements-mdx.md)  
  
  
