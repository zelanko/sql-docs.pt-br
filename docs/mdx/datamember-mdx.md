---
title: DataMember (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2979799686ad1d97018471111c57670383f7f4f8
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34577848"
---
# <a name="datamember-mdx"></a>DataMember (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna o membro de dados gerado pelo sistema associado a um membro não folha de uma dimensão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Member_Expression.DataMember  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
## <a name="remarks"></a>Remarks  
 Essa função opera em membros não folha em qualquer hierarquia e podem ser usada pelo [UPDATE CUBE instrução (MDX)](../mdx/mdx-data-manipulation-update-cube.md) comando write-back dados a um membro não folha diretamente, em vez de descendentes do membro folha.  
  
> [!NOTE]  
>  Retorna o membro especificado se o membro especificado for um membro folha ou se o membro não folha não tiver um membro de dados associado.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir usa o **DataMember** função em uma medida calculada para mostrar a cota de vendas para cada funcionário individual:  
  
```  
WITH MEMBER measures.InvidualQuota AS   
([Employee].[Employees].currentmember.datamember, [Measures].[Sales Amount Quota])  
,FORMAT_STRING='Currency'  
SELECT {[Measures].[Sales Amount Quota],[Measures].InvidualQuota} ON COLUMNS,  
[Employee].[Employees].MEMBERS ON ROWS  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [Principais conceitos em MDX &#40;do Analysis Services&#41;](../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)  
  
  
