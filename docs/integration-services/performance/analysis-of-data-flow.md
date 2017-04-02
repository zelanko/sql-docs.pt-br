---
title: "An&#225;lise do Fluxo de Dados | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5654cb30-cad2-470c-97b3-59cb331033e5
caps.latest.revision: 11
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 11
---
# An&#225;lise do Fluxo de Dados
  Você pode usar a exibição [execution_data_statistics](../../integration-services/system-views/catalog-execution-data-statistics.md) do banco de dados **SSISDB** para analisar o fluxo de dados de pacotes. Esta exibição exibe uma linha a cada vez que um componente de fluxo de dados envia dados a um componente downstream. As informações podem ser usadas para obter um entendimento mais profundo das linhas que são enviadas para cada componente.  
  
> [!NOTE]  
>  O nível de log deve ser definido para **Detalhado** para capturar as informações com a exibição de catalog.execution_data_statistics.  
  
 O exemplo a seguir exibe o número de linhas enviadas entre componentes de um pacote.  
  
```  
use SSISDB  
select package_name, task_name, source_component_name, destination_component_name, rows_sent  
from catalog.execution_data_statistics  
where execution_id = 132  
order by source_component_name, destination_component_name  
  
```  
  
 O exemplo a seguir calcula o número de linhas por milissegundo enviadas por cada componente para uma execução específica. Os valores calculados são:  
  
-   **total_rows** – a soma de todas as linhas enviadas pelo componente  
  
-   **wall_clock_time_ms** – o tempo de execução decorrido total, em milissegundos, para cada componente  
  
-   **num_rows_per_millisecond** – o número de linhas por milissegundo enviadas por cada componente  
  
 A cláusula **HAVING** é usada para impedir um erro de divisão por zero nos cálculos.  
  
```  
use SSISDB  
select source_component_name, destination_component_name,  
    sum(rows_sent) as total_rows,  
    DATEDIFF(ms,min(created_time),max(created_time)) as wall_clock_time_ms,  
    ((0.0+sum(rows_sent)) / (datediff(ms,min(created_time),max(created_time)))) as [num_rows_per_millisecond]  
from [catalog].[execution_data_statistics]  
where execution_id = 132  
group by source_component_name, destination_component_name  
having (datediff(ms,min(created_time),max(created_time))) > 0  
order by source_component_name desc  
  
```  
  
## Tarefas relacionadas  
 [Depurando fluxo de dados](../../integration-services/troubleshooting/debugging-data-flow.md)  
  
 [Solucionando problemas de ferramentas para execução de pacotes](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)  
  
## Consulte também  
 [Dados em fluxos de dados](../../integration-services/data-flow/data-in-data-flows.md)  
  
  