---
title: Log de rastreamento de serviço do servidor de relatório | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- logs [Reporting Services], trace
- traces [Reporting Services]
- system information [Reporting Services]
- versions [Reporting Services]
ms.assetid: 2fde08b2-137d-4f4b-88e5-216030216e0d
caps.latest.revision: 49
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: d0fd7269ca32442cc53ad86d124db2eb8c1ff5d7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37270272"
---
# <a name="report-server-service-trace-log"></a>Log de rastreamento do serviço Servidor de Relatório
  O [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] log de rastreamento do servidor de relatório é um arquivo de texto ASCII que contém informações detalhadas para operações de serviço do servidor de relatório, incluindo as operações executadas pelo Web servidor de relatórios de serviço Gerenciador de relatórios e processamento em segundo plano. O arquivo de log de rastreamento inclui informações redundantes que estão registradas em outros arquivos de log, além de informações adicionais que, de outro modo, não seriam disponibilizadas. As informações do log de rastreamento podem ser úteis se você estiver depurando um aplicativo que inclui um servidor de relatório ou investigando um problema específico que foi gravado no log de evento ou de execução.  
  
> [!NOTE]  
>  Em versões anteriores, havia vários arquivos de log de rastreamento, um para cada aplicativo. Os arquivos a seguir são obsoletos e não são mais criados no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versões posteriores: reportserverwebapp _*\<timestamp >*. log, ReportServer _*\<timestamp >*. log e reportserverservice_main _*\<timestamp >*. log.  
  
 **Neste tópico:**  
  
