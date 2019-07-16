---
title: EXPORTAÇÃO (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2cf3cf85b0efb024d65744f6eea0f5eea47ead83
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68074848"
---
# <a name="export-dmx"></a>EXPORT (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Extrai um modelo de mineração ou objeto de estrutura de mineração do servidor para um arquivo .abf (Analysis Services Backup).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
EXPORT <object type> <object name>[, <object name>] [<object type> <object name>[, <object name] ] TO <filename> [WITH DEPENDENCIES]  
```  
  
## <a name="arguments"></a>Argumentos  
 *tipo de objeto*  
 Opcional o tipo de objeto a ser exportado (modelo de mineração ou estrutura de mineração).  
  
 *nome do objeto*  
 Opcional. Nome do objeto a ser exportado.  
  
 *filename*  
 Nome e local do arquivo a ser exportado como cadeia de caracteres.  
  
## <a name="remarks"></a>Comentários  
 Se a instrução especificar um modelo de mineração, o arquivo resultante também conterá uma estrutura de mineração associada. Se a declaração especifica **WITH DEPENDENCIES**, todos os objetos necessários para processar o objeto (por exemplo, a fonte de dados e a exibição da fonte de dados) estão incluídos no arquivo. abf.  
  
 Você deve ser um banco de dados ou administrador do servidor para exportar ou importar objetos de um [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] banco de dados.  
  
## <a name="export-mining-structure-example"></a>Exemplo de estrutura de mineração de exportação  
 O exemplo a seguir exporta as estruturas de mineração Targeted Mailing e Forecasting, e o modelo de mineração Association para um local de arquivo específico. Como o modelo Association integra a estrutura de mineração de Market Basket, o exemplo exporta igualmente a estrutura Market Basket. Outros modelos de mineração que existam como parte da estrutura de mineração de cesta de compras não será exportado, porque o modelo de associação foi exportado usando **modelo de MINERAÇÃO**, e não **estrutura de MINERAÇÃO**.  
  
```  
EXPORT MINING STRUCTURE [Targeted Mailing], [Forecasting] MINING MODEL Association TO 'C:\TM_NEW.abf'  
```  
  
## <a name="export-mining-model-example"></a>Exemplo de modelo de mineração de exportação  
 O exemplo a seguir exporta o modelo de mineração de Associação para um local de arquivo especificado. Como a instrução especifica **WITH DEPENDENCIES**, a fonte de dados e objetos de exibição da fonte de dados também estão incluídos no arquivo. abf.  
  
```  
EXPORT MINING MODEL [Association] TO 'C:\Association_NEW.abf' WITH DEPENDENCIES  
```  
  
## <a name="see-also"></a>Consulte também  
 [Extensões de mineração de dados &#40;DMX&#41; instruções de definição de dados](../dmx/dmx-statements-data-definition.md)   
 [Extensões de mineração de dados &#40;DMX&#41; instruções de manipulação de dados](../dmx/dmx-statements-data-manipulation.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de instrução](../dmx/data-mining-extensions-dmx-statements.md)   
 [IMPORTAÇÃO &#40;DMX&#41;](../dmx/import-dmx.md)   
 [Exportar e importar objetos de Mineração de dados](../analysis-services/data-mining/export-and-import-data-mining-objects.md)  
  
  
