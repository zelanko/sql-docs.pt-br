---
title: DataMember (MDX) | Microsoft Docs
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
- DATAMEMBER
dev_langs:
- kbMDX
helpviewer_keywords:
- DataMember function
ms.assetid: 65bf21e8-1cb2-4ae8-bfbe-bb4d72589557
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b6be9e31f666eafaba1ec7ad346a7e5bb28da9b0
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="datamember-mdx"></a>DataMember (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o membro de dados gerado pelo sistema associado a um membro não folha de uma dimensão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Member_Expression.DataMember  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
## <a name="remarks"></a>Comentários  
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
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)   
 [Principais conceitos em MDX &#40; Analysis Services &#41;](../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)  
  
  

