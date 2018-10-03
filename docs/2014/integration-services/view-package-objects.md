---
title: Exibir objetos de pacote | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, properties
- properties [Integration Services]
- Package Explorer window [Integration Services]
- packages [Integration Services], properties
- explorer view [Integration Services]
- SSIS packages, properties
- viewing package objects
- SQL Server Integration Services packages, properties
ms.assetid: a85c0245-0a68-4eb0-83b1-9b11df80bd10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 568773a255c6a1d264544ef540d88fa6afa0d277
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48163246"
---
# <a name="view-package-objects"></a>Exibir objetos do pacote
  No Designer do [!INCLUDE[ssIS](../includes/ssis-md.md)] , a guia **Explorador de Pacotes** fornece uma exibição de explorer do pacote. A exibição reflete a hierarquia de contêiner da arquitetura [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . O contêiner de pacote está no topo da hierarquia e você expande o pacote para exibir as conexões, executáveis, manipuladores de eventos, provedores de log, restrições de precedência e variáveis no pacote.  
  
 Os executáveis, que são contêineres e tarefas do pacote, podem incluir manipuladores de eventos, restrições de precedência e variáveis. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] dá suporte a uma hierarquia de contêineres aninhada, e os contêineres Loop For, Loop Foreach e Sequência podem incluir outros executáveis.  
  
 Se um pacote incluir um fluxo de dados, o **Explorador de Pacotes** listará a tarefa de Fluxo de Dados e incluirá uma pasta **Componentes** que lista os componentes de fluxo de dados.  
  
 Na guia **Explorador de Pacotes** , você pode excluir objetos em um pacote e acessar a janela **Propriedades** para exibir as propriedades do objeto.  
  
 O diagrama a seguir mostra uma exibição de árvore de um pacote simples.  
  
 ![Captura de tela da guia Explorador de Pacotes](media/packageexplorer.gif "Captura de tela da guia Explorador de Pacotes")  
  
### <a name="to-view-package-content"></a>Para exibir o conteúdo do pacote  
  
-   [Exibir objetos de pacote no Explorador de Pacotes](../../2014/integration-services/view-package-objects-in-package-explorer.md)  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas do Integration Services](control-flow/integration-services-tasks.md)   
 [Contêineres do Integration Services](control-flow/integration-services-containers.md)   
 [Restrições de precedência](control-flow/precedence-constraints.md)   
 [Serviços de integração &#40;SSIS&#41; variáveis](integration-services-ssis-variables.md)   
 [Manipuladores de eventos do SSIS &#40;Integration Services&#41;](integration-services-ssis-event-handlers.md)   
 [Registro em Log do SSIS &#40;Integration Services&#41;](performance/integration-services-ssis-logging.md)  
  
  
