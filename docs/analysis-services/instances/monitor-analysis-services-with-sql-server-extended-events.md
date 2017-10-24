---
title: Monitorar o Analysis Services com eventos estendidos do SQL Server | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- XEvents
- Sql13.ssms.XeASNewEventSession.General.f1
- Sql13.ssms.XeASNewEventSession.Events.f1
- Sql13.ssms.XeASNewEventSession.Targets.f1
- Sql13.ssms.XeASNewEventSession.Advanced.f1
ms.assetid: b57cc2fe-52dc-4fa9-8554-5a866e25c6d7
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cec6da660c202dfde5a1169dd34397fca5c51207
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="monitor-analysis-services-with-sql-server-extended-events"></a>Monitorar o Analysis Services com Eventos Estendidos do SQL Server
  Os Eventos Estendidos (*xEvents*) são um sistema leve de monitoramento de desempenho e rastreamento que usa pouquíssimos recursos do sistema, o que o torna uma ferramenta ideal para problemas de diagnóstico nos servidores de teste e de produção. Além disso, é altamente escalonável, configurável e mais fácil de usar no SQL Server 2016 por meio do novo suporte interno de ferramenta. No SQL Server Management Studio, em conexões com instâncias do Analysis Services, você pode configurar, executar e monitorar um rastreamento em tempo real, semelhante ao uso do SQL Server Profiler. A adição de ferramentas melhores deve tornar o xEvents uma substituição mais adequada para o SQL Server Profiler e criar mais simetria na forma de diagnosticar problemas relacionados ao mecanismo de banco de dados e às cargas de trabalho do Analysis Services.  
  
 Além do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], você também pode configurar sessões de Eventos Estendidos do  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] da maneira antiga, por meio de scripts de XMLA, da mesma forma que era compatível em versões anteriores.  
  
 Todos os eventos do Analysis Services podem ser captados e destinados a usuários específicos, conforme definido em [Eventos Estendidos](../../relational-databases/extended-events/extended-events.md).  
  
