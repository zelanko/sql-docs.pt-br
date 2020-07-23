---
title: OPENQUERY (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a075f314af0eb8ea2eb0bc941ada0bc38e22fec3
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "86970378"
---
# <a name="ltsource-data-querygt---openquery"></a>&lt;consulta de dados &gt; de origem-OPENQUERY
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Substitui uma consulta de dados de origem por uma consulta em uma fonte de dados existente. As instruções de inserção, seleção de junção de previsão e seleção de junção de previsão NATURAL dão suporte a **OPENQUERY**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
OPENQUERY(<named datasource>, <query syntax>)  
```  
  
## <a name="arguments"></a>Argumentos  
 *fonte de fontes nomeada*  
 Uma fonte de dados que existe no banco de dado [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
 *sintaxe de consulta*  
 Sintaxe de consulta que retorna um conjunto de linhas.  
  
## <a name="remarks"></a>Comentários  
 **OPENQUERY** fornece uma maneira mais segura de acessar dados externos ao dar suporte a permissões de fonte de dados. Como a cadeia de conexão é armazenada na fonte de dados, os administradores podem usar as propriedades da fonte de dados para gerenciar o acesso aos dados. Para obter mais informações sobre fontes de dados, consulte [fontes de dados com suporte &#40;SSAS-&#41;multidimensional ](https://docs.microsoft.com/analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional).  
  
 Você pode obter uma lista das fontes de dados que estão disponíveis em um servidor consultando o conjunto de linhas de esquema **MDSCHEMA_INPUT_DATASOURCES** . Para obter mais informações sobre como usar **MDSCHEMA_INPUT_DATASOURCES**, consulte [MDSCHEMA_INPUT_DATASOURCES conjunto de linhas](https://docs.microsoft.com/previous-versions/sql/sql-server-2012/ms126243(v=sql.110)).  
  
 Também é possível retornar uma lista das fontes de dados no banco de dados atual do Analysis Services usando a seguinte consulta DMX:  
  
 `SELECT * FROM $system.MDSCHEMA_INPUT_DATASOURCES`  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa a fonte de dados MyDS já definida no banco de dado [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para criar uma conexão com o [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] Database e consultar a exibição **vTargetMail** .  
  
```  
OPENQUERY (MyDS,'SELECT TOP 1000 * FROM vTargetMail')  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#62;de consulta de dados de origem&#60;](../dmx/source-data-query.md)   
 [&#40;instruções de manipulação de dados do DMX&#41; extensões do Data Mining](../dmx/dmx-statements-data-manipulation.md)   
 [Referência de instruções de DMX &#40extensões de Mineração de Dados&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
