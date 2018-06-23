---
title: Propriedades personalizadas do destino de processamento de partição | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3eac4413-0c90-4b06-8f7e-d0d72f4d869d
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 2724682cebfcae1e5c6a14b9c7cd815c96ad4a7c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019404"
---
# <a name="partition-processing-destination-custom-properties"></a>Propriedades personalizadas do destino Processamento de Partições
  O destino Processamento de Partições tem propriedades personalizadas e propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas do destino Processamento de Partições. Todas as propriedades são de leitura/gravação.  
  
|Propriedade|Tipo de Dados|Description|  
|--------------|---------------|-----------------|  
|ASConnectionString|Cadeia de caracteres|A cadeia de conexão com um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|KeyDuplicate|Inteiro (enumeração)|Quando for UseDefaultConfiguration `False`, um valor que indica como tratar erros de chave duplicada. Os valores possíveis são `IgnoreError` (0), `ReportAndContinue` (1), e `ReportAndStop` (2). O valor padrão dessa propriedade é `IgnoreError` (0).|  
|KeyErrorAction|Inteiro (enumeração)|Quando for UseDefaultConfiguration `False`, um valor que indica como tratar erros de chave. Os valores possíveis são `ConvertToUnknown` (0) e `DiscardRecord` (1). O valor padrão dessa propriedade é `ConvertToUnknown` (0).|  
|KeyErrorLimit|Integer|Quando for UseDefaultConfiguration `False`, o limite superior de erros de chave que são permitidos.|  
|KeyErrorLimitAction|Inteiro (enumeração)|Quando for UseDefaultConfiguration `False`, um valor que indica a ação a ser realizada quando `KeyErrorLimit` for atingido. Os valores possíveis são `StopLogging` (1) e `StopProcessing` (0). O valor padrão dessa propriedade é `StopProcessing` (0).|  
|KeyErrorLogFile|Cadeia de caracteres|Quando for UseDefaultConfiguration `False`, o nome de arquivo e caminho do arquivo de log de erro.|  
|KeyNotFound|Inteiro (enumeração)|Quando for UseDefaultConfiguration `False`, um valor que indica como tratar erros de chave não tem. Os valores possíveis são `IgnoreError` (0), `ReportAndContinue` (1), e `ReportAndStop` (2). O valor padrão dessa propriedade é `ReportAndContinue` (1).|  
|NullKeyConvertedToUnknown|Inteiro (enumeração)|Quando for UseDefaultConfiguration `False`, um valor que indica como controlar chaves nulas convertidas no valor desconhecido. Os valores possíveis são `IgnoreError` (0), `ReportAndContinue` (1), e `ReportAndStop` (2). O valor padrão dessa propriedade é `IgnoreError` (0).|  
|NullKeyNotAllowed|Inteiro (enumeração)|Quando for UseDefaultConfiguration `False`, um valor que indica como controlar nulos desaprovados. Os valores possíveis são `IgnoreError` (0), `ReportAndContinue` (1), e `ReportAndStop` (2). O valor padrão dessa propriedade é `ReportAndContinue` (1).|  
|ProcessType|Inteiro (enumeração)|O tipo de processamento de partições usado pela transformação. Os valores possíveis são `ProcessAdd` (1) (incremental), `ProcessFull` (0) e `ProcessUpdate` (2).|  
|UseDefaultConfiguration|Booliano|Um valor que especifica se a transformação usa a configuração de erro padrão. Se essa propriedade for `False`, a transformação usa os valores das propriedades personalizadas de tratamento de erros listados nesta tabela, incluindo KeyDuplicate, KeyErrorAction e assim por diante.|  
  
 A entrada e as colunas de entrada do destino Processamento de Partições não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Destino de processamento de partições](partition-processing-destination.md).  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades comuns](../common-properties.md)  
  
  