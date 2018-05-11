---
title: Propriedades DAX | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3960c3c2b98b26ce7508d5f11d1eafbdc486dca3
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="dax-properties"></a>Propriedades do DAX
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
   A seção DAX de msmdsrv.ini contém as configurações usadas para controlar certos comportamentos de consulta em [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], como o limite superior no número de linhas retornadas em um conjunto de resultados de consulta DAX.

  Para grandes conjuntos de linhas, como aqueles retornados nos modelos DirectQuery, o padrão de um milhão de linhas pode ser insuficiente. Você saberá se o limite deve ser ajustado se receber esse erro: "O conjunto de resultados de uma consulta de fonte de dados externa excedeu o tamanho máximo permitido de '1000000' linhas."

Para aumentar o limite superior, defina a configuração **MaxIntermediateRowSize** . Você precisará adicionar manualmente todo o elemento para a seção DAX do arquivo de configuração. A configuração não está presente no arquivo até você adicioná-la.

## <a name="configuration-snippet"></a>Trecho de código de Configuração

```
<ConfigurationSettings>
. . .
<DAX>
  <PredicateCheckSpoolCardinalityThreshold>5000
  </PredicateCheckSpoolCardinalityThreshold>
  <DQ>
     <MaxIntermediateRowsetSize>1000000
     </MaxIntermediateRowsetSize>
  </DQ>
</DAX>
. . .
```

## <a name="property-descriptions"></a>Descrições de propriedades

Configuração |Value |Description
--------|-------|-----------
MaxIntermediateRowsetSize | 1.000.000 | Número máximo de linhas retornadas em uma consulta DAX. Adicione manualmente essa entrada ao arquivo msmdsrv.ini e aumente o valor se o padrão for baixo demais.
PredicateCheckSpoolCardinalityThreshold| 5000 | Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da Microsoft.

Para obter mais informações sobre propriedades adicionais do servidor e como defini-las, consulte [Propriedades do servidor do Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md).
