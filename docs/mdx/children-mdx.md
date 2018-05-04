---
title: Filhos (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CHILDREN
dev_langs:
- kbMDX
helpviewer_keywords:
- Children function
ms.assetid: ce2c3069-914c-44a3-8a4c-5cbd4fb71e4c
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 03cb4f1a05e9be35a92c63c5904816ed8d0ad227
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="children-mdx"></a>Children (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna o conjunto de filhos de um membro especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Member_Expression.Children  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
## <a name="remarks"></a>Remarks  
 O **filhos** função retorna um conjunto ordenado naturalmente que contém os filhos de um membro especificado. Se o membro especificado não tiver nenhum filho, essa função retornará um conjunto vazio.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna os filhos do membro Estados Unidos da hierarquia Geografia na dimensão Geografia.  
  
```  
SELECT [Geography].[Geography].[Country].&[United States].Children ON 0  
FROM [Adventure Works]  
```  
  
 O exemplo a seguir retorna todos os membros de **medidas** dimensão no eixo da coluna, isso inclui todos os membros calculados e o conjunto de todos os filhos do `[Product].[Model Name]` hierarquia no eixo da linha de atributo a **Adventure Works** cubo.  
  
```  
SELECT  
    Measures.AllMembers ON COLUMNS,  
    [Product].[Model Name].Children ON ROWS  
FROM  
    [Adventure Works]  
  
```  
  
|Versão|Histórico|  
|-------------|-------------|  
|[!INCLUDE[ssBOL2005_R03](../includes/ssbol2005-r03-md.md)]|**Conteúdo alterado:**<br /> — Atualizada a sintaxe e argumentos para melhorar a clareza.<br /><br /> — Exemplos atualizados somados.|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
