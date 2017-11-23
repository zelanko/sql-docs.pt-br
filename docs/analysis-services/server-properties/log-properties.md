---
title: Propriedades de log | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: server-properties
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- QueryLogFileSize property
- QueryLogTableName property
- TraceBackgroundDistributionPeriod property
- TraceMaxRowsetSize property
- NullKeyConvertedToUnknown property
- CrashReportsFolder property
- TraceDefinitionFile property
- SQLDumperFlagsOn property
- KeyErrorLimit property
- SnapshotDefinitionFile property
- MinidumpErrorList property
- ErrorLogFileName property
- KeyDuplicate property
- IgnoreDataTruncation property
- logs [Analysis Services]
- Enabled property
- FileSizeMB property
- TraceFileWriteTrailerPeriod property
- TraceQueryResponseTextChunkSize property
- File property
- FileBufferSize property
- TraceRowsetBackgroundFlushPeriod property
- ErrorLogFileSize property
- TraceRequestParameters property
- KeyErrorLimitAction property
- CreateQueryLogTable property
- LogDir property
- TraceBackgroundFlushPeriod property
- TraceFileBufferSize property
- SQLDumperFlagsOff property
- QueryLogConnectionString property
- KeyNotFound property
- KeyErrorLogFile property
- TraceReportFQDN property
- KeyErrorAction property
- QueryLogFileName property
- MessageLogs property
- MiniDumpFlagsOn property
- SnapshotFrequencySec property
- QueryLogSampling property
- CreateAndSendCrashReports property
- LogDurationSec property
ms.assetid: 33fd90ee-cead-48f0-8ff9-9b458994c766
caps.latest.revision: "23"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 773aa4d93c8c6621184f8288964bd80d5efd826c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="log-properties"></a>Propriedades do log
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oferece suporte às propriedades do servidor de log listadas nas tabelas a seguir. Para obter mais informações sobre propriedades adicionais do servidor e como defini-las, consulte [Propriedades do servidor do Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
## <a name="general"></a>Geral  
 **Arquivo**  
 Uma propriedade de cadeia de caracteres que identifica o nome do arquivo de log do servidor. Esta propriedade só se aplicará quando um arquivo de disco for usado para log, em vez de uma tabela de banco de dados (o comportamento padrão).  
  
 O valor padrão desta propriedade é msmdsrv.log.  
  
 **FileBufferSize**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MessageLogs**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="error-log"></a>Log de erros  
 Você pode definir essas propriedades no nível da instância de servidor para modificar os valores padrão para a Configuração de Erros que aparece em outras ferramentas e designers. Consulte [configuração de erro para o cubo, partição e o processamento da dimensão &#40; SSAS Multidimensional &#41; ](../../analysis-services/multidimensional-models/error-configuration-for-cube-partition-and-dimension-processing.md) e <xref:Microsoft.AnalysisServices.MiningStructure.ErrorConfiguration%2A> para obter mais informações.  
  
 **ErrorLog\ErrorLogFileName**  
 Uma propriedade usada como padrão durante a operação de processamento executada pelo servidor.  
  
 **ErrorLog\ErrorLogFileSize**  
 Uma propriedade usada como padrão durante a operação de processamento executada pelo servidor.  
  
 **ErrorLog\KeyErrorAction**  
 Especifica a ação executada pelo servidor quando um erro **KeyNotFound** ocorre. As respostas válidas para esse erro incluem:  
  
-   **ConvertToUnknown** informa ao servidor para alocar o valor de chave de erro para o membro desconhecido.  
  
-   **DiscardRecord** informa ao servidor para excluir o registro.  
  
 **ErrorLog\KeyErrorLogFile**  
 Esse é um nome de arquivo definido pelo usuário que deve ter uma extensão de arquivo .log, localizado em uma pasta na qual a conta de serviço tem permissões de leitura/gravação. Este arquivo de log conterá somente os erros gerados durante o processamento. Use o Flight Recorder se precisar de informações mais detalhadas.  
  
 **ErrorLog\KeyErrorLimit**  
 Esse é o número máximo de erros de integridade de dados que o servidor permitirá antes da falha do processamento. Um valor -1 indica que não há limite. O padrão é 0, o que significa parar o processamento depois do primeiro erro. Você também pode defini-lo como um número inteiro.  
  
 **ErrorLog\KeyErrorLimitAction**  
 Especifica a ação executada pelo servidor quando o número de erros de chave atingiu o limite superior. As respostas válidas para essa ação incluem:  
  
-   **StopProcessing** informa ao servidor para parar o processamento quando o limite de erros for atingido.  
  
-   **StopLogging** informa ao servidor para parar o log de erros quando o limite de erros for atingido, mas permitir que o processamento continue.  
  
 **ErrorLog\ LogErrorTypes\KeyNotFound**  
 Especifica a ação executada pelo servidor quando um erro **KeyNotFound** ocorre. As respostas válidas para esse erro incluem:  
  
-   **IgnoreError** informa ao servidor para continuar o processamento sem registrar em log o erros ou contá-lo até o limite de erros de chave. Ao ignorar o erro, você simplesmente permite que o processamento continue sem adicioná-lo à contagem de erros ou registrá-lo em log na tela ou no arquivo de log. O registro em questão tem um problema de integridade de dados e não pode ser adicionado ao banco de dados. O registro será descartado ou agregado ao Membro desconhecido, conforme determinado pela propriedade **KeyErrorAction** .  
  
-   **ReportAndContinue** informa ao servidor para registrar em log o erro, contá-lo até o limite de erros de chave e continuar o processamento. O registro que aciona o erro é descartado ou convertido no Membro Desconhecido.  
  
-   **ReportAndStop** informa ao servidor para registrar em log o erro e parar o processamento imediatamente, independentemente do limite de erros de chave. O registro que aciona o erro é descartado ou convertido no Membro Desconhecido.  
  
 **ErrorLog\ LogErrorTypes\KeyDuplicate**  
 Especifica a ação executada pelo servidor quando uma chave duplicada é encontrada. Os valores válidos incluem **IgnoreError** para continuar o processamento como se o erro não tivesse ocorrido, **ReportAndContinue** para registrar em log o erro e continuar o processamento, e **ReportAndStop** para registrar em log o erro e parar o processamento imediatamente, mesmo se a contagem de erro estiver abaixo do limite de erros.  
  
 **ErrorLog\ LogErrorTypes\NullKeyConvertedToUnknown**  
 Especifica a ação executada pelo servidor quando uma chave nula tiver sido convertida em Membro Desconhecido. Os valores válidos incluem **IgnoreError** para continuar o processamento como se o erro não tivesse ocorrido, **ReportAndContinue** para registrar em log o erro e continuar o processamento, e **ReportAndStop** para registrar em log o erro e parar o processamento imediatamente, mesmo se a contagem de erro estiver abaixo do limite de erros.  
  
 **ErrorLog\ LogErrorTypes\NullKeyNotAllowed**  
 Especifica a ação executada pelo servidor quando **NullProcessing** estiver definido como **Error** para um atributo de dimensão. Um erro é gerado quando um valor nulo não é permitido em um determinado atributo. Esta propriedade de configuração de erro informa a próxima etapa, que é relatar o erro e continuar o processamento até que o limite de erros seja atingido. Os valores válidos incluem **IgnoreError** para continuar o processamento como se o erro não tivesse ocorrido, **ReportAndContinue** para registrar em log o erro e continuar o processamento, e **ReportAndStop** para registrar em log o erro e parar o processamento imediatamente, mesmo se a contagem de erro estiver abaixo do limite de erros.  
  
 **ErrorLog\ LogErrorTypes\CalculationError**  
 Uma propriedade usada como padrão durante a operação de processamento executada pelo servidor.  
  
 **ErrorLog\IgnoreDataTruncation**  
 Uma propriedade usada como padrão durante a operação de processamento executada pelo servidor.  
  
## <a name="exception"></a>Exceção  
 **Exception\CreateAndSendCrashReports**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Exception\CrashReportsFolder**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Exception\SQLDumperFlagsOn**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Exception\SQLDumperFlagsOff**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Exception\MiniDumpFlagsOn**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Exception\MinidumpErrorList**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="flight-recorder"></a>Flight Recorder  
 **FlightRecorder\Enabled**  
 Uma propriedade booliana que indica se o recurso de flight recorder está habilitado.  
  
 **FlightRecorder\FileSizeMB**  
 Uma propriedade de inteiro de 32 bits assinada que define o tamanho do arquivo de disco do flight recorder, em megabytes.  
  
 **FlightRecorder\LogDurationSec**  
 Uma propriedade de inteiro de 32 bits assinada que define a frequência com que o flight recorder é rodado, em segundos.  
  
 **FlightRecorder\SnapshotDefinitionFile**  
 Uma propriedade de cadeia de caracteres que define o nome do arquivo de definição de instantâneo, que contém comandos de identificação emitidos ao servidor quando um instantâneo é tirado.  
  
 O valor padrão desta propriedade é em branco, que por sua vez, assume o nome de arquivo FlightRecorderSnapshotDef.xml como padrão.  
  
 **FlightRecorder\SnapshotFrequencySec**  
 Uma propriedade de inteiro de 32 bits assinada que define a frequência de instantâneo, em segundos.  
  
 **FlightRecorder\TraceDefinitionFile**  
 Uma propriedade de cadeia de caracteres que especifica o nome do arquivo de definição de rastreamento do flight recorder.  
  
 O valor padrão desta propriedade é em branco, que por sua vez, assume FlightRecorderTraceDef.xml como padrão.  
  
## <a name="query-log"></a>Log de consultas  
 **Aplica-se a:** somente modo de servidor multidimensional  
  
 **QueryLog\QueryLogFileName**  
 Uma propriedade de cadeia de caracteres que especifica o nome do arquivo de log de consultas. Esta propriedade só se aplicará quando um arquivo de disco for usado para log, em vez de uma tabela de banco de dados (o comportamento padrão).  
  
 **QueryLog\QueryLogSampling**  
 Uma propriedade de inteiro de 32 bits assinada que especifica a taxa de amostragem do log de consultas.  
  
 O valor padrão desta propriedade é 10, o que significa que 1 entre cada 10 consultas de servidor é registrada.  
  
 **QueryLog\QueryLogFileSize**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **QueryLog\QueryLogConnectionString**  
 Uma propriedade de cadeia de caracteres que especifica a conexão com o banco de dados de log de consultas.  
  
 **QueryLog\QueryLogTableName**  
 Uma propriedade de cadeia de caracteres que especifica o nome da tabela de log de consultas.  
  
 O valor padrão desta propriedade é OlapQueryLog.  
  
 **QueryLog\CreateQueryLogTable**  
 Uma propriedade booliana que especifica se deve ser criada a tabela de log de consultas.  
  
 O valor padrão desta propriedade é falso, o que indica que o servidor não criará a tabela de log automaticamente e não registrará os eventos de consulta.  
  
> [!NOTE]  
>  Para obter mais informações sobre como configurar o log de consultas, consulte [Configurar o log de consultas do Analysis Services](http://go.microsoft.com/fwlink/?LinkId=81890).  
  
## <a name="trace"></a>Rastreamento  
 **Trace\TraceBackgroundDistributionPeriod**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Trace\TraceBackgroundFlushPeriod**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Trace\TraceFileBufferSize**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Trace\TraceFileWriteTrailerPeriod**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Trace\TraceMaxRowsetSize**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Trace\TraceProtocolTraffic**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Trace\TraceQueryResponseTextChunkSize**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Trace\TraceReportFQDN**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Trace\TraceRequestParameters**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Trace\TraceRowsetBackgroundFlushPeriod**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades do servidor do Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Determina o Modo de Servidor de uma instância do Analysis Services.](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
