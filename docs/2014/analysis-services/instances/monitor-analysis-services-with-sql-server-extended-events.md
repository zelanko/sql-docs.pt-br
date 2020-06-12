---
title: Usar SQL Server XEvents (eventos estendidos) para monitorar Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b57cc2fe-52dc-4fa9-8554-5a866e25c6d7
author: minewiskan
ms.author: owend
ms.openlocfilehash: 60f1811d1bf4714284e9676623422870345c8261
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84543798"
---
# <a name="use-sql-server-extended-events-xevents-to-monitor-analysis-services"></a>Usar eventos estendidos do SQL Server (XEvents) para monitorar o Analysis Services
  Analysis Services fornece recursos de rastreamento por meio do uso de [eventos estendidos](../../relational-databases/extended-events/extended-events.md).  
  
 Eventos Estendidos são uma infraestrutura de evento que é altamente escalonável e configurável para sistemas de servidor. Eventos Estendidos são um sistema de monitoramento de desempenho de peso leve que usa poucos recursos de desempenho.  
  
 Todos os eventos de Analysis Services podem ser capturados e direcionados para consumidores específicos, conforme definido em [eventos estendidos](../../relational-databases/extended-events/extended-events.md), por meio de XEvents.  
  
## <a name="initiating-extended-events-in-analysis-services"></a>Iniciando Eventos Estendidos no Analysis Services  
 O rastreamento de Eventos Estendidos é habilitado usando um comando de script de objeto de criação XMLA, conforme mostrado abaixo:  
  
```  
<Execute ...>  
   <Command>  
      <Batch ...>  
         <Create ...>  
            <ObjectDefinition>  
               <Trace>  
                  <ID>trace_id</ID>  
                  <Name>trace_name</Name>  
                  <ddl300_300:XEvent>  
                     <event_session ...>  
                        <event package="AS" name="AS_event">  
                           <action package="PACKAGE0" .../>  
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
 O evento do Analysis Services a ser exposto. Consulte [Eventos de rastreamento do Analysis Services](https://docs.microsoft.com/bi-reference/trace-events/analysis-services-trace-events) para os nomes dos eventos.  
  
 *data_filename*  
 O nome do arquivo que contém dados dos eventos. Este nome terá um carimbo de data/hora como sufixo para evitar a substituição de dados se o rastreamento for enviado repetidas vezes.  
  
 *metadata_filename*  
 O nome do arquivo que contém metadados dos eventos. Este nome terá um carimbo de data/hora como sufixo para evitar a substituição de dados se o rastreamento for enviado repetidas vezes.  
  
## <a name="stopping-extended-events-in-analysis-services"></a>Interrompendo eventos estendidos no Analysis Services  
 Para interromper o objeto de rastreamento de Eventos Estendidos, exclua esse objeto usando um comando de script de objeto de exclusão XMLA, conforme mostrado abaixo:  
  
```  
<Execute xmlns="urn:schemas-microsoft-com:xml-analysis">  
   <Command>  
      <Batch ...>  
         <Delete ...>  
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
  
## <a name="see-also"></a>Consulte Também  
 [Eventos estendidos](../../relational-databases/extended-events/extended-events.md)  
  
  
