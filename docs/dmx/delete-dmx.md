---
description: DELETE (DMX)
title: EXCLUIR (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c6050a387af893e984b95c036181b7f16a269dc0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491517"
---
# <a name="delete-dmx"></a>DELETE (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Limpa um modelo de mineração, uma estrutura de mineração ou uma estrutura de mineração e todos os modelos de mineração associados, dependendo das cláusulas DMX (Data Mining Extensions) usadas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DELETE FROM [MINING MODEL] <model>[.CONTENT]  
DELETE FROM [MINING STRUCTURE] <structure>[.CONTENT]|[.CASES]  
```  
  
## <a name="arguments"></a>Argumentos  
 *modelo*  
 Identificador de modelo.  
  
 *estruturá*  
 Identificador de estrutura.  
  
## <a name="remarks"></a>Comentários  
 Se você não especificar o **modelo de mineração** ou a **estrutura de mineração**, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] procurará o tipo de objeto com base no nome e processará o objeto correto. Se o servidor contiver uma estrutura de mineração e um modelo de mineração com nomes idênticos, um erro será retornado.  
  
 A tabela a seguir descreve o resultado de se usarem as diferentes formas da sintaxe.  
  
|de|Result|  
|---------------|------------|  
|EXCLUIR DA ESTRUTURA DE MINERAÇÃO*\<structure>*<br /><br /> ou<br /><br /> EXCLUIR da estrutura de mineração *\<structure>* . DISPUTA|Executa ProcessClear na estrutura de mineração. Todo o conteúdo é limpo da estrutura de mineração e de seus modelos de mineração associados.|  
|EXCLUIR da estrutura de mineração *\<structure>* . BOLSAS|Executa ProcessClearStructureOnly na estrutura de mineração. Todo o conteúdo é limpo da estrutura de mineração, deixando intactos os modelos de mineração associados. O detalhamento dos modelos de mineração associados falhará após a estrutura de mineração ter sido desmarcada.|  
|EXCLUIR DO MODELO DE MINERAÇÃO*\<model>*<br /><br /> ou<br /><br /> EXCLUIR do modelo de mineração *\<model>* . DISPUTA|Executa ProcessClear no modelo de mineração, mas deixa os valores de estado intactos. Os valores de estado consistem nos estados possíveis de uma coluna. Por exemplo, os valores de estado de uma coluna de sexo seriam masculino e feminino.|  
  
 Para obter mais informações sobre tipos de processamento, consulte [elemento Type &#40;&#41;XMLA ](https://docs.microsoft.com/analysis-services/xmla/xml-elements-properties/type-element-xmla).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir remove todo o conteúdo do modelo de NB_Sample.  
  
```  
DELETE FROM NB_Sample.CONTENT  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#40;&#41; instruções de definição de dados DMX de extensões de mineração de dados](../dmx/dmx-statements-data-definition.md)   
 [&#40;instruções de manipulação de dados do DMX&#41; extensões do Data Mining](../dmx/dmx-statements-data-manipulation.md)   
 [Referência de instruções de DMX &#40extensões de Mineração de Dados&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
