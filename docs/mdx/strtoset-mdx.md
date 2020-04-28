---
title: StrToSet (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 729dae70fce03b3dec1394900126b216d09dc497
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68036793"
---
# <a name="strtoset-mdx"></a>StrToSet (MDX)


  Retorna o conjunto especificado por uma cadeia de caracteres formatada com MDX (Multidimensional Expressions).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
StrToSet(Set_Specification [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Specification*  
 Uma expressão de cadeia de caracteres válida especificando, direta ou indiretamente, um conjunto.  
  
## <a name="remarks"></a>Comentários  
 A função **StrToSet** retorna o conjunto especificado na expressão de cadeia de caracteres. A função **StrToSet** normalmente é usada com funções definidas pelo usuário para retornar uma especificação de conjunto de uma função externa de volta para uma instrução MDX ou quando uma consulta MDX é parametrizada.  
  
-   Quando o sinalizador restrito é usado, a especificação do conjunto deve conter nomes de membros qualificados ou não qualificados ou um conjunto de tuplas contendo nomes de membros qualificados ou não qualificados entre chaves {}. Esse sinalizador CONSTRAINED é usado para reduzir o risco de ataques de injeção pela cadeia de caracteres especificada. Se uma cadeia de caracteres fornecida não pode ser totalmente resolvida para nomes de membros qualificados ou não qualificados, surge o seguinte erro: "As restrições impostas pelo sinalizador CONSTRAINED na função STRTOVALUE foram violadas."  
  
-   Quando o sinalizador CONSTRAINED não é usado, a especificação de conjunto especificada é resolvida como uma linguagem MDX válida que retorna um conjunto.  
  
-   Para entender melhor as diferenças entre conjuntos e membros, consulte Usando expressões de conjuntos e Usando expressões de membros.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna o conjunto de membros da hierarquia de atributo State-província usando a função **StrToSet** . A especificação de conjunto fornece uma expressão de conjunto MDX válida.  
  
```  
SELECT StrToSet ('[Geography].[State-Province].Members')  
ON 0  
FROM [Adventure Works]  
  
```  
  
 O exemplo a seguir retorna um erro devido ao sinalizador CONSTRAINED. Enquanto a especificação de conjunto fornece uma expressão de conjunto MDX válida, o sinalizador CONSTRAINED requer nomes de membros qualificados ou não qualificados na especificação de conjunto.  
  
```  
SELECT StrToSet ('[Geography].[State-Province].Members', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
  
```  
  
 O exemplo a seguir retorna a medida Valor das Vendas do Revendedor para os países Alemanha e Canadá. A especificação de conjunto fornecida na cadeia de caracteres especificada contém nomes de membros qualificados, conforme exigido pelo sinalizador CONSTRAINED.  
  
```  
SELECT StrToSet ('{[Geography].[Geography].[Country].[Germany],[Geography].[Geography].[Country].[Canada]}', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