-   [Onde estão os arquivos de log do servidor de relatório?](#bkmk_view_log)  
  
-   [Configurações de rastreamento](#bkmk_trace_configuration_settings)  
  
-   [Adicionando configurações personalizadas para especificar um local de arquivo de despejo](#bkmk_add_custom)  
  
-   [Campos de arquivo de log](#bkmk_log_file_fields)  
  
##  <a name="bkmk_view_log"></a> Onde estão os arquivos de log do Servidor de Relatório?  
 Os arquivos de log de rastreamento são `ReportServerService_<timestamp>.log` e estão localizados na seguinte pasta:  
  
 `C:\Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\LogFiles`  
  
 O log de rastreamento é criado diariamente, começando na primeira entrada que ocorre após a meia-noite (horário local), e sempre que o serviço é reiniciado. O carimbo de data e hora é baseado em UTC (Tempo Universal Coordenado). O arquivo está em formato pt-BR. Por padrão, os logs de rastreamento são limitados a 32 megabytes e, por padrão, excluídos depois de 14 dias.  
  
 Exibir um breve vídeo que demonstra o uso do Microsoft Power Query para exibir arquivos de log [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] .  
  
 ![Exibir um vídeo sobre logs de SSRS e Power Query](../media/generic-video-thumbnail.png "exibir um vídeo sobre logs de SSRS e Power Query")  
  
##  <a name="bkmk_trace_configuration_settings"></a> Configurações de rastreamento  
 O comportamento do log de rastreamento é gerenciado no arquivo de configuração **ReportingServicesrService.exe.config**. O arquivo de configuração está localizado no caminho de pasta a seguir:  
  
 `\Program Files\Microsoft SQL Server\MSRS12.<instance name>\Reporting Services\ReportServer\bin`.  
  
 O exemplo a seguir ilustra a estrutura XML das configurações `RStrace`. O valor para `DefaultTraceSwitch` determina o tipo de informação que é adicionado ao log. Exceto para o `Components` de atributo, os valores para `RStrace` são os mesmos em todos os arquivos de configuração.  
  
```  
<system.diagnostics>  
      <switches>  
          <add name="DefaultTraceSwitch" value="3" />  
      </switches>  
</system.diagnostics>  
<RStrace>  
      <add name="FileName" value="ReportServerService_" />  
      <add name="FileSizeLimitMb" value="32" />  
      <add name="KeepFilesForDays" value="14" />  
      <add name="Prefix" value="tid, time" />  
      <add name="TraceListeners" value="file" />  
      <add name="TraceFileMode" value="unique" />  
      <add name="Components" value="all" />  
</RStrace>  
```  
  
 A tabela a seguir fornece informações sobre cada configuração.  
  
|Configuração|Description|  
|-------------|-----------------|  
|`RStrace`|Especifica os namespaces usados para erros e rastreamento.|  
|`DefaultTraceSwitch`|Especifica o nível de informações que é relatado no log de rastreamento ReportServerService. Cada nível inclui as informações relatadas por todos os níveis de baixa numeração. A desabilitação do rastreamento não é recomendada. Os valores válidos são:<br /><br /> 0 = Desabilita o rastreamento. O arquivo de log ReportServerService é habilitado por padrão. Para desativá-lo, defina o nível de rastreamento como 0.<br /><br /> 1 = Exceções e reinicializações<br /><br /> 2 = Exceções, reinicializações, avisos<br /><br /> 3 = Exceções, reinicializações, avisos, mensagens de status (padrão)<br /><br /> 4 = Modo detalhado|  
|**FileName**|Especifica a primeira parte do nome de arquivo de log. O valor especificado por `Prefix` completa o resto do nome.|  
|**FileSizeLimitMb**|Especifica o limite superior do tamanho do log de rastreamento. O arquivo é medido em megabytes. Os valores válidos são de 0 a um inteiro máximo. O valor padrão é 32. Se você especificar 0 ou um número negativo, o servidor de relatório tratará o valor como 1.<br /><br /> Você pode controlar o tamanho do arquivo definindo níveis de rastreamento (de 0 a 4) para controlar a quantidade de conteúdo registrado. Você também pode especificar quais componentes devem ser rastreados. Se o limite máximo do arquivo de log for atingido antes da data de validade de 14 dias, as entradas mais antigas serão substituídas pelas mais novas.|  
|**KeepFilesForDays**|Especifica o número de dias depois dos quais um arquivo de log de rastreamento será excluído. Os valores válidos são de 0 a um inteiro máximo. O valor padrão é 14. Se você especificar 0 ou um número negativo, o servidor de relatório tratará o valor como 1.|  
|`Prefix`|Especifica um valor gerado que diferencia uma instância de log de outra. Por padrão, os valores do carimbo de data/hora são adicionados aos nomes de arquivo de log de rastreamento. Esse valor é definido como " tid, time ". Não modifique esta configuração.|  
|**TraceListeners**|Especifica um destino para a saída do conteúdo do log de rastreamento. Você pode especificar vários destinos usando uma vírgula para separar cada um. Os valores válidos são:<br /><br /> DebugWindow<br /><br /> File (padrão)<br /><br /> StdOut|  
|**TraceFileMode**|Especifica se os logs de rastreamento contêm dados para um período de 24 horas. Um log de rastreamento exclusivo deve existir para cada componente em cada dia. Esse valor é definido como "Unique (default)". Não modifique esse valor.|  
|`Components`|Especifica os componentes para os quais as informações do log de rastreamento são geradas e o nível de rastreamento neste formato:<br /><br /> \<component category>:\<tracelevel><br /><br /> As categorias de componente podem ser definidas como:<br />`All` é usado para rastrear atividades gerais dos servidor de relatório para todos os processos que não estão incluídos em categorias específicas.<br />`RunningJobs` é usado para rastrear uma operação de relatório ou assinatura em andamento.<br />`SemanticQueryEngine` é usado para rastrear uma consulta semântica que é processada quando um usuário executa a exploração de dados ad hoc em um relatório baseado em modelos. <br />`SemanticModelGenerator` é usado para rastrear a geração do modelo.<br />`http` é usado para habilitar o arquivo de log HTTP do servidor de relatório. Para obter mais informações, consulte [Log de HTTP do servidor de relatório](report-server-http-log.md).<br /><br /> <br /><br /> Os valores válidos de nível de rastreamento são:<br /><br /> 0 = Desabilita o rastreamento<br /><br /> 1 = Exceções e reinicializações<br /><br /> 2 = Exceções, reinicializações, avisos<br /><br /> 3 = Exceções, reinicializações, avisos, mensagens de status (padrão)<br /><br /> 4 = Modo detalhado<br /><br /> O valor padrão do servidor de relatório é: "all:3".<br /><br /> Você pode especificar todos ou alguns dos componentes (`all`, `RunningJobs`, `SemanticQueryEngine`, `SemanticModelGenerator`). Se não desejar gerar informações para um componente específico, desabilite o rastreamento desse componente (por exemplo, "SemanticModelGenerator:0"). Não desabilite o rastreamento para `all`.<br /><br /> Se você não adicionar um nível de rastreamento ao componente, o valor especificado para `DefaultTraceSwitch` será usado. Por exemplo, se você especificar "all,RunningJobs,SemanticQueryEngine,SemanticModelGenerator", todos os componentes utilizarão o nível de rastreamento padrão.<br /><br /> Defina "SemanticQueryEngine:4" se desejar exibir as instruções Transact-SQL geradas para cada consulta semântica. As instruções Transact-SQL são registradas no log de rastreamento. O exemplo a seguir ilustra a configuração que adiciona instruções Transact-SQL ao log:<br /><br /> \<add name="Components" value="all,SemanticQueryEngine:4" />|  
  
##  <a name="bkmk_add_custom"></a> Adicionando configurações personalizadas para especificar um local de arquivo de despejo  
 Você pode adicionar uma configuração personalizada para definir o local usado pela ferramenta Dr. Watson para Windows usa para armazenar arquivos de despejo. A configuração personalizada é `Directory`. O exemplo a seguir fornece uma ilustração de como esta configuração é especificada na seção `RStrace`:  
  
```  
<add name="Directory" value="U:\logs\" />  
```  
  
 Para obter mais informações, consulte o [Artigo 913046 da Base de Dados de Conhecimento](http://support.microsoft.com/?kbid=913046) no site do [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
##  <a name="bkmk_log_file_fields"></a> Campos do arquivo de log  
 Os campos a seguir podem ser localizados em um log de rastreamento:  
  
-   Informações de sistema, incluindo o sistema operacional, a versão, o número de processadores e a memória.  
  
-   Componente do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] e informações de versão.  
  
-   Eventos registrados no log de aplicativo.  
  
-   Exceções geradas pelo servidor de relatório.  
  
-   Avisos sobre poucos recursos registrados por um servidor de relatório.  
  
-   Envelopes SOAP de entrada e envelopes SOAP de saída resumidos.  
  
-   Cabeçalho HTTP, rastreamento de pilha e informações de rastreamento de depuração.  
  
 Você pode revisar as informações do log de rastreamento para determinar se uma entrega de relatório ocorreu, quem recebeu o relatório e quantas tentativas de entrega foram feitas. Os logs de rastreamento também registram atividades de execução de relatório e as variáveis de ambiente que estão habilitadas durante o processamento do relatório. Erros e exceções também são incluídos em logs de rastreamento. Por exemplo, você pode localizar relatório de erros de tempo limite (indicados como uma `ThreadAbortExceptions` entrada).  
  
## <a name="see-also"></a>Consulte também  
 [Fontes e arquivos de log do Reporting Services](../report-server/reporting-services-log-files-and-sources.md)   
 [Referência de erros e eventos &#40;Reporting Services&#41;](../troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  
