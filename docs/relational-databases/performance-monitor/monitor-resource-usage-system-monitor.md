---
title: Monitorar o uso de recursos (Monitor do Sistema) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server], resource usage
- System Monitor [SQL Server], about Windows System Monitor
- resource usage monitoring [SQL Server]
- System Monitor [SQL Server]
- counters [SQL Server], resource usage subjects
- performance counters [SQL Server], resource usage subjects
- Windows System Monitor [SQL Server], about Windows System Monitor
- monitoring [SQL Server], server resource usage
- monitoring resource usage [SQL Server]
- Windows System Monitor [SQL Server]
- database monitoring [SQL Server], resource usage
- database performance [SQL Server], resource usage
- tuning databases [SQL Server], resource usage
- server performance [SQL Server], resource usage
ms.assetid: f2993a28-0b81-46f2-aec0-6877fe990387
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: 8de6f5ade289780d5f0929af2f5a62e7facfe39b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62649552"
---
# <a name="monitor-resource-usage-system-monitor"></a>Monitorar o uso de recursos (Monitor do Sistema)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Se estiver executando o sistema operacional Microsoft Windows Server, use a ferramenta gráfica Monitor do Sistema para avaliar o desempenho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. É possível visualizar objetos, contadores de desempenho e o comportamento de outros objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , como processadores, memória, cache, threads e processos. Cada um desses objetos possui um conjunto de contadores associado para medir o uso de dispositivos, o comprimento de filas, demoras e outros indicadores da taxa de transferência e do congestionamento interno.  
  
> [!NOTE]  
>  O Monitor do Sistema substituiu o Monitor de Desempenho a partir do Windows NT 4.0.  
  
## <a name="benefits-of-system-monitor"></a>Benefícios do Monitor do Sistema  
 O Monitor do Sistema pode ser útil monitorar o sistema operacional Windows e os contadores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao mesmo tempo para determinar a correlação entre o desempenho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o Windows. Por exemplo, monitorar os contadores de entrada/saída (E/S) em disco do Windows e os contadores do Gerenciador de Buffer do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao mesmo tempo pode revelar o comportamento do sistema inteiro.  
  
 O Monitor do Sistema permite obter estatísticas sobre a atividade e o desempenho atuais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Usando o Monitor do Sistema, você pode:  
  
-   Exibir dados simultaneamente de qualquer quantidade de computadores.  
  
-   Visualizar e alterar gráficos, de modo a refletir a atividade atual, e exibir valores de contadores que são atualizados a uma frequência definida pelo usuário.  
  
-   Exportar dados de gráficos, logs, logs de alertas e relatórios para aplicativos de planilha ou de banco de dados, para manipulação adicional e impressão.  
  
-   Adicionar alertas do sistema que listam um evento no log de alertas e que podem notificá-lo, emitindo um alerta de rede.  
  
-   Executar um aplicativo predefinido na primeira vez ou toda vez que um valor de contador estiver acima ou abaixo de um valor definido pelo usuário.  
  
-   Criar arquivos de log contendo dados sobre diversos objetos de computadores diferentes.  
  
-   Adicionar a um arquivo seções selecionadas de outros arquivos de log existentes, para formar um arquivo morto de longo prazo.  
  
-   Exibir relatórios sobre a atividade atual ou criar relatórios a partir de arquivos de log existentes.  
  
-   Salvar gráficos, alertas, logs ou configurações de relatórios individuais ou toda a configuração do workspace, para reutilização.  
  
    > [!NOTE]  
    >  O Monitor do Sistema substituiu o Monitor de Desempenho a partir do Windows NT 4.0. Você pode usar o Monitor do Sistema ou o Monitor de Desempenho para essas tarefas.  
  
## <a name="system-monitor-performance"></a>Desempenho do Monitor do Sistema  
 Ao monitorar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o sistema operacional Microsoft Windows para investigar questões relacionadas ao desempenho, concentre seus esforços iniciais em três áreas principais:  
  
-   Atividade de disco  
  
-   Utilização de processador  
  
-   Uso de memória  
  
 Monitorar um computador em que o Monitor do Sistema é executado pode influir ligeiramente em seu desempenho. Portanto, registre os dados do Monitor do Sistema em outro disco (ou computador), de modo a reduzir o efeito no computador que está sendo monitorado, ou execute o Monitor do Sistema a partir de um computador remoto. Monitore apenas os contadores que lhe interessam. Se você monitorar contadores demais, haverá sobrecarga de uso de recursos no processo de monitoramento, o que afetará o desempenho do computador que está sendo monitorado.  
  
## <a name="system-monitor-tasks"></a>Tarefas do Monitor do Sistema  
  
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
  
  
