---
title: Geral (caixa de diálogo de propriedades de partição) (SSMS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.partitionproperties.general.f1
ms.assetid: efb505be-354f-4d23-8f2d-3e76fa50d27b
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 54ef8ce15795f8744b8ab7d368c05892a2dc850a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37170147"
---
# <a name="general-partition-properties-dialog-box-ssms"></a>Geral (caixa de diálogo Propriedades da Partição) (SSMS)
  Use a página **Geral** da caixa de diálogo **Propriedades da Partição** no SQL Server Management Studio para definir as propriedades gerais de uma partição em um grupo de medidas para um cubo em um banco de dados do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
## <a name="options"></a>Opções  
  
|Termo|Definição|  
|----------|----------------|  
|**ID de Design de agregação**|Exibe o identificador do design de agregação usado pela partição.|  
|**Prefixo de agregação**|Exibe o prefixo padrão de instâncias de agregação que são contidas pela partição.|  
|**Criar Carimbo de Data/Hora**|Exibe a data e a hora de criação da partição.|  
|**Modo de armazenamento atual**|Exibe o modo de armazenamento atual da partição.<br /><br /> Observação: esse modo pode variar dependendo das configurações do cache pró-ativo da partição. Para obter mais informações sobre cache pró-ativo, consulte [Cache pró-ativo &#40;Partições&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).|  
|**Descrição**|Digite para alterar a descrição da partição.|  
|**Linhas estimadas**|Digite o número estimado de linhas na fonte de dados subjacente representada pela partição. Esse valor é usado durante o processamento para estimar o tempo e o armazenamento necessários para processar a partição.|  
|**Tamanho estimado**|Exibe o tamanho estimado da partição.|  
|**ID**|Exibe o identificador da partição.|  
|**Último processamento**|Exibe a data e a hora do último processamento da partição.|  
|**Última Atualização de Esquema**|Exibe a data e a hora da última atualização dos metadados da partição.|  
|**Nome**|Exibe o nome da partição.|  
|**Modo de processamento**|Selecione o modo de processamento da partição. Para obter mais informações sobre modos de processamento para [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] objetos, consulte [processamento de objeto de modelo Multidimensional](multidimensional-models/processing-a-multidimensional-model-analysis-services.md).|  
|**ID da fonte de dados remotos**|Exibe o identificador da fonte de dados remota da qual são recuperados os dados de origem da partição.<br /><br /> Observação: essa propriedade contém um valor apenas para partições remotas.|  
|**Fatia**|Exibe a expressão que identifica a fatia de dados representada pela partição.|  
|**Origem**|Exibe a tabela ou consulta que fornece os dados de origem da partição.|  
|**Estado**|Exibe o estado do processamento atual da partição.|  
|**Local de armazenamento**|Exibe a pasta na qual são armazenados os dados da partição.<br /><br /> Observação: essa propriedade conterá um valor apenas se um local de armazenamento diferente do local de armazenamento padrão for especificado para a instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].|  
|**Tipo**|Exibe o tipo da partição.|  
  
## <a name="see-also"></a>Consulte também  
 [Partições &#40;Analysis Services - dados multidimensionais&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [Partições remotas](multidimensional-models-olap-logical-cube-objects/partitions-remote-partitions.md)   
 [Caixa de diálogo Propriedades de partição &#40;SSMS&#41;](partition-properties-dialog-box-ssms.md)   
 [Seleção de &#40;caixa de diálogo Propriedades de partição&#41; &#40;SSMS&#41;](selection-partition-properties-dialog-box-ssms.md)   
 [Cache pró-ativo &#40;caixa de diálogo Propriedades de partição&#41; &#40;SSMS&#41;](proactive-caching-partition-properties-dialog-box-ssms.md)   
 [Configuração de erros para cubo, partição e processamento da dimensão &#40;SSAS - Multidimensional&#41;](multidimensional-models/error-configuration-for-cube-partition-and-dimension-processing.md)  
  
  
