---
title: "Identificar afunilamentos | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "afunilamentos de recursos [SQL Server]"
  - "monitoramento de banco de dados [SQL Server], afunilamentos"
  - "desempenho [SQL Server], afunilamentos"
  - "ajustando bancos de dados [SQL Server], afunilamentos"
  - "monitorando o desempenho do servidor [SQL Server], afunilamentos"
  - "monitorando o desempenho [SQL Server], afunilamentos"
  - "desempenho do banco de dados [SQL Server], afunilamentos"
  - "desempenho do servidor [SQL Server], afunilamentos"
  - "afunilamentos [SQL Server]"
  - "identificando afunilamentos [SQL Server]"
ms.assetid: db079e65-ee80-4105-aec9-f8230d0d6635
caps.latest.revision: 18
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 18
---
# Identificar afunilamentos
  O acesso simultâneo a recursos compartilhados provoca afunilamentos. Em geral, os afunilamentos estão presentes em todo sistema de software e são inevitáveis. Porém, demandas excessivas em recursos compartilhados causam um tempo de resposta ruim e devem ser identificadas e ajustadas.  
  
 São causas de afunilamentos:  
  
-   Recursos insuficientes, exigindo componentes adicionais ou atualizados.  
  
-   Recursos de mesmo tipo entre os quais as cargas de trabalho não são distribuídas de maneira uniforme; por exemplo, um disco sendo monopolizado.  
  
-   Mau funcionamento de recursos.  
  
-   Recursos incorretamente configurados.  
  
## Analisando afunilamentos  
 Durações excessivas de diversos eventos são indicadores de afunilamentos que podem ser ajustados.  
  
 Por exemplo:  
  
-   Algum outro componente pode impedir a carga de alcançar esse componente e aumentar, assim, o tempo para a conclusão da carga.  
  
-   Solicitações de clientes podem levar mais tempo devido a congestionamento da rede.  
  
 A seguir, encontram-se cinco grandes áreas a monitorar, ao rastrear o desempenho do servidor, para identificar afunilamentos.  
  
|Possível área de afunilamento|Efeitos no servidor|  
|------------------------------|---------------------------|  
|Uso de memória|Memória insuficiente alocado ou disponível para o Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] degrada o desempenho. Os dados têm que ser lidos do disco, em vez de diretamente do cache de dados. Sistemas operacionais Microsoft Windows executam paginação excessiva, permutando dados de e para o disco, segundo a necessidade de páginas.|  
|Utilização de CPU|Uma taxa de utilização de CPU cronicamente alta pode indicar que as consultas do [!INCLUDE[tsql](../../includes/tsql-md.md)] precisam ser ajustadas ou que é necessário atualizar a CPU.|  
|Entrada/saída (E/S) de disco|[!INCLUDE[tsql](../../includes/tsql-md.md)] consultas podem ser ajustadas de modo a reduzir E/S desnecessária; por exemplo, empregando índices.|  
|Conexões de usuário|Muitos usuários podem estar acessando o servidor simultaneamente, provocando degradação do desempenho.|  
|Bloqueios|Aplicativos incorretamente projetados podem causar bloqueios e obstruir a simultaneidade, causando tempos de resposta mais longos e taxas de transferência de transações mais baixas.|  
  
## Consulte também  
 [Monitorar o uso da CPU](../../relational-databases/performance-monitor/monitor-cpu-usage.md)   
 [Monitorar o uso do disco](../../relational-databases/performance-monitor/monitor-disk-usage.md)   
 [Monitorar o uso da memória](../../relational-databases/performance-monitor/monitor-memory-usage.md)   
 [SQL Server, objeto General Statistics](../../relational-databases/performance-monitor/sql-server-general-statistics-object.md)   
 [SQL Server, objeto Locks](../../relational-databases/performance-monitor/sql-server-locks-object.md)  
  
  