---
title: "Propriedades personalizadas do destino de processamento de partição | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3eac4413-0c90-4b06-8f7e-d0d72f4d869d
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0a4ed16b65d8f6c7096551f7a55382e97213c9da
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="partition-processing-destination-custom-properties"></a>Propriedades personalizadas do destino Processamento de Partições
  O destino Processamento de Partições tem propriedades personalizadas e propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas do destino Processamento de Partições. Todas as propriedades são de leitura/gravação.  
  
|Propriedade|Tipo de Dados|Description|  
|--------------|---------------|-----------------|  
|ASConnectionString|Cadeia de caracteres|A cadeia de conexão com um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|KeyDuplicate|Inteiro (enumeração)|Quando UseDefaultConfiguration é **False**, um valor que indica como tratar erros de chave duplicada. Os valores possíveis são **IgnoreError** (0), **ReportAndContinue** (1) e **ReportAndStop** (2). O valor padrão dessa propriedade é **IgnoreError** (0).|  
|KeyErrorAction|Inteiro (enumeração)|Quando for UseDefaultConfiguration é **False**, um valor que indica como tratar erros de chave. Os valores possíveis são **ConvertToUnknown** (0) e **DiscardRecord** (1). O valor padrão dessa propriedade é **ConvertToUnknown** (0).|  
|KeyErrorLimit|Integer|Quando for UseDefaultConfiguration é **False**, o limite superior de erros de chave permitido.|  
|KeyErrorLimitAction|Inteiro (enumeração)|Quando UseDefaultConfiguration é **False**, um valor que indica a ação a ser realizada quando **KeyErrorLimit** for atingido. Os valores possíveis são **StopLogging** (1) e **StopProcessing** (0). O valor padrão dessa propriedade é **StopProcessing** (0).|  
|KeyErrorLogFile|Cadeia de caracteres|Quando UseDefaultConfiguration é **False**, o caminho e o nome do arquivo de log de erro.|  
|KeyNotFound|Inteiro (enumeração)|Quando for UseDefaultConfiguration é **False**, um valor que indica como tratar erros de chave ausentes. Os valores possíveis são **IgnoreError** (0), **ReportAndContinue** (1) e **ReportAndStop** (2). O valor padrão dessa propriedade é **ReportAndContinue** (1).|  
|NullKeyConvertedToUnknown|Inteiro (enumeração)|Quando UseDefaultConfiguration é **False**, um valor que indica como tratar chaves nulas convertidas para o valor desconhecido. Os valores possíveis são **IgnoreError** (0), **ReportAndContinue** (1) e **ReportAndStop** (2). O valor padrão dessa propriedade é **IgnoreError** (0).|  
|NullKeyNotAllowed|Inteiro (enumeração)|Quando UseDefaultConfiguration é **False**, um valor que indica como tratar nulos não permitidos. Os valores possíveis são **IgnoreError** (0), **ReportAndContinue** (1) e **ReportAndStop** (2). O valor padrão dessa propriedade é **ReportAndContinue** (1).|  
|ProcessType|Inteiro (enumeração)|O tipo de processamento de partições usado pela transformação. Os valores possíveis são **ProcessAdd** (1) (incremental), **ProcessFull** (0) e **ProcessUpdate** (2).|  
|UseDefaultConfiguration|Booliano|Um valor que especifica se a transformação usa a configuração de erro padrão. Se essa propriedade for **False**, a transformação usará os valores das propriedades personalizadas de tratamento de erros listadas nesta tabela, incluindo KeyDuplicate, KeyErrorAction e assim por diante.|  
  
 A entrada e as colunas de entrada do destino Processamento de Partições não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Destino de processamento de partições](../../integration-services/data-flow/partition-processing-destination.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades comuns](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
