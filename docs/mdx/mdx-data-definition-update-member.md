---
title: Instrução UPDATE MEMBER (MDX) | Microsoft Docs
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
- UPDATE_MEMBER
- UPDATE MEMBER
- MEMBER
- UPDATE
helpviewer_keywords:
- calculated members [MDX]
- UPDATE MEMBER statement
ms.assetid: 07ab708d-d165-4fb1-a9f9-fb8197ff0dab
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 6f5591eeaaa2afd346e8038426f72e9b0c21520c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-data-definition---update-member"></a>Definição de dados MDX - UPDATE MEMBER
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Atualiza um membro calculado existente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
UPDATE MEMBER Cube_Name.Member_Name   
   AS MDX_Expression  
      [,Property_Name = Property_Value, ...n]  
......[,SCOPE_ISOLATION = CUBE]  
```  
  
## <a name="arguments"></a>Argumentos  
 *Cube_Name*  
 Uma cadeia de caracteres válida que especifica o nome do cubo que contém o membro.  
  
 *Member_Name*  
 Uma cadeia de caracteres válida que especifica o nome de um membro existente.  
  
 *MDX_Expression*  
 Uma linguagem MDX válida para a qual o membro será atualizado.  
  
 *Property_Name*  
 Uma cadeia de caracteres válida que especifica o nome de propriedade de membro calculado.  
  
 *Property_Value*  
 Uma expressão escalar válida que especifica o valor de propriedade do membro calculado.  
  
## <a name="remarks"></a>Remarks  
 A instrução UPDATE MEMBER atualiza um membro calculado existente enquanto preserva a precedência relativa desse membro em relação a outros cálculos. Portanto, não é possível usar a instrução UPDATE MEMBER para alterar SOLVEORDER.  
  
 Não é possível especificar uma instrução UPDATE MEMBER no script MDX de um cubo.  
  
 A especificação de um cubo diferente daquele conectado no momento causa um erro. Portanto, deve-se usar CURRENTCUBE no lugar de um nome de cubo para indicar o cubo atual.  
  
 Para obter mais informações sobre propriedades do membro definidas por OLE DB, consulte a documentação OLE DB.  
  
## <a name="standard-properties"></a>Propriedades padrão  
 Cada membro tem um conjunto de propriedades padrão. A tabela a seguir relaciona as propriedades padrão.  
  
|Identificador de propriedade|Significado|  
|-------------------------|-------------|  
|FORMAT_STRING|Um [!INCLUDE[msCoName](../includes/msconame-md.md)] cadeia de formato de estilo do Office que o aplicativo cliente pode usar para exibir valores de célula.|  
|VISIBLE|Um valor que indica se o membro calculado é visível em um conjunto de linhas de esquema. Calculados visíveis membros podem ser adicionados a um conjunto com o [AddCalculatedMembers](../mdx/addcalculatedmembers-mdx.md) função. Um valor diferente de zero indica que o membro calculado é visível. O valor padrão dessa propriedade é *visível*.<br /><br /> Em geral, membros calculados não visíveis são usados como etapas intermediárias em membros calculados mais complexos. Esses membros calculados também podem ser consultados por outros tipos de membros, como medidas.|  
|NON_EMPTY_BEHAVIOR|A medida ou o conjunto usado por MDX para determinar o comportamento de membros calculados ao resolver células vazias.|  
|CAPTION|Um valor de cadeia de caracteres que especifica a legenda que o aplicativo cliente usa para exibir o membro.|  
|DISPLAY_FOLDER|Um valor de cadeia de caracteres que especifica o caminho da pasta de exibição onde o membro será mostrado pelo aplicativo cliente. O separador de nível de pasta é definido pelo aplicativo cliente. Para ferramentas e clientes fornecidos pelo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], a barra invertida (\\) como separador de nível. Para fornecer várias pastas de exibição para um membro definido, use um ponto-e-vírgula (;) para separar as pastas.|  
|ASSOCIATED_MEASURE_GROUP|O nome do grupo de medidas ao qual esse membro está associado.|  
  
## <a name="see-also"></a>Consulte também  
 [Instrução de membro DROP &#40;MDX&#41;](../mdx/mdx-data-definition-drop-member.md)   
 [Criar declaração de membro & #40; MDX & #41;](../mdx/mdx-data-definition-create-member.md)   
 [Instruções de definição de dados MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
