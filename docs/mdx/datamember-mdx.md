---
description: DataMember (MDX)
title: DataMember (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ea373dc4ffe7eb01b19969288afce45489ab4e8c
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196030"
---
# <a name="datamember-mdx"></a>DataMember (MDX)


  Retorna o membro de dados gerado pelo sistema associado a um membro não folha de uma dimensão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Member_Expression.DataMember  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
## <a name="remarks"></a>Comentários  
 Essa função opera em membros não folha em qualquer hierarquia e pode ser usada pelo comando [Update Cube Statement (MDX)](../mdx/mdx-data-manipulation-update-cube.md) para fazer write-back de dados para um membro não folha diretamente, em vez de para os descendentes do membro folha.  
  
> [!NOTE]  
>  Retorna o membro especificado se o membro especificado for um membro folha ou se o membro não folha não tiver um membro de dados associado.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir usa a função **DataMember** em uma medida calculada para mostrar a cota de vendas para cada funcionário individual:  
  
```  
WITH MEMBER measures.InvidualQuota AS   
([Employee].[Employees].currentmember.datamember, [Measures].[Sales Amount Quota])  
,FORMAT_STRING='Currency'  
SELECT {[Measures].[Sales Amount Quota],[Measures].InvidualQuota} ON COLUMNS,  
[Employee].[Employees].MEMBERS ON ROWS  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função MDX &#40;&#41;MDX ](../mdx/mdx-function-reference-mdx.md)   
 [Principais conceitos em MDX &#40;Analysis Services&#41;](/analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services)  
  
