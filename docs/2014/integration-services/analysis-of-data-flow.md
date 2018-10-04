---
title: Análise de fluxo de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 5654cb30-cad2-470c-97b3-59cb331033e5
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e612fefcebd0537d13a4377484bbaddc04d086a0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48064516"
---
# <a name="analysis-of-data-flow"></a>Análise do Fluxo de Dados
  Você pode usar o [execution_data_statistics](../relational-databases/statistics/statistics.md) `SSISDB` para analisar o fluxo de dados de pacotes do banco de dados. Esta exibição exibe uma linha a cada vez que um componente de fluxo de dados envia dados a um componente downstream. As informações podem ser usadas para obter um entendimento mais profundo das linhas que são enviadas para cada componente.  
  
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
  
 O `HAVING` cláusula é usada para impedir um erro de divisão por zero nos cálculos.  
  
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
  
## <a name="related-tasks"></a>Related Tasks  
 [Depurar o fluxo de dados](troubleshooting/debugging-data-flow.md)  
  
 [Ferramentas de solução de problemas de execução de pacote](troubleshooting/troubleshooting-tools-for-package-execution.md)  
  
## <a name="see-also"></a>Consulte também  
 [Dados em fluxos de dados](data-flow/data-in-data-flows.md)  
  
  
