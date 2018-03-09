---
title: StrToMember (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: STRTOMEMBER
dev_langs: kbMDX
helpviewer_keywords: StrToMember function
ms.assetid: eb8a3dc0-5ae4-434e-b321-680a81a59e67
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: b26a0a5922f138bc13bbb13099809629ee336b02
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="strtomember-mdx"></a>StrToMember (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna o membro especificado por uma cadeia de caracteres formatada em linguagem MDX.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
StrToMember(Member_Name [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Name*  
 Uma expressão de cadeia de caracteres válidos especificando, direta ou indiretamente, um membro.  
  
## <a name="remarks"></a>Remarks  
 O **StrToMember** função retorna o membro especificado na expressão de cadeia de caracteres. O **StrToMember** função geralmente é usada com funções definidas pelo usuário para retornar uma especificação de membro de uma função externa para uma instrução MDX, ou quando uma consulta MDX é parametrizada.  
  
-   Quando o sinalizador CONSTRAINED for usado, o nome de membro deverá ser diretamente resolvido para um nome de membro qualificado ou não qualificado. Esse sinalizador CONSTRAINED é usado para reduzir o risco de ataques de injeção pela cadeia de caracteres especificada. Se uma cadeia de caracteres fornecida não for totalmente resolvida para um nome de membro qualificado ou não qualificado, surge o seguinte erro: "As restrições impostas pelo sinalizador CONSTRAINED na função STRTOMEMBER foram violadas".  
  
-   Quando o sinalizador de CONSTRAINED não for usado, o membro especificado poderá resolver diretamente um nome de membro ou uma linguagem MDX que resolve um nome.  
  
-   Para entender melhor as diferenças entre conjuntos e membros, consulte Usando expressões de conjuntos e Usando expressões de membros.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna a medida quantidade de vendas de revendedor para o membro Bayern na hierarquia de atributo estado-província usando o **StrToMember** função. A cadeia de caracteres especificada forneceu o nome de membro qualificado.  
  
```  
SELECT {StrToMember ('[Geography].[State-Province].[Bayern]')}  
ON 0,  
{[Measures].[Reseller Sales Amount]} ON 1  
FROM [Adventure Works]  
  
```  
  
 O exemplo a seguir retorna a medida quantidade de vendas de revendedor para o membro Bayern usando o **StrToMember** função. Considerando que a cadeia de caracteres de nome de membro forneceu apenas um nome de membro não qualificado, a consulta retorna a primeira instância do membro especificado, que está na hierarquia Geografia do Cliente, na dimensão Cliente, que não faz intersecção com Vendas do Revendedor. As práticas recomendadas ditam que se especifique o nome qualificado para assegurar resultados esperados.  
  
```  
SELECT {StrToMember ('[Bayern]').Parent}  
ON 0,  
{[Measures].[Reseller Sales Amount]} ON 1  
FROM [Adventure Works]  
  
```  
  
 O exemplo a seguir retorna a medida quantidade de vendas de revendedor para o membro Bayern na hierarquia de atributo estado-província usando o **StrToMember** função. A cadeia de caracteres de nome de membro fornecida resolve um nome de membro qualificado.  
  
```  
SELECT {StrToMember('[Geography].[Geography].[Country].[Germany].FirstChild', CONSTRAINED)}  
ON 0,  
{[Measures].[Reseller Sales Amount]} ON 1  
FROM [Adventure Works]  
  
```  
  
 O exemplo a seguir retorna um erro devido ao sinalizador CONSTRAINED. Enquanto a cadeia de caracteres de nome de membro fornecida contém uma expressão de membro MDX válida, que resolve um nome de membro qualificado, o sinalizador CONSTRAINED exige nomes de membros qualificados ou não qualificados na cadeia de caracteres de nome de membro.  
  
```  
SELECT StrToMember ('[Geography].[Geography].[Country].[Germany].FirstChild', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
