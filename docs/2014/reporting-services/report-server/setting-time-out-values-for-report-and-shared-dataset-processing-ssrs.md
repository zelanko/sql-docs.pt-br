---
title: Definindo valores de tempo limite para processamento de relatório e conjuntos de dados compartilhados (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- time-outs [Reporting Services]
- query time-outs [Reporting Services]
- report processing [Reporting Services], time-outs
- report execution time-outs [Reporting Services]
ms.assetid: 0f9dc61d-d03c-4bbf-8090-7a53844350f8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fdbca5818e3430c0445444f3fb98b426e5f8a79c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66103207"
---
# <a name="setting-time-out-values-for-report-and-shared-dataset-processing-ssrs"></a>Definindo valores de tempo limite para processamento de relatório e conjuntos de dados compartilhados (SSRS)
  Você pode especificar valores de tempo limite para definir limites para o uso dos recursos do sistema. O servidor de relatório dá suporte a dois valores de tempo limite:  
  
-   Um valor de tempo limite de consulta de conjunto de dados inserido é o número de segundos durante os quais o servidor de relatório aguarda uma resposta do banco de dados. Esse valor é definido em um relatório.  
  
-   Um valor de tempo limite de consulta de conjunto de dados compartilhado é o número de segundos durante os quais o servidor de relatório aguarda uma resposta do banco de dados. Esse valor faz parte da definição do conjunto de dados compartilhado e pode ser alterado quando você gerencia o conjunto de dados compartilhado no servidor de relatório.  
  
-   Um valor de tempo limite de execução de relatório é o número máximo de segundos durante os quais o processamento de um relatório pode prosseguir até sua interrupção. Esse valor é definido no nível de sistema. Você pode variar essa configuração para relatórios individuais.  
  
 A maior parte dos erros de tempo limite ocorre durante o processamento de consultas. Caso você esteja encontrando erros de tempo limite, experimente aumentar o valor de tempo limite de consulta. Não deixe de ajustar o valor de tempo limite de execução de relatório de modo que ele seja superior ao tempo limite de consulta. O período deve ser suficiente para a conclusão do processamento da consulta e do relatório.  
  
## <a name="setting-a-query-time-out-for-an-embedded-dataset-in-a-report"></a>Definindo um tempo limite de consulta para um conjunto de dados inserido em um relatório  
 Os valores de tempo limite de consulta são especificados durante a criação do relatório quando você define um conjunto de dados inserido. O valor de tempo limite é armazenado com o relatório, no elemento `Timeout` da definição do relatório. Por padrão, este valor é definido como 30 segundos. Para obter mais informações, consulte [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](../report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
  
 Os usuários com permissão para modificar as propriedades de um relatório publicado podem redefinir esse valor, editando o arquivo de definição do relatório.  
  
 Você também pode especificar um valor de tempo limite de consulta para assinaturas controladas por dados. O valor de tempo limite de consulta é especificado nas páginas de Assinatura Controlada por Dados. O valor especificado determina quanto tempo o servidor de relatório aguarda pela conclusão do processamento da consulta ao recuperar dados da fonte de dados do assinante.  
  
## <a name="setting-a-query-time-out-for-a-shared-dataset"></a>Definindo um tempo limite de consulta para um conjunto de dados compartilhado  
 Os valores de tempo limite de consulta são especificados em segundos no servidor de relatório quando você cria ou gerencia um conjunto de dados compartilhado. Por padrão, esse valor é definido como 0 segundo, que é o equivalente ao valor de nenhum tempo limite. Para obter mais informações, consulte [Gerenciar conjuntos de dados compartilhados](../report-data/manage-shared-datasets.md).  
  
## <a name="setting-a-report-execution-time-out"></a>Definindo um tempo limite de execução de relatórios  
 Você pode definir o valor do tempo limite de execução de relatórios para limitar a quantidade de tempo que um servidor de relatório usa para processar um relatório. Os valores de tempo limite de execução de relatório podem ser especificados no Gerenciador de Relatórios. Você pode definir um valor padrão para todos os relatórios na página Configurações de Site e anular esse valor na página de propriedades de Execução para um relatório específico. Por padrão, o valor é definido como 1.800 segundos. Para obter mais informações, consulte [Definir as propriedades do processamento de relatórios](set-report-processing-properties.md).  
  
## <a name="how-report-execution-time-out-values-are-evaluated"></a>Como são avaliados os valores de tempo limite de execução de relatório  
 O servidor de relatório avalia os trabalhos em execução em intervalos de 60 segundos. A cada intervalo de 60 segundos, o servidor de relatório compara o tempo de processamento atual com o valor de tempo limite de execução do relatório. Se o tempo de processamento para um relatório exceder o valor de tempo limite de execução de relatório, o processamento do relatório será interrompido.  
  
 Observe que se você especificar um valor de tempo limite inferior a 60 segundos, o relatório poderá ser executado totalmente se o processamento for iniciado e concluído durante a parte silenciosa do ciclo quando o servidor de relatório não estiver avaliando os trabalhos em execução. Por exemplo, se você definir um valor de tempo limite de 10 segundos para um relatório que leva 20 segundos para ser executado, ele será processado totalmente se a execução do relatório for iniciada antecipadamente no ciclo de 60 segundos.  
  
> [!NOTE]  
>  Você pode definir `RunningRequestsDbCycle` no arquivo RSReportServer.config para alterar a frequência de avaliação dos trabalhos em execução.  
  
## <a name="see-also"></a>Consulte também  
 [Definir opções de processamento &#40;Reporting Services no modo integrado do SharePoint&#41;](../set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)   
 [Servidor de relatório do Reporting Services &#40;Modo Nativo&#41;](reporting-services-report-server-native-mode.md)   
 [Manage a Running Process](../subscriptions/manage-a-running-process.md)   
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../report-manager-ssrs-native-mode.md)  
  
  
