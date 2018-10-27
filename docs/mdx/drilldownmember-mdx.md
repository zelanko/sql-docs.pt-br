---
title: DrilldownMember (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f5ab4ee77bad08ab3883645ad5e2628a265aa4e9
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50144891"
---
# <a name="drilldownmember-mdx"></a>DrilldownMember (MDX)


  Faz uma busca detalhada dos membros de um determinado conjunto que estejam presentes em um segundo conjunto especificado.  
  
 Alternativamente, a função faz uma busca detalhada em um conjunto de tuplas usando a primeira hierarquia de tuplas ou a hierarquia especificada opcionalmente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DrillDownMember(<Set_Expression1>, <Set_Expression2> [,[<Target_Hierarchy>]] [,[RECURSIVE][,INCLUDE_CALC_MEMBERS]])  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression1*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Set_Expression2*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Target_Hierarchy*  
 Uma linguagem MDX válida que retorna uma hierarquia.  
  
 *Recursiva*  
 Uma palavra-chave que indica comparação recursiva de conjuntos.  
  
 *Include_Calc_Members*  
 Uma palavra-chave para habilitar a ser incluído nos resultados da busca detalhada dos membros calculados.  
  
## <a name="remarks"></a>Comentários  
 Essa função retorna um conjunto de membros filho que são ordenados por hierarquia e inclui membros especificados no primeiro conjunto que também estão presentes no segundo conjunto. Membros pai não serão buscados se o primeiro conjunto contiver o membro pai e um ou mais filhos. O primeiro conjunto pode ter qualquer dimensionalidade, mas o segundo deve conter um conjunto unidimensional. A ordem é preservada entre os membros originais no primeiro conjunto, a não ser que todos os membros filho incluídos no conjunto de resultados da função sejam imediatamente incluídos com seu membro pai. A função constrói o conjunto de resultados recuperando os filhos para cada membro no primeiro conjunto que também está presente no segundo conjunto. Se **RECURSIVA** for especificado, a função continua a comparar recursivamente os membros do resultado definidos em relação ao segundo conjunto, recuperando os filhos para cada membro no conjunto de resultados que também está presente no segundo conjunto até que não mais os membros do conjunto de resultados podem ser encontrados no segundo conjunto.  
  
 Consultando a propriedade XMLA **MdpropMdxDrillFunctions** lhe permite verificar se o nível de suporte que o servidor fornece para as funções de detalhamento; consulte [propriedades XMLA com suporte &#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties)para obter detalhes.  
  
 O primeiro conjunto pode conter tuplas em vez de membros. A busca detalhada de tupla é uma extensão de OLE DB e retorna um conjunto de tuplas em vez de membros.  
  
> [!IMPORTANT]  
>  Um membro não será buscado se for seguido imediatamente por um dos seus filhos. A ordem dos membros do conjunto é importante para tanto o Drilldown * quanto Drillup\* famílias de funções.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir faz uma busca detalhada na Austrália, que é o membro do primeiro conjunto que também está presente no segundo conjunto.  
  
```  
SELECT DrilldownMember   
   ( [Geography].[Geography].Children,  
      {[Geography].[Geography].[Country].[Australia],  
        [Geography].[Geography].[State-Province].[New South Wales]}  
   )  
   ON 0  
   FROM [Adventure Works]  
```  
  
 O exemplo a seguir faz uma busca detalhada na Austrália, que é o membro do primeiro conjunto que também está presente no segundo conjunto. Porém, como o argumento RECURSIVE está presente, a função continua a comparar recursivamente os membros do conjunto de resultados (membros do nível de Estado) em relação ao segundo conjunto, recuperando os filhos para cada membro no conjunto de resultados (membros do nível Cidade) que também está presente no segundo conjunto, até que nenhum membro do conjunto de resultados possa ser encontrado no segundo conjunto.  
  
```  
SELECT DrilldownMember   
   ( [Geography].[Geography].Children,  
      {[Geography].[Geography].[Country].[Australia],  
        [Geography].[Geography].[State-Province].[New South Wales]}  
   ,RECURSIVE)  
   ON 0  
   FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
