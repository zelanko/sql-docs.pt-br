---
title: "Monitorar o uso de recursos (Monitor do Sistema) | Microsoft Docs"
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
  - "monitorando o desempenho [SQL Server], uso do recurso"
  - "Monitor do Sistema [SQL Server], sobre o Monitor do Sistema do Windows"
  - "monitoramento de uso de recursos [SQL Server]"
  - "Monitor do Sistema [SQL Server]"
  - "contadores [SQL Server], questões de uso de recursos"
  - "contadores de desempenho [SQL Server], questões de uso de recursos"
  - "Monitor do Sistema do Windows [SQL Server], sobre o Monitor do Sistema do Windows"
  - "monitorando [SQL Server], uso de recursos do servidor"
  - "monitorando o uso de recursos [SQL Server]"
  - "Monitor do Sistema do Windows [SQL Server]"
  - "monitoramento de banco de dados [SQL Server], uso de recursos"
  - "desempenho de banco de dados [SQL Server], uso de recursos"
  - "ajustando bancos de dados [SQL Server], uso de recursos"
  - "desempenho do servidor [SQL Server], uso de recursos"
ms.assetid: f2993a28-0b81-46f2-aec0-6877fe990387
caps.latest.revision: 29
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 29
---
# Monitorar o uso de recursos (Monitor do Sistema)
  Se estiver executando o sistema operacional Microsoft Windows Server, use a ferramenta gráfica Monitor do Sistema para avaliar o desempenho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. É possível visualizar objetos, contadores de desempenho e o comportamento de outros objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como processadores, memória, cache, threads e processos. Cada um desses objetos possui um conjunto de contadores associado para medir o uso de dispositivos, o comprimento de filas, demoras e outros indicadores da taxa de transferência e do congestionamento interno.  
  
> [!NOTE]  
>  O Monitor do Sistema substituiu o Monitor de Desempenho a partir do Windows NT 4.0.  
  
## Benefícios do Monitor do Sistema  
 O Monitor do Sistema pode ser útil monitorar o sistema operacional Windows e os contadores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao mesmo tempo para determinar a correlação entre o desempenho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o Windows. Por exemplo, monitorar os contadores de entrada/saída (E/S) em disco do Windows e os contadores do Gerenciador de Buffer do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao mesmo tempo pode revelar o comportamento do sistema inteiro.  
  
 O Monitor do Sistema permite obter estatísticas sobre a atividade e o desempenho atuais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Usando o Monitor do Sistema, você pode:  
  
-   Exibir dados simultaneamente de qualquer quantidade de computadores.  
  
-   Visualizar e alterar gráficos, de modo a refletir a atividade atual, e exibir valores de contadores que são atualizados a uma frequência definida pelo usuário.   
  
-   Exportar dados de gráficos, logs, logs de alertas e relatórios para aplicativos de planilha ou de banco de dados, para manipulação adicional e impressão.  
  
-   Adicionar alertas do sistema que listam um evento no log de alertas e que podem notificá-lo, emitindo um alerta de rede.  
  
-   Executar um aplicativo predefinido na primeira vez ou toda vez que um valor de contador estiver acima ou abaixo de um valor definido pelo usuário.  
  
-   Criar arquivos de log contendo dados sobre diversos objetos de computadores diferentes.  
  
-   Adicionar a um arquivo seções selecionadas de outros arquivos de log existentes, para formar um arquivo morto de longo prazo.  
  
-   Exibir relatórios sobre a atividade atual ou criar relatórios a partir de arquivos de log existentes.  
  
-   Salvar gráficos, alertas, logs ou configurações de relatórios individuais ou toda a configuração do espaço de trabalho, para reutilização.  
  
    > [!NOTE]  
    >  O Monitor do Sistema substituiu o Monitor de Desempenho a partir do Windows NT 4.0. Você pode usar o Monitor do Sistema ou o Monitor de Desempenho para essas tarefas.  
  
## Desempenho do Monitor do Sistema  
 Ao monitorar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o sistema operacional Microsoft Windows para investigar questões relacionadas ao desempenho, concentre seus esforços iniciais em três áreas principais:  
  
-   Atividade de disco  
  
-   Utilização de processador  
  
-   Uso de memória  
  
 Monitorar um computador em que o Monitor do Sistema é executado pode influir ligeiramente em seu desempenho. Portanto, registre os dados do Monitor do Sistema em outro disco (ou computador), de modo a reduzir o efeito no computador que está sendo monitorado, ou execute o Monitor do Sistema a partir de um computador remoto. Monitore apenas os contadores que lhe interessam. Se você monitorar contadores demais, haverá sobrecarga de uso de recursos no processo de monitoramento, o que afetará o desempenho do computador que está sendo monitorado.  
  
## Tarefas do Monitor do Sistema  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Descreve quando usar o Monitor do Sistema e discute a sobrecarga de desempenho quando você usa o Monitor do Sistema.|[Executar o Monitor do Sistema](../../relational-databases/performance-monitor/run-system-monitor.md)|  
|Descreve como monitorar contadores de disco para determinar a atividade de disco e a quantidade de E/S gerada pelos componentes do SQL Server.|[Monitorar o uso do disco](../../relational-databases/performance-monitor/monitor-disk-usage.md)|  
|Descreve como monitorar uma instância do Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para determinar se as taxas de uso de CPU estão dentro dos intervalos normais.|[Monitorar o uso da CPU](../../relational-databases/performance-monitor/monitor-cpu-usage.md)|  
|Descreve como monitorar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para confirmar que o uso de memória está dentro de intervalos normais.|[Monitorar o uso da memória](../../relational-databases/performance-monitor/monitor-memory-usage.md)|  
|Descreve como criar um alerta a ser emitido quando um valor limite de um contador do Monitor do Sistema for atingido.|[Criar um alerta de banco de dados do SQL Server](../../relational-databases/performance-monitor/create-a-sql-server-database-alert.md)|  
|Descreve como criar gráficos, alertas, logs e relatórios para monitorar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|[Criar gráficos, alertas, logs e relatórios](../../relational-databases/performance-monitor/create-charts-alerts-logs-and-reports.md)|  
|Lista os objetos e contadores que o Monitor do Sistema usa para monitorar a atividade em computadores que executem uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|[Usar objetos do SQL Server](../../relational-databases/performance-monitor/use-sql-server-objects.md)|  
|Lista os objetos e contadores que o Monitor do Sistema usa para monitorar a atividade de OLTP na memória.|[Contadores de desempenho XTP &#40;OLTP in-memory&#41; do SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)|  
  
  