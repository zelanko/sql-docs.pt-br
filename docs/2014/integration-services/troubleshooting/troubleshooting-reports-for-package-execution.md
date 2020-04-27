---
title: Relatórios de solução de problemas para execução de pacotes | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 8fc476ac-bd69-434e-9636-70776e0b3b6c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1c1a59d9e77806666c487b0778edd574bcaa5e42
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62926301"
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
  
## <a name="related-tasks"></a>Related Tasks  
 [Exibir relatórios do servidor do Integration Services](../view-reports-for-the-integration-services-server.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Relatórios do servidor do Integration Services](../reports-for-the-integration-services-server.md)  
  
 [Solucionando problemas de ferramentas para execução de pacotes](troubleshooting-tools-for-package-execution.md)  
  
  
