---
title: Desempenho, instantâneos, cache (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- performance [Reporting Services]
- Reporting Services, performance
ms.assetid: 85afd00f-e8d7-4ef7-9174-2ff84d82f960
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0b1faef483d62d1e7853e30279d9c789ebb05372
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63190965"
---
# <a name="performance-snapshots-caching-reporting-services"></a>Desempenho, instantâneos, cache (Reporting Services)
  O desempenho do servidor de relatório é afetado por uma combinação de fatores que incluem o hardware, o número de usuários simultâneos que acessam relatórios, a quantidade de dados em um relatório e o formato de saída. Para entender os fatores de desempenho específicos de sua instalação e quais reparos produzirão os resultados desejados, será necessário obter dados de linha de base e executar testes. Para obter mais informações sobre ferramentas e diretrizes, consulte as seguintes publicações no MSDN: [Reporting Services a otimização de desempenho](https://blogs.msdn.com/b/sqlcat/archive/2013/10/30/reporting-services-performance-and-optimization.aspx) e [usando o Visual Studio 2005 para realizar testes de carga em um SQL Server 2005 Reporting Services Report Server](https://go.microsoft.com/fwlink/?LinkID=77519).  
  
 Os princípios gerais a serem considerados incluem o seguinte:  
  
-   O processamento e a renderização de relatórios são operações que consomem muita memória. Quando possível, escolha um computador que tenha bastante memória.  
  
-   A hospedagem do servidor de relatório e do banco de dados do servidor de relatório em computadores separados tende a fornecer um melhor desempenho do hospedar ambos em um único computador avançado.  
  
-   Se o processamento de todos os relatórios estiver lento, avalie a possibilidade de uma implantação de expansão na qual várias instâncias do servidor de relatório oferecem suporte a um único banco de dados do servidor de relatório. Para obter os melhores resultados, use o software de balanceamento de carga para distribuir solicitações uniformemente pela implantação.  
  
-   Se um único relatório estiver sendo executado lentamente, ajuste as consultas ao conjunto de dados do relatório se o relatório tiver que ser executado sob demanda. Também é possível usar conjuntos de dados compartilhados que você pode armazenar em cache enquanto estiver armazenando em cache o relatório ou executando o relatório como um instantâneo.  
  
-   Se o processamento de todos os relatórios for lento em um formato específico (por exemplo, ao renderizar em PDF), tente realizar entrega de compartilhamento de arquivos, adicionar mais memória ou escolher um formato diferente.  
  
-   Para saber quanto demora o processamento de um relatório e obter outras métricas de uso, revise o log de execução do servidor de relatório. Para obter mais informações, consulte [Log de execução do servidor de relatório e exibição do ExecutionLog3](report-server-executionlog-and-the-executionlog3-view.md).  
  
-   Para obter mais informações sobre como solucionar problemas de desempenho ajustando configurações de gerenciamento de memória, consulte [Configurar memória disponível para aplicativos do Servidor de Relatório](../report-server/configure-available-memory-for-report-server-applications.md).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Monitorando o desempenho do servidor de relatório](monitoring-report-server-performance.md)  
 Descreve os objetos de desempenho que podem ser usados para controlar a carga de processamento no servidor.  
  
 [Definir propriedades de processamento de relatórios](set-report-processing-properties.md)  
 Descreve maneiras de configurar um relatório para ser executado sob demanda, a partir do cache ou em uma agenda como um instantâneo de relatório.  
  
 [Configurar memória disponível para aplicativos do Servidor de Relatório](../report-server/configure-available-memory-for-report-server-applications.md)  
 Descreve como você pode substituir o comportamento padrão de gerenciamento de memória.  
  
 [Armazenando relatórios em cache &#40;SSRS&#41;](caching-reports-ssrs.md)  
 Descreve o comportamento do cache de relatório em um servidor de relatório.  
  
 [Conjuntos de dados compartilhados em cache &#40;SSRS&#41;](cache-shared-datasets-ssrs.md)  
 Descreve o comportamento do cache de conjunto de dados compartilhados em um servidor de relatório.  
  
 [Processar relatórios grandes](process-large-reports.md)  
 Fornece recomendações para configurar e distribuir um relatório grande.  
  
 [Definindo valores de tempo limite para processamento de relatórios e conjuntos de dados compartilhados &#40;SSRS&#41;](setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md)  
 Explica como definir tempos limite no processamento de consultas e relatórios.  
  
## <a name="see-also"></a>Consulte também  
 [Manage a Running Process](../subscriptions/manage-a-running-process.md)   
 [Verificando uma execução de relatório](verifying-a-report-run.md)  
  
  
