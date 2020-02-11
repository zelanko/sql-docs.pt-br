---
title: Propriedades personalizadas do destino de processamento de partição | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 3eac4413-0c90-4b06-8f7e-d0d72f4d869d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3dbab24f756498d7427f9961e4176249daac8dfb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62770942"
---
# <a name="partition-processing-destination-custom-properties"></a>Propriedades personalizadas do destino Processamento de Partições
  O destino Processamento de Partições tem propriedades personalizadas e propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas do destino Processamento de Partições. Todas as propriedades são de leitura/gravação.  
  
|Propriedade|Tipo de Dados|DESCRIÇÃO|  
|--------------|---------------|-----------------|  
|ASConnectionString|String|A cadeia de conexão com um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|KeyDuplicate|Inteiro (enumeração)|Quando UseDefaultConfiguration é `False`, um valor que indica como tratar erros de chave duplicada. Os valores possíveis são `IgnoreError` (0), `ReportAndContinue` (1) e `ReportAndStop` (2). O valor padrão dessa propriedade é `IgnoreError` (0).|  
|KeyErrorAction|Inteiro (enumeração)|Quando UseDefaultConfiguration é `False`, um valor que indica como lidar com erros de chave. Os valores possíveis são `ConvertToUnknown` (0) e `DiscardRecord` (1). O valor padrão dessa propriedade é `ConvertToUnknown` (0).|  
|KeyErrorLimit|Integer|Quando UseDefaultConfiguration é `False`, o limite superior de erros de chave que são permitidos.|  
|KeyErrorLimitAction|Inteiro (enumeração)|Quando UseDefaultConfiguration é `False`, um valor que indica a ação a ser tomada `KeyErrorLimit` quando é atingido. Os valores possíveis são `StopLogging` (1) e `StopProcessing` (0). O valor padrão dessa propriedade é `StopProcessing` (0).|  
|KeyErrorLogFile|String|Quando UseDefaultConfiguration é `False`, o caminho e o nome de arquivo do arquivo de log de erros.|  
|KeyNotFound|Inteiro (enumeração)|Quando UseDefaultConfiguration é `False`, um valor que indica como tratar erros de chave ausentes. Os valores possíveis são `IgnoreError` (0), `ReportAndContinue` (1) e `ReportAndStop` (2). O valor padrão desta propriedade é `ReportAndContinue` (1).|  
|NullKeyConvertedToUnknown|Inteiro (enumeração)|Quando UseDefaultConfiguration é `False`, um valor que indica como lidar com chaves nulas convertidas para o valor desconhecido. Os valores possíveis são `IgnoreError` (0), `ReportAndContinue` (1) e `ReportAndStop` (2). O valor padrão dessa propriedade é `IgnoreError` (0).|  
|NullKeyNotAllowed|Inteiro (enumeração)|Quando UseDefaultConfiguration é `False`, um valor que indica como tratar nulos não permitidos. Os valores possíveis são `IgnoreError` (0), `ReportAndContinue` (1) e `ReportAndStop` (2). O valor padrão desta propriedade é `ReportAndContinue` (1).|  
|ProcessType|Inteiro (enumeração)|O tipo de processamento de partições usado pela transformação. Os valores possíveis são `ProcessAdd` (1) (incremental), `ProcessFull` (0) e `ProcessUpdate` (2).|  
|UseDefaultConfiguration|Boolean|Um valor que especifica se a transformação usa a configuração de erro padrão. Se essa propriedade for `False`, a transformação usará os valores das propriedades personalizadas de tratamento de erros listadas nesta tabela, incluindo KeyDuplicate, keyerroaction e assim por diante.|  
  
 A entrada e as colunas de entrada do destino Processamento de Partições não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Destino de processamento de partições](partition-processing-destination.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades comuns](../common-properties.md)  
  
  
