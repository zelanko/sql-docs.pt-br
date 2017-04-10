---
title: "Propriedades personalizadas do destino de processamento de dimens&#245;es | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9700f663-53f2-49b6-b1ef-92c7b752d6a1
caps.latest.revision: 6
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 6
---
# Propriedades personalizadas do destino de processamento de dimens&#245;es
  O destino Processamento de Dimensões tem propriedades personalizadas e propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas do destino Processamento de Dimensões. Todas as propriedades são de leitura/gravação.  
  
|Propriedade|Tipo de Dados|Description|  
|--------------|---------------|-----------------|  
|ASConnectionString|Cadeia de caracteres|A cadeia de caracteres de conexão com uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou com um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|KeyDuplicate|Inteiro (enumeração)|Quando UseDefaultConfiguration é **False**, um valor que indica como tratar erros de chave duplicada. Os valores possíveis são **IgnoreError** (0), **ReportAndContinue** (1) e **ReportAndStop** (2). O valor padrão dessa propriedade é **IgnoreError** (0).|  
|KeyErrorAction|Inteiro (enumeração)|Quando UseDefaultConfiguration for **False**, um valor que indica como tratar erros de chave. Os valores possíveis são **ConvertToUnknown** (0) e **DiscardRecord** (1). O valor padrão dessa propriedade é **ConvertToUnknown** (0).|  
|KeyErrorLimit|Integer|Quando UseDefaultConfiguration for **False**, o limite superior de erros de chave permitido.|  
|KeyErrorLimitAction|Inteiro (enumeração)|Quando UseDefaultConfiguration é **False**, um valor que indica a ação a ser realizada quando **KeyErrorLimit** for atingido. Os valores possíveis são **StopLogging** (1) e **StopProcessing** (0). O valor padrão dessa propriedade é **StopProcessing** (0).|  
|KeyErrorLogFile|Cadeia de caracteres|Quando UseDefaultConfiguration é **False**, o caminho e o nome do arquivo de log de erro.|  
|KeyNotFound|Inteiro (enumeração)|Quando for UseDefaultConfiguration é **False**, um valor que indica como tratar erros de chave ausentes. Os valores possíveis são **IgnoreError** (0), **ReportAndContinue** (1) e **ReportAndStop** (2). O valor padrão dessa propriedade é **IgnoreError** (0).|  
|NullKeyConvertedToUnknown|Inteiro (enumeração)|Quando UseDefaultConfiguration é **False**, um valor que indica como tratar chaves nulas convertidas para o valor desconhecido. Os valores possíveis são **IgnoreError** (0), **ReportAndContinue** (1) e **ReportAndStop** (2). O valor padrão dessa propriedade é **IgnoreError** (0).|  
|NullKeyNotAllowed|Inteiro (enumeração)|Quando UseDefaultConfiguration é **False**, um valor que indica como tratar nulos não permitidos. Os valores possíveis são **IgnoreError** (0), **ReportAndContinue** (1) e **ReportAndStop** (2). O valor padrão dessa propriedade é **IgnoreError** (0).|  
|ProcessType|Inteiro (enumeração)|O tipo de processamento de dimensões usado pela transformação. Os valores são **ProcessAdd** (1) (incremental), **ProcessFull** (0) e **ProcessUpdate** (2).|  
|UseDefaultConfiguration|Booliano|Um valor que especifica se a transformação usa a configuração de erro padrão. Se essa propriedade for **False**, a transformação incluirá informações sobre processamento de erros.|  
  
 A entrada e as colunas de entrada do destino Processamento de Dimensões não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Destino de processamento de dimensões](../../integration-services/data-flow/dimension-processing-destination.md).  
  
## Consulte também  
 [Propriedades comuns](../Topic/Common%20Properties.md)  
  
  