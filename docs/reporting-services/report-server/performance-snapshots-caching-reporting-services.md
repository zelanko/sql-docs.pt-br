---
title: "Desempenho, instantâneos, cache (Reporting Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- performance [Reporting Services]
- Reporting Services, performance
ms.assetid: 85afd00f-e8d7-4ef7-9174-2ff84d82f960
caps.latest.revision: 20
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c752ea8a5f05a1dc861b0297b7a1c0eaca5cfc88
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="performance-snapshots-caching-reporting-services"></a>Desempenho, instantâneos, cache (Reporting Services)
  O desempenho do servidor de relatório é afetado por uma combinação de fatores que incluem o hardware, o número de usuários simultâneos que acessam relatórios, a quantidade de dados em um relatório e o formato de saída. Para entender os fatores de desempenho específicos de sua instalação e quais reparos produzirão os resultados desejados, será necessário obter dados de linha de base e executar testes. Para obter mais informações sobre ferramentas e diretrizes, consulte as seguintes publicações no MSDN: [Otimização de desempenho do Reporting Services](http://blogs.msdn.com/b/sqlcat/archive/2013/10/30/reporting-services-performance-and-optimization.aspx) e [Usando o Visual Studio 2005 para executar um teste de carregamento em um servidor de relatório do SQL Server 2005](http://go.microsoft.com/fwlink/?LinkID=77519).  
  
 Os princípios gerais a serem considerados incluem o seguinte:  
  
-   O processamento e a renderização de relatórios são operações que consomem muita memória. Quando possível, escolha um computador que tenha bastante memória.  
  
-   A hospedagem do servidor de relatório e do banco de dados do servidor de relatório em computadores separados tende a fornecer um melhor desempenho do hospedar ambos em um único computador avançado.  
  
-   Se o processamento de todos os relatórios estiver lento, avalie a possibilidade de uma implantação de expansão na qual várias instâncias do servidor de relatório oferecem suporte a um único banco de dados do servidor de relatório. Para obter os melhores resultados, use o software de balanceamento de carga para distribuir solicitações uniformemente pela implantação.  
  
-   Se um único relatório estiver sendo executado lentamente, ajuste as consultas ao conjunto de dados do relatório se o relatório tiver que ser executado sob demanda. Também é possível usar conjuntos de dados compartilhados que você pode armazenar em cache enquanto estiver armazenando em cache o relatório ou executando o relatório como um instantâneo.  
  
-   Se o processamento de todos os relatórios for lento em um formato específico (por exemplo, ao renderizar em PDF), tente realizar entrega de compartilhamento de arquivos, adicionar mais memória ou escolher um formato diferente.  
  
-   Para saber quanto demora o processamento de um relatório e obter outras métricas de uso, revise o log de execução do servidor de relatório. Para obter mais informações, veja [ExecutionLog do servidor de relatório e exibição do ExecutionLog3](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md).  
  
-   Para obter mais informações sobre como solucionar problemas de desempenho ajustando configurações de gerenciamento de memória, consulte [Configurar memória disponível para aplicativos do Servidor de Relatório](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Monitorando o desempenho do servidor de relatório](../../reporting-services/report-server/monitoring-report-server-performance.md)  
 Descreve os objetos de desempenho que podem ser usados para controlar a carga de processamento no servidor.  
  
 [Definir propriedades de processamento de relatórios](../../reporting-services/report-server/set-report-processing-properties.md)  
 Descreve maneiras de configurar um relatório para ser executado sob demanda, a partir do cache ou em uma agenda como um instantâneo de relatório.  
  
 [Configurar memória disponível para aplicativos do Servidor de Relatório](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md)  
 Descreve como você pode substituir o comportamento padrão de gerenciamento de memória.  
  
 [Armazenando relatórios em cache &#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md)  
 Descreve o comportamento do cache de relatório em um servidor de relatório.  
  
 [Conjuntos de dados compartilhados em cache &#40;SSRS&#41;](../../reporting-services/report-server/cache-shared-datasets-ssrs.md)  
 Descreve o comportamento do cache de conjunto de dados compartilhados em um servidor de relatório.  
  
 [Processar relatórios grandes](../../reporting-services/report-server/process-large-reports.md)  
 Fornece recomendações para configurar e distribuir um relatório grande.  
  
 [Definindo valores de tempo limite para processamento de relatórios e conjuntos de dados compartilhados &#40;SSRS&#41;](../../reporting-services/report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md)  
 Explica como definir tempos limite no processamento de consultas e relatórios.  
  
## <a name="see-also"></a>Consulte também  
 [Manage a Running Process](../../reporting-services/subscriptions/manage-a-running-process.md)   
 [Verificar a execução de um relatório](../../reporting-services/report-server/verifying-a-report-run.md)  
  
  
