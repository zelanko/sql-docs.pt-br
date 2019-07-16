---
title: Instrução UPDATE MEMBER (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 73a2bf2973d8c4f8f9bf9ac886728fb45250343f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038138"
---
# <a name="mdx-data-definition---update-member"></a>Definição de dados MDX – UPDATE MEMBER


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
  
## <a name="remarks"></a>Comentários  
 A instrução UPDATE MEMBER atualiza um membro calculado existente enquanto preserva a precedência relativa desse membro em relação a outros cálculos. Portanto, não é possível usar a instrução UPDATE MEMBER para alterar SOLVEORDER.  
  
 Não é possível especificar uma instrução UPDATE MEMBER no script MDX de um cubo.  
  
 A especificação de um cubo diferente daquele conectado no momento causa um erro. Portanto, deve-se usar CURRENTCUBE no lugar de um nome de cubo para indicar o cubo atual.  
  
 Para obter mais informações sobre propriedades do membro definidas por OLE DB, consulte a documentação OLE DB.  
  
## <a name="standard-properties"></a>Propriedades padrão  
 Cada membro tem um conjunto de propriedades padrão. A tabela a seguir relaciona as propriedades padrão.  
  
|Identificador de propriedade|Significado|  
|-------------------------|-------------|  
|FORMAT_STRING|Uma cadeia de formato de estilo Office que o aplicativo cliente pode usar para exibir valores de célula.|  
|VISIBLE|Um valor que indica se o membro calculado é visível em um conjunto de linhas de esquema. Calculados visíveis membros podem ser adicionados a um conjunto com o [AddCalculatedMembers](../mdx/addcalculatedmembers-mdx.md) função. Um valor diferente de zero indica que o membro calculado é visível. O valor padrão desta propriedade é *Visible*.<br /><br /> Em geral, membros calculados não visíveis são usados como etapas intermediárias em membros calculados mais complexos. Esses membros calculados também podem ser consultados por outros tipos de membros, como medidas.|  
|NON_EMPTY_BEHAVIOR|A medida ou o conjunto usado por MDX para determinar o comportamento de membros calculados ao resolver células vazias.|  
|CAPTION|Um valor de cadeia de caracteres que especifica a legenda que o aplicativo cliente usa para exibir o membro.|  
|DISPLAY_FOLDER|Um valor de cadeia de caracteres que especifica o caminho da pasta de exibição onde o membro será mostrado pelo aplicativo cliente. O separador de nível de pasta é definido pelo aplicativo cliente. Para as ferramentas e clientes fornecidos pelo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], a barra invertida (\\) como separador de nível. Para fornecer várias pastas de exibição para um membro definido, use um ponto-e-vírgula (;) para separar as pastas.|  
|ASSOCIATED_MEASURE_GROUP|O nome do grupo de medidas ao qual esse membro está associado.|  
  
## <a name="see-also"></a>Consulte também  
 [Instrução de membro DROP &#40;MDX&#41;](../mdx/mdx-data-definition-drop-member.md)   
 [Instrução CREATE MEMBER &#40;MDX&#41;](../mdx/mdx-data-definition-create-member.md)   
 [Instruções de definição de dados MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
