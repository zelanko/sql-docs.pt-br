---
title: Relatórios de solução de problemas para execução de pacotes | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 8fc476ac-bd69-434e-9636-70776e0b3b6c
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a52a29196fb0578482ebfff068adff736c954efa
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47818944"
---
# <a name="troubleshooting-reports-for-package-execution"></a>Solucionando problemas de relatórios para execução de pacotes
  Na versão atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], os relatórios padrão estão disponíveis no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para ajudar você a monitorar e solucionar problemas de pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , que foram implantados no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Dois desses relatórios de pacotes em especial ajudam você a exibir o status de execução do pacote e a identificar a causa de falhas de execução.  
  
-   **Painel do Integration Services** – este relatório fornece uma visão geral de todas as execuções de pacote na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nas últimas 24 horas. O relatório exibe informações, como Status, Tipo de Operação, Nome do Pacote, etc., para cada pacote.  
  
     A Hora de Início, a Hora de Término e a Duração podem ser interpretadas desta forma:  
  
    -   Se o pacote ainda estiver em execução, Duração = hora atual – Hora de Início  
  
    -   Se o pacote tiver sido concluído, Duração = Hora de Término – Hora de Início  
  
     Para cada pacote executado no servidor, o painel permite "ampliar" para localizar detalhes específicos sobre erros de execução de pacote que possam ter ocorrido. Por exemplo, clique em **Visão Geral** para exibir uma visão geral de alto nível do status das tarefas na execução, ou em **Todas as Mensagens** para exibir as mensagens detalhadas que foram capturadas como parte da execução do pacote.  
  
     Você pode filtrar a tabela exibida em qualquer página clicando em **Filtrar** e, em seguida, selecionando os critérios na caixa de diálogo **Configurações de Filtro** . Os critérios de filtro disponíveis dependem dos dados sendo exibidos. É possível alterar a ordem de classificação do relatório clicando no ícone de classificação na caixa de diálogo **Configurações de Filtro** .  
  
-   **Relatório de Atividade – Todas as Execuções** – este relatório exibe um resumo de todas as execuções do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que foram efetuadas no servidor. O resumo exibe informações para cada execução, como status, hora de início e hora de término. Cada entrada resumida inclui links para mais informações sobre a execução, inclusive mensagens geradas durante a execução e dados de desempenho. Como no Painel do Integration Services, você pode aplicar um filtro à tabela para reduzir as informações exibidas.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Relatórios do servidor do Integration Services](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports)  
  
 [Solucionando problemas de ferramentas para execução de pacotes](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)  
  
  
