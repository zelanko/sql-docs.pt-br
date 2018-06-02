---
title: UnknownMember (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b74454c00f48a36b963e6c7f5b7b1bdf4e2ea44e
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34582208"
---
# <a name="unknownmember-mdx"></a>UnknownMember (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna o membro desconhecido associado a um nível ou membro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Member expression syntax  
Member_Expression.UnknownMember  
  
Hierarchy_expression syntax  
Hierarchy_Expression.UnknownMember  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
 *Expressão_Hierarquia*  
 Uma linguagem MDX válida que retorna uma hierarquia.  
  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] cria um membro desconhecido para associar dados da tabela de fatos uma hierarquia quando a hierarquia não é conhecida. O membro desconhecido pode estar em um dos seguintes níveis:  
  
-   No nível superior para hierarquias de atributo que não são agregadas.  
  
-   No primeiro nível abaixo de **todos os** nível para hierarquias naturais.  
  
-   Em qualquer nível para hierarquias não naturais.  
  
 Se uma expressão de membro for especificada, o **UnknownMember** função retorna o filho do membro desconhecido do membro especificado. Se o membro especificado não existir, a função retornará nulo.  
  
 Se uma expressão de hierarquia for especificada, o **UnknownMember** função retorna o membro desconhecido no nível superior, se houver.  
  
 Se o membro desconhecido não existe no nível ou membro, o **UnknownMember** função cria um membro nulo.  
  
> [!NOTE]  
>  Se o membro desconhecido não existir na hierarquia ou membro, um erro será gerado.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna o membro desconhecido para o membro Todos os Produtos na hierarquia de atributo Produto para todos os membros da dimensão Medidas.  
  
```  
SELECT [Product].[Product].[All Products].UnknownMember  
    ON Columns,  
[Measures].Members  
    ON Rows  
FROM [Adventure Works]  
  
```  
  
 O exemplo a seguir retorna o membro desconhecido para a hierarquia Categorias de Produtos para todos os membros da dimensão Medidas.  
  
```  
SELECT [Product].[Product Categories].UnknownMember  
    ON Columns,  
[Measures].Members  
    ON Rows  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
