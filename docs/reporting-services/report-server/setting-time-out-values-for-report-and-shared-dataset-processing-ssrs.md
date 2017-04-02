---
title: "Definindo valores de tempo limite para processamento de relat&#243;rio e conjuntos de dados compartilhados (SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "tempos limite [Reporting Services]"
  - "tempos limite de consultas [Reporting Services]"
  - "processamento de relatório [Reporting Services], tempos limite"
  - "tempos limite de execução de relatório [Reporting Services]"
ms.assetid: 0f9dc61d-d03c-4bbf-8090-7a53844350f8
caps.latest.revision: 39
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 39
---
# Definindo valores de tempo limite para processamento de relat&#243;rio e conjuntos de dados compartilhados (SSRS)
  Você pode [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] especificar valores de tempo limite para definir limites para o uso dos recursos do sistema. O servidor de relatório dá suporte a dois valores de tempo limite:  
  
-   Um valor de tempo limite de consulta de conjunto de dados inserido é o número de segundos durante os quais o servidor de relatório aguarda uma resposta do banco de dados. Esse valor é definido em um relatório.  
  
-   Um valor de tempo limite de consulta de conjunto de dados compartilhado é o número de segundos durante os quais o servidor de relatório aguarda uma resposta do banco de dados. Esse valor faz parte da definição do conjunto de dados compartilhado e pode ser alterado quando você gerencia o conjunto de dados compartilhado no servidor de relatório.  
  
-   Um valor de tempo limite de execução de relatório é o número máximo de segundos durante os quais o processamento de um relatório pode prosseguir até sua interrupção. Esse valor é definido no nível de sistema. Você pode variar essa configuração para relatórios individuais.  
  
 A maior parte dos erros de tempo limite ocorre durante o processamento de consultas. Caso você esteja encontrando erros de tempo limite, experimente aumentar o valor de tempo limite de consulta. Não deixe de ajustar o valor de tempo limite de execução de relatório de modo que ele seja superior ao tempo limite de consulta. O período deve ser suficiente para a conclusão do processamento da consulta e do relatório.  
  
## Definindo um tempo limite de consulta para um conjunto de dados inserido em um relatório  
 Os valores de tempo limite de consulta são especificados durante a criação do relatório quando você define um conjunto de dados inserido. O valor de tempo limite é armazenado com o relatório, no elemento **Timeout** da definição do relatório. Por padrão, este valor é definido como 30 segundos. Para obter mais informações, consulte [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
  
 Os usuários com permissão para modificar as propriedades de um relatório publicado podem redefinir esse valor, editando o arquivo de definição do relatório.  
  
 Você também pode especificar um valor de tempo limite de consulta para assinaturas controladas por dados. O valor de tempo limite de consulta é especificado nas páginas de Assinatura Controlada por Dados. O valor especificado determina quanto tempo o servidor de relatório aguarda pela conclusão do processamento da consulta ao recuperar dados da fonte de dados do assinante.  
  
## Definindo um tempo limite de consulta para um conjunto de dados compartilhado  
 Os valores de tempo limite de consulta são especificados em segundos no servidor de relatório quando você cria ou gerencia um conjunto de dados compartilhado. Por padrão, esse valor é definido como 0 segundo, que é o equivalente ao valor de nenhum tempo limite. Para obter mais informações, consulte [Gerenciar conjuntos de dados compartilhados](../../reporting-services/report-data/manage-shared-datasets.md).  
  
## Definindo um tempo limite de execução de relatórios  
 Você pode definir o valor do tempo limite de execução de relatórios para limitar a quantidade de tempo que um servidor de relatório usa para processar um relatório. Os valores de tempo limite de execução de relatório podem ser especificados no Gerenciador de Relatórios. Você pode definir um valor padrão para todos os relatórios na página Configurações de Site e anular esse valor na página de propriedades de Execução para um relatório específico. Por padrão, o valor é definido como 1.800 segundos. Para obter mais informações, consulte [Definir as propriedades do processamento de relatórios](../../reporting-services/report-server/set-report-processing-properties.md).  
  
## Como são avaliados os valores de tempo limite de execução de relatório  
 O servidor de relatório avalia os trabalhos em execução em intervalos de 60 segundos. A cada intervalo de 60 segundos, o servidor de relatório compara o tempo de processamento atual com o valor de tempo limite de execução do relatório. Se o tempo de processamento para um relatório exceder o valor de tempo limite de execução de relatório, o processamento do relatório será interrompido.  
  
 Observe que se você especificar um valor de tempo limite inferior a 60 segundos, o relatório poderá ser executado totalmente se o processamento for iniciado e concluído durante a parte silenciosa do ciclo quando o servidor de relatório não estiver avaliando os trabalhos em execução. Por exemplo, se você definir um valor de tempo limite de 10 segundos para um relatório que leva 20 segundos para ser executado, ele será processado totalmente se a execução do relatório for iniciada antecipadamente no ciclo de 60 segundos.  
  
> [!NOTE]  
>  Você pode definira configuração **RunningRequestsDbCycle** no arquivo RSReportServer.config para alterar a frequência de avaliação dos trabalhos em execução.  
  
## Consulte também  
 [Definir opções de processamento &#40;Reporting Services no modo integrado do SharePoint&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)   
 [Servidor de relatório do Reporting Services &#40;Modo Nativo&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [Manage a Running Process](../../reporting-services/subscriptions/manage-a-running-process.md)   
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../Topic/Report%20Manager%20%20\(SSRS%20Native%20Mode\).md)  
  
  