---
title: Propriedades personalizadas do destino de processamento de partição | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 3eac4413-0c90-4b06-8f7e-d0d72f4d869d
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9139ff2af92d861f356514e9e78073c3e858ab81
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48048586"
---
# <a name="partition-processing-destination-custom-properties"></a>Propriedades personalizadas do destino Processamento de Partições
  O destino Processamento de Partições tem propriedades personalizadas e propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas do destino Processamento de Partições. Todas as propriedades são de leitura/gravação.  
  
|Propriedade|Tipo de Dados|Description|  
|--------------|---------------|-----------------|  
|ASConnectionString|Cadeia de caracteres|A cadeia de conexão com um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|KeyDuplicate|Inteiro (enumeração)|Quando UseDefaultConfiguration é `False`, um valor que indica como tratar erros de chave duplicada. Os valores possíveis são `IgnoreError` (0), `ReportAndContinue` (1), e `ReportAndStop` (2). O valor padrão dessa propriedade é `IgnoreError` (0).|  
|KeyErrorAction|Inteiro (enumeração)|Quando UseDefaultConfiguration é `False`, um valor que indica como tratar erros de chave. Os valores possíveis são `ConvertToUnknown` (0) e `DiscardRecord` (1). O valor padrão dessa propriedade é `ConvertToUnknown` (0).|  
|KeyErrorLimit|Integer|Quando UseDefaultConfiguration é `False`, o limite superior de erros de chave que são permitidos.|  
|KeyErrorLimitAction|Inteiro (enumeração)|Quando for UseDefaultConfiguration `False`, um valor que indica a ação a ser tomada quando `KeyErrorLimit` for atingido. Os valores possíveis são `StopLogging` (1) e `StopProcessing` (0). O valor padrão dessa propriedade é `StopProcessing` (0).|  
|KeyErrorLogFile|Cadeia de caracteres|Quando UseDefaultConfiguration é `False`, o nome de arquivo e caminho do arquivo de log de erro.|  
|KeyNotFound|Inteiro (enumeração)|Quando UseDefaultConfiguration é `False`, um valor que indica como tratar erros de chave ausentes. Os valores possíveis são `IgnoreError` (0), `ReportAndContinue` (1), e `ReportAndStop` (2). O valor padrão dessa propriedade é `ReportAndContinue` (1).|  
|NullKeyConvertedToUnknown|Inteiro (enumeração)|Quando UseDefaultConfiguration é `False`, um valor que indica como tratar chaves nulas convertidas no valor desconhecido. Os valores possíveis são `IgnoreError` (0), `ReportAndContinue` (1), e `ReportAndStop` (2). O valor padrão dessa propriedade é `IgnoreError` (0).|  
|NullKeyNotAllowed|Inteiro (enumeração)|Quando UseDefaultConfiguration é `False`, um valor que indica como controlar nulos desaprovados. Os valores possíveis são `IgnoreError` (0), `ReportAndContinue` (1), e `ReportAndStop` (2). O valor padrão dessa propriedade é `ReportAndContinue` (1).|  
|ProcessType|Inteiro (enumeração)|O tipo de processamento de partições usado pela transformação. Os valores possíveis são `ProcessAdd` (1) (incremental), `ProcessFull` (0) e `ProcessUpdate` (2).|  
|UseDefaultConfiguration|Booliano|Um valor que especifica se a transformação usa a configuração de erro padrão. Se essa propriedade for `False`, a transformação usa os valores das propriedades personalizadas de tratamento de erros listadas nesta tabela, incluindo KeyDuplicate, KeyErrorAction e assim por diante.|  
  
 A entrada e as colunas de entrada do destino Processamento de Partições não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Destino de processamento de partições](partition-processing-destination.md).  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades comuns](../common-properties.md)  
  
  
