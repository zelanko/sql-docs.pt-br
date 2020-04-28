---
title: Filhos (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0af4d7b97777002dc5683c075f82531ccc8df86e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68016803"
---
# <a name="children-mdx"></a>Children (MDX)


  Retorna o conjunto de filhos de um membro especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Member_Expression.Children  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
## <a name="remarks"></a>Comentários  
 A função **Children** retorna um conjunto ordenado naturalmente que contém os filhos de um membro especificado. Se o membro especificado não tiver nenhum filho, essa função retornará um conjunto vazio.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna os filhos do membro Estados Unidos da hierarquia Geografia na dimensão Geografia.  
  
```  
SELECT [Geography].[Geography].[Country].&[United States].Children ON 0  
FROM [Adventure Works]  
```  
  
 O exemplo a seguir retorna todos os membros da dimensão **medidas** no eixo de coluna, incluindo todos os membros calculados e o conjunto de todos os filhos `[Product].[Model Name]` da hierarquia de atributo no eixo de linha do cubo **Adventure Works** .  
  
```  
SELECT  
    Measures.AllMembers ON COLUMNS,  
    [Product].[Model Name].Children ON ROWS  
FROM  
    [Adventure Works]  
  
```  
  
|Versão|Histórico|  
|-------------|-------------|  
|[!INCLUDE[ssBOL2005_R03](../includes/ssbol2005-r03-md.md)]|**Conteúdo alterado:**<br /> -Sintaxe e argumentos atualizados para melhorar a clareza.<br /><br /> -Foram adicionados exemplos atualizados.|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
