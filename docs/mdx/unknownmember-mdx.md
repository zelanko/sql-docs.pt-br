---
title: UnknownMember (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- UnknownMember
dev_langs:
- kbMDX
helpviewer_keywords:
- UnknownMember function
ms.assetid: 5ae39cbe-65c8-4a59-9548-71b28ecf6eb5
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 131993b1038229138df3e7d084b5d842693b7f0f
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="unknownmember-mdx"></a>UnknownMember (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
## <a name="remarks"></a>Comentários  
 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] cria um membro desconhecido para associar dados da tabela de fatos uma hierarquia quando a hierarquia não é conhecida. O membro desconhecido pode estar em um dos seguintes níveis:  
  
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
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

