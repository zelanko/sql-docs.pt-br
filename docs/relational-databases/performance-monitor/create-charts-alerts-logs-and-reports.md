---
title: Criar gráficos, alertas, logs e relatórios | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- System Monitor [SQL Server], charts and reports
- charts [SQL Server]
- reports [SQL Server]
- reports [SQL Server], creating
- Windows System Monitor [SQL Server], charts and reports
- logs [SQL Server], System Monitor
- System Monitor [SQL Server], logs
- Windows System Monitor [SQL Server], logs
ms.assetid: c9162b37-e5dc-43d1-a3aa-1e9ebc69fecc
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 5e67b62ec00e2dd98ff4289c1f725892592340e0
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68024763"
---
# <a name="create-charts-alerts-logs-and-reports"></a>Criar gráficos, alertas, logs e relatórios
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O Monitor do Sistema permite criar gráficos, alertas, logs e relatórios para monitorar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="charts"></a>Gráficos  
 Os gráficos podem monitorar o desempenho atual de objetos e contadores selecionados; por exemplo, o uso da CPU ou E/S em disco. É possível adicionar diversas combinações de objetos e contadores a um gráfico do Monitor do Sistema. Também é possível adicionar objetos e contadores do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows a um gráfico.  
  
 Cada gráfico representa um subconjunto de informações a monitorar. Por exemplo, um gráfico pode rastrear estatísticas de uso de memória e um outro gráfico pode rastrear estatísticas de E/S em disco.  
  
 Usar um gráfico pode ser útil para as seguintes tarefas:  
  
-   Investigar por que um computador ou aplicativo está lento ou ineficiente.  
  
-   Monitorar continuamente os sistemas para localizar problemas de desempenho intermitentes.  
  
-   Descobrir por que a capacidade precisa ser aumentada.  
  
-   Exibir uma tendência na forma de um gráfico de linhas.  
  
-   Exibir uma comparação na forma de um gráfico de histograma.  
  
 Gráficos são úteis para o monitoramento de curto prazo em tempo real de um computador local ou remoto (por exemplo, quando se deseja monitorar um evento enquanto ele ocorre).  
  
## <a name="alerts"></a>Alertas  
 Usando alertas, o Monitor do Sistema rastreia eventos específicos e emite notificações a seu respeito conforme solicitado. Um log de alertas pode monitorar o desempenho atual de contadores e instâncias de objetos selecionados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Quando um contador excede um determinado valor, o log registra a data e a hora do evento. Um evento também pode gerar um alerta de rede. Você pode fazer com que um programa especificado seja executado na primeira vez ou em todas as vezes que o evento ocorrer. Por exemplo, um alerta pode enviar uma mensagem de rede a todos os administradores do sistema avisando que a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está ficando com pouco espaço em disco.  
  
## <a name="logs"></a>Logs  
 Os logs permitem registrar informações sobre a atividade atual de objetos e computadores selecionados para visualização e análise posteriores. É possível coletar dados de vários sistemas em um mesmo arquivo de log. Por exemplo, é possível criar logs diferentes que coletem informações sobre o desempenho de objetos selecionados em diversos computadores para análise futura. Você pode salvar essas seleções sob um nome de arquivo e reutilizá-las quando quiser criar um outro log de informações similares para comparação.  
  
 Arquivos de log fornecem informações preciosas para a solução de problemas ou planejamento. Enquanto que gráficos, alertas e relatórios sobre a atividade atual propiciam um feedback instantâneo, os arquivos de log permitem rastrear os contadores por um longo intervalo de tempo. Assim, você pode examinar as informações mais minuciosamente e documentar o desempenho do sistema.  
  
## <a name="reports"></a>Relatórios  
 Os relatórios permitem exibir valores de instâncias e contadores de objetos selecionados que mudam constantemente. Os valores aparecem em colunas para cada instância. É possível ajustar os intervalos do relatório, imprimir instantâneos e exportar dados. Use relatórios quando precisar exibir os números brutos.  
  
 Para obter mais informações sobre como criar gráficos, alertas, logs e relatórios ou sobre objetos e contadores do Windows, consulte a documentação do Windows.  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
