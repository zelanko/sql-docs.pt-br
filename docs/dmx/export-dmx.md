---
title: EXPORTAR (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 622f575541d1a111e5cda6a28617ad400a977292
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892806"
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
 Opcional. o tipo do objeto a ser exportado (modelo de mineração ou estrutura de mineração).  
  
 *nome do objeto*  
 Opcional. Nome do objeto a ser exportado.  
  
 *filename*  
 Nome e local do arquivo a ser exportado como cadeia de caracteres.  
  
## <a name="remarks"></a>Comentários  
 Se a instrução especificar um modelo de mineração, o arquivo resultante também conterá uma estrutura de mineração associada. Se a instrução especifica **com dependências**, todos os objetos necessários para processar o objeto (por exemplo, a fonte de dados e a exibição da fonte de dados) são incluídos no arquivo. ABF.  
  
 Você deve ser um administrador de banco de dados ou servidor para exportar ou importar [!INCLUDE[msCoName](../includes/msconame-md.md)] objetos de um [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] banco de dados.  
  
## <a name="export-mining-structure-example"></a>Exemplo de estrutura de mineração de exportação  
 O exemplo a seguir exporta as estruturas de mineração Targeted Mailing e Forecasting, e o modelo de mineração Association para um local de arquivo específico. Como o modelo Association integra a estrutura de mineração de Market Basket, o exemplo exporta igualmente a estrutura Market Basket. Qualquer outro modelo de mineração que possa existir como parte da estrutura de mineração de cesta de mercado não será exportado porque o modelo de associação foi exportado usando o **modelo de mineração**, não a **estrutura de mineração**.  
  
```  
EXPORT MINING STRUCTURE [Targeted Mailing], [Forecasting] MINING MODEL Association TO 'C:\TM_NEW.abf'  
```  
  
## <a name="export-mining-model-example"></a>Exemplo de modelo de mineração de exportação  
 O exemplo a seguir exporta o modelo de mineração de Associação para um local de arquivo especificado. Como a instrução especifica **com dependências**, os objetos fonte de dados e exibição da fonte de dados também estão incluídos no arquivo. ABF.  
  
```  
EXPORT MINING MODEL [Association] TO 'C:\Association_NEW.abf' WITH DEPENDENCIES  
```  
  
## <a name="see-also"></a>Consulte também  
 [Instruções de definição &#40;de&#41; dados DMX das extensões de mineração de dados](../dmx/dmx-statements-data-definition.md)   
 [Instruções de manipulação &#40;de&#41; dados DMX de extensões de mineração de dados](../dmx/dmx-statements-data-manipulation.md)   
 [Referência de instrução &#40;DMX&#41; de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-statements.md)   
 [IMPORTAR &#40;DMX&#41;](../dmx/import-dmx.md)   
 [Exportar e importar objetos de Mineração de dados](https://docs.microsoft.com/analysis-services/data-mining/export-and-import-data-mining-objects)  
  
  