> [!NOTE]  
>  Assista a este [breve vídeo de introdução](https://www.youtube.com/watch?v=ja2mOHWRVC0&index=1&list=PLv2BtOtLblH1YvzQ5YnjfQFr_oKEvMk19) ou leia a [postagem do blog de suporte](http://blogs.msdn.com/b/analysisservices/archive/2015/09/22/using-extended-events-with-sql-server-analysis-services-2016-cpt-2-3.aspx) para saber mais sobre os xEvents para Analysis Services no SQL Server 2016.  
  
##  <a name="bkmk_top"></a> Neste tópico  
  
-   [Usar o Management Studio para configurar o Analysis Services](#bkmk_ssas_extended_events_ssms)  
  
-   [Script XMLA para iniciar Eventos Estendidos no Analysis Services](#bkmk_script_start)  
  
##  <a name="bkmk_ssas_extended_events_ssms"></a> Usar o Management Studio para configurar o Analysis Services  
 Para instâncias multidimensionais e de tabela, o Management Studio fornece uma nova pasta de gerenciamento que inclui sessões de xEvent iniciadas pelo usuário. Você pode executar várias sessões simultaneamente. No entanto, na implementação atual, a interface do usuário dos Eventos Estendidos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não têm suporte para a atualização ou substituição de uma sessão existente.  
  
 ![ssas_extended_events_ssms_start](../../analysis-services/instances/media/ssas-extended-events-ssms-start.png "ssas_extended_events_ssms_start")  
  
 **Escolher eventos**  
  
 Caso já saiba os eventos que pretende captar, pesquisá-los é a melhor maneira de adicioná-los para o rastreamento. Caso contrário, os eventos a seguir são usados normalmente para operações de monitoramento:  
  
-   **CommandBegin** e **CommandEnd**.  
  
-   **QueryBegin**, **QueryEnd**e **QuerySubcubeVerbose** (mostra toda a consulta MDX ou DAX enviada ao servidor), além de **ResourceUsage** para estatísticas sobre os recursos consumidos pela consulta e sobre a quantidade de linhas retornadas.  
  
-   **ProgressReportBegin** e **ProgressReportEnd** (para operações de processamento).  
  
-   **AuditLogin** e **AuditLogout** (capta a identidade do usuário sob a qual um aplicativo cliente se conecta ao Analysis Services).  
  
 **Escolher o armazenamento de dados**  
  
 A sessão pode ser transmitida dinamicamente em uma janela no Management Studio ou ser persistente em um arquivo para análise posterior usando Power Query ou o Excel.  
  
-   **event_file** armazena os dados da sessão em um arquivo .xel.  
  
-   **event_stream** habilita a opção **Observar dados dinâmicos** no Management Studio.  
  
-   **ring_buffer** armazena os dados da sessão na memória, desde que o servidor esteja em execução. Em uma reinicialização do servidor, os dados da sessão são descartados  
  
 **Adicionar Campos do Evento**  
  
 Não deixe de configurar a sessão para incluir os Campos do Evento de modo que você possa ver facilmente as informações de interesse.  
  
 **Configurar** é uma opção do lado mais distante da caixa de diálogo.  
  
 ![Configurar SSAS-xevents](../../analysis-services/instances/media/ssas-xevents-configure.PNG "ssas-xevents-configurar")  
  
 Na configuração, na guia Campos do Evento, escolha **TextData** para que esse campo seja exibido ao lado do evento, mostrando valores de retorno e incluindo consultas em execução no servidor.  
  
 Depois de configurar uma sessão para o armazenamento de dados e eventos desejados, você pode clicar no botão de script para enviar sua configuração para um dos destinos com suporte, incluindo um arquivo, uma nova consulta no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e a área de transferência.  
  
 **Atualizar sessões**  
  
 Quando criar a sessão, não deixe de atualizar a pasta Sessões no Management Studio para ver a sessão que acabou de criar. Caso configure um event_stream, você pode clicar com o botão direito do mouse no nome da sessão e escolher a opção **Observar dados dinâmicos** para monitorar as atividades do servidor em tempo real.  
  
##  <a name="bkmk_script_start"></a> Script XMLA para iniciar Eventos Estendidos no Analysis Services  
 O rastreamento de Eventos Estendidos é habilitado usando um comando de script de objeto de criação XMLA, conforme mostrado abaixo:  
  
```  
<Execute …>  
   <Command>  
      <Batch …>  
         <Create …>  
            <ObjectDefinition>  
               <Trace>  
                  <ID>trace_id</ID>  
                  <Name>trace_name</Name>  
                  <ddl300_300:XEvent>  
                     <event_session …>  
                        <event package="AS" name="AS_event">  
                           <action package="PACKAGE0" …/>  
                        </event>  
                        <target package="PACKAGE0" name="asynchronous_file_target">  
                           <parameter name="filename" value="data_filename.xel"/>  
                           <parameter name="metadatafile" value="metadata_filename.xem"/>  
                        </target>  
                     </event_session>  
                  </ddl300_300:XEvent>  
               </Trace>  
            </ObjectDefinition>  
         </Create>  
      </Batch>  
   </Command>  
   <Properties></Properties>  
</Execute>  
  
```  
  
 Onde os seguintes elementos serão definidos pelo usuário, dependendo das necessidades do rastreamento:  
  
 *trace_id*  
 Define o identificador exclusivo para este rastreamento.  
  
 *trace_name*  
 O nome especificado para este rastreamento; normalmente uma definição legível do rastreamento. O uso do valor *trace_id* como o nome é uma prática comum.  
  
 *AS_event*  
 O evento do Analysis Services a ser exposto. Consulte [Eventos de rastreamento do Analysis Services](../../analysis-services/trace-events/analysis-services-trace-events.md) para os nomes dos eventos.  
  
 *data_filename*  
 O nome do arquivo que contém dados dos eventos. Este nome terá um carimbo de data/hora como sufixo para evitar a substituição de dados se o rastreamento for enviado repetidas vezes.  
  
 *metadata_filename*  
 O nome do arquivo que contém metadados dos eventos. Este nome terá um carimbo de data/hora como sufixo para evitar a substituição de dados se o rastreamento for enviado repetidas vezes.  
  
||  
|-|  
|![Ícone de seta usado com de volta para o link superior](../../analysis-services/instances/media/uparrow16x16.gif "ícone de seta usado com de volta para o link superior") [neste tópico](#bkmk_top)|  
  
##  <a name="bkmk_script_stop"></a> Script XMLA para interromper Eventos Estendidos no Analysis Services  
 Para interromper o objeto de rastreamento de Eventos Estendidos, exclua esse objeto usando um comando de script de objeto de exclusão XMLA, conforme mostrado abaixo:  
  
```  
<Execute xmlns="urn:schemas-microsoft-com:xml-analysis">  
   <Command>  
      <Batch …>  
         <Delete …>  
            <Object>  
               <TraceID>trace_id</TraceID>  
            </Object>  
         </Delete>  
      </Batch>  
   </Command>  
   <Properties></Properties>  
</Execute>  
  
```  
  
 Onde os seguintes elementos serão definidos pelo usuário, dependendo das necessidades do rastreamento:  
  
 *trace_id*  
 Define o identificador exclusivo para o rastreamento a ser excluído.  
  
||  
|-|  
|![Ícone de seta usado com de volta para o link superior](../../analysis-services/instances/media/uparrow16x16.gif "ícone de seta usado com de volta para o link superior") [neste tópico](#bkmk_top)|  
  
## <a name="see-also"></a>Consulte também  
 [Eventos estendidos](../../relational-databases/extended-events/extended-events.md)  
  
  

