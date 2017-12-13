---
title: Cubo de armazenamento (Analysis Services - dados multidimensionais) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- measure groups [Analysis Services], cubes
- cubes [Analysis Services], storage
- linked measure groups [Analysis Services]
- storing data [Analysis Services], cubes
- partitions [Analysis Services], cubes
- storage [Analysis Services], cubes
ms.assetid: 1b1ad360-9a9b-4996-bee9-84238a2bb4ac
caps.latest.revision: "41"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 83762a6da2ee3b67c388fdd7b1b3ac5ffc144573
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="cube-storage-analysis-services---multidimensional-data"></a>Armazenamento de cubo (Analysis Services – Dados Multidimensional)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Armazenamento pode incluir apenas os metadados do cubo ou pode incluir todos os dados de origem da tabela de fatos, bem como as agregações definidas por dimensões relacionadas ao grupo de medidas. A quantidade de dados armazenados depende do modo de armazenamento selecionado e do número de agregações. A quantidade de dados armazenados afeta diretamente o desempenho de consulta. [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa diversas técnicas para minimizar o espaço necessário para o armazenamento de dados de cubo e agregações:  
  
-   As opções de armazenamento permitem selecionar os modos e os locais de armazenamento mais apropriados para os dados do cubo.  
  
-   Um algoritmo sofisticado projeta agregações de resumo eficientes para minimizar o armazenamento sem comprometer a velocidade.  
  
-   O armazenamento não é alocado para células vazias.  
  
 O armazenamento é definido em uma base partição por partição e há pelo menos uma partição para cada grupo de medidas em um cubo. Para obter mais informações, consulte [partições &#40; Analysis Services - dados multidimensionais &#41; ](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md), [Modos de armazenamento e processamento de partição](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md), [e grupos de medidas](../../analysis-services/multidimensional-models/measures-and-measure-groups.md), e [criar medidas e grupos de medidas em modelos multidimensionais](../../analysis-services/multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md) .  
  
## <a name="partition-storage"></a>Armazenamento de partição   
 O armazenamento de um grupo de medidas pode ser dividido em várias partições. As partições permitem que você distribua um grupo de medidas em segmentos discretos em um único servidor, ou por vários servidores, e para otimizar o desempenho de armazenamento e a consulta. Cada partição em um grupo de medidas pode ser baseada em uma fonte de dados diferente e armazenada usando diferentes configurações de armazenamento.  
  
 Você pode especificar a fonte de dados de uma partição ao criá-la. Você também pode alterar a fonte de dados de qualquer partição existente. Um grupo de medidas pode ser particionado verticalmente ou horizontalmente. Cada partição em um grupo de medidas particionado verticalmente está baseada em uma exibição filtrada de uma única tabela de origem. Por exemplo, se um grupo de medidas estiver baseado em uma única tabela que contiver vários anos de dados, será possível criar uma partição separada para os dados de cada ano. Por outro lado, cada partição em um grupo de medidas particionado horizontalmente será baseado em uma tabela separada. Você pode usar partições horizontais se a fonte de dados armazenar os dados de cada ano em uma tabela separada.  
  
 As partições são criadas inicialmente com as mesmas configurações de armazenamento que o grupo de medidas no qual eles são criados. As configurações de armazenamento determinam se os dados de detalhes e agregações são armazenados em um formato multidimensional na instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], no formato relacional no servidor de origem ou uma combinação de ambos. As configurações de armazenamento também determinam se o cache pró-ativo é usado para processar automaticamente as alterações de dados de origem para dados multidimensionais armazenados no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 As partições de um cubo não são visíveis ao usuário. No entanto, a escolha de configurações de armazenamento para partições diferentes pode afetar a instantaneidade dos dados, a quantidade de espaço em disco usado e o desempenho de consulta. As partições podem ser armazenadas em várias instâncias do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Isso fornece uma abordagem de cluster do armazenamento do cubo e distribui cargas de trabalho pelos servidores [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para obter mais informações, consulte [modos de armazenamento de partição e processamento](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md), [partições remotas](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-remote-partitions.md), e [partições &#40; Analysis Services - dados multidimensionais &#41; ](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md).  
  
## <a name="linked-measure-groups"></a>Grupos de medidas vinculados  
 Isso pode exigir um espaço em disco considerável para armazenar várias cópias de um cubo em instâncias diferentes do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], mas você pode reduzir, consideravelmente, o espaço necessário substituindo as cópias do grupo de medidas por grupos de medidas vinculados. Um grupo de medidas vinculado é baseado em um grupo de medidas em um cubo em outro banco de dados [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], na mesma instância ou em uma instância diferente do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Um grupo de medidas vinculado também pode ser usado com dimensões vinculadas do mesmo cubo de origem. As dimensões vinculadas e os grupos de medidas usam as agregações do cubo de origem e não têm requisitos de armazenamento de dados próprios. Portanto, mantendo os grupos de medidas de origem e dimensões em um banco de dados e criando cubos vinculados e dimensões em cubos em outros bancos de dados, você pode economizar espaço em disco que, de outra maneira, seria usado para armazenamento. Para obter mais informações, consulte [grupos de medidas vinculados](../../analysis-services/multidimensional-models/linked-measure-groups.md).  
  
## <a name="see-also"></a>Consulte também  
 [Agregações e designs de agregação](../../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)  
  
  
