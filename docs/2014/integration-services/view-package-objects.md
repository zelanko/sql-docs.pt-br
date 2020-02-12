---
title: Exibir objetos de pacote | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
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
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 78a9b551ae44348de1c007533be3606b33c974cd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62926272"
---
# <a name="view-package-objects"></a>Exibir objetos do pacote
  No Designer do [!INCLUDE[ssIS](../includes/ssis-md.md)] , a guia **Explorador de Pacotes** fornece uma exibição de explorer do pacote. A exibição reflete a hierarquia de contêiner da arquitetura [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . O contêiner de pacote está no topo da hierarquia e você expande o pacote para exibir as conexões, executáveis, manipuladores de eventos, provedores de log, restrições de precedência e variáveis no pacote.  
  
 Os executáveis, que são contêineres e tarefas do pacote, podem incluir manipuladores de eventos, restrições de precedência e variáveis. 
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] dá suporte a uma hierarquia de contêineres aninhada, e os contêineres Loop For, Loop Foreach e Sequência podem incluir outros executáveis.  
  
 Se um pacote incluir um fluxo de dados, o **Explorador de Pacotes** listará a tarefa de Fluxo de Dados e incluirá uma pasta **Componentes** que lista os componentes de fluxo de dados.  
  
 Na guia **Explorador de Pacotes** , você pode excluir objetos em um pacote e acessar a janela **Propriedades** para exibir as propriedades do objeto.  
  
 O diagrama a seguir mostra uma exibição de árvore de um pacote simples.  
  
 ![Captura de tela da guia Explorador de Pacotes](media/packageexplorer.gif "Captura de tela da guia Explorador de Pacotes")  
  
### <a name="to-view-package-content"></a>Para exibir o conteúdo do pacote  
  
-   [Exibir objetos de pacote no Explorador de Pacotes](../../2014/integration-services/view-package-objects-in-package-explorer.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefas do Integration Services](control-flow/integration-services-tasks.md)   
 [Contêineres do Integration Services](control-flow/integration-services-containers.md)   
 [Restrições de precedência](control-flow/precedence-constraints.md)   
 [Variáveis do SSIS &#40;Integration Services&#41;](integration-services-ssis-variables.md)   
 [Manipuladores de eventos do SSIS &#40;Integration Services&#41;](integration-services-ssis-event-handlers.md)   
 [Registro em Log do SSIS &#40;Integration Services&#41;](performance/integration-services-ssis-logging.md)  
  
  
