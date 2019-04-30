---
title: DataMember (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 98b10c951043416280c05fd6a0e5eeb5df92c104
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63248138"
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
 Essa função opera em membros não folha em qualquer hierarquia e pode ser usada pela [instrução do UPDATE CUBE (MDX)](../mdx/mdx-data-manipulation-update-cube.md) comando aos dados de write-back para um membro não folha diretamente, em vez de descendentes do membro folha.  
  
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
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [Principais conceitos em MDX &#40;Analysis Services&#41;](../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)  
  
  
