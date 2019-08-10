---
title: OPENQUERY (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: caac43eb176e17a6e92e487f3dedae71a252f5af
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68887724"
---
# <a name="ltsource-data-querygt---openquery"></a>&lt;consulta&gt; de dados de origem-OPENQUERY
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Substitui uma consulta de dados de origem por uma consulta em uma fonte de dados existente. As instruções de inserção, seleção de junção de previsão e seleção de junção de previsão NATURAL dão suporte a **OPENQUERY**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
OPENQUERY(<named datasource>, <query syntax>)  
```  
  
## <a name="arguments"></a>Argumentos  
 *fonte de fontes nomeada*  
 Uma fonte de dados que existe no [!INCLUDE[msCoName](../includes/msconame-md.md)] banco de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] dado.  
  
 *sintaxe de consulta*  
 Sintaxe de consulta que retorna um conjunto de linhas.  
  
## <a name="remarks"></a>Comentários  
 **OPENQUERY** fornece uma maneira mais segura de acessar dados externos ao dar suporte a permissões de fonte de dados. Como a cadeia de conexão é armazenada na fonte de dados, os administradores podem usar as propriedades da fonte de dados para gerenciar o acesso aos dados. Para obter mais informações sobre fontes de dados, consulte [fontes &#40;de dados com suporte SSAS&#41;-](https://docs.microsoft.com/analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional)multidimensional.  
  
 Você pode obter uma lista das fontes de dados que estão disponíveis em um servidor consultando o conjunto de linhas de esquema **MDSCHEMA_INPUT_DATASOURCES** . Para obter mais informações sobre como usar **MDSCHEMA_INPUT_DATASOURCES**, consulte [conjunto de linhas MDSCHEMA_INPUT_DATASOURCES](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-input-datasources-rowset).  
  
 Também é possível retornar uma lista das fontes de dados no banco de dados atual do Analysis Services usando a seguinte consulta DMX:  
  
 `SELECT * FROM $system.MDSCHEMA_INPUT_DATASOURCES`  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa a fonte de dados MyDS já definida [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] no banco de dado para criar uma [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] conexão com o Database e consultar a exibição **vTargetMail** .  
  
```  
OPENQUERY (MyDS,'SELECT TOP 1000 * FROM vTargetMail')  
```  
  
## <a name="see-also"></a>Consulte também  
 [&#60;consulta de dados de origem&#62;](../dmx/source-data-query.md)   
 [Instruções de manipulação &#40;de&#41; dados DMX de extensões de mineração de dados](../dmx/dmx-statements-data-manipulation.md)   
 [Referência de instruções de DMX &#40extensões de Mineração de Dados&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
