---
title: Desenvolver uma tarefa personalizada | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom tasks [Integration Services], about custom tasks
- Task class
- custom tasks [Integration Services]
- SSIS custom tasks
- SSIS custom tasks, about custom tasks
- IDtsTaskUI interface
- DtsTaskAttribute attribute
- tasks [Integration Services], custom
- TaskHost object
ms.assetid: dcbd8615-fa6d-4ddb-b8a5-0b19dddd6239
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 75522733a4054bd0a827913fee3cca060c2bdbdc
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65724399"
---
# <a name="developing-a-custom-task"></a>Desenvolvendo uma tarefa personalizada

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  O [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] usa tarefas para executar unidades de trabalho como suporte à extração, transformação e carregamento de dados. O [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] inclui várias tarefas que executam as ações usadas mais frequentemente, da execução de uma instrução SQL ao download de um arquivo de um site de FTP. Se as tarefas incluídas e as ações suportadas não satisfizerem seus requisitos completamente, você poderá criar uma tarefa personalizada.  
  
 Para criar uma tarefa personalizada, é preciso criar uma classe que herde da classe base <xref:Microsoft.SqlServer.Dts.Runtime.Task>, aplicar o atributo <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute> em sua nova classe e substituir os métodos e propriedades importantes da classe base, incluindo o método <xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A>.  
  
## <a name="in-this-section"></a>Nesta seção  
 Esta seção descreve como criar, configurar e codificar uma tarefa personalizada e sua interface de usuário personalizada opcional.  
  
 [Criar uma tarefa personalizada](../../../integration-services/extending-packages-custom-objects/task/creating-a-custom-task.md)  
 Descreve a primeira etapa, que é criar a tarefa personalizada.  
  
 [Codificar uma tarefa personalizada](../../../integration-services/extending-packages-custom-objects/task/coding-a-custom-task.md)  
 Descreve como codificar os métodos principais de uma tarefa personalizada.  
  
 [Conectar-se a fontes de dados em uma tarefa personalizada](../../../integration-services/extending-packages-custom-objects/task/connecting-to-data-sources-in-a-custom-task.md)  
 Descreve como conectar uma tarefa personalizada a uma fonte de dados.  
  
 [Gerar e definir eventos em uma tarefa personalizada](../../../integration-services/extending-packages-custom-objects/task/raising-and-defining-events-in-a-custom-task.md)  
 Descreve como gerar eventos e definir eventos personalizados da tarefa personalizada.  
  
 [Adicionar suporte para depuração em uma tarefa personalizada](../../../integration-services/extending-packages-custom-objects/task/adding-support-for-debugging-in-a-custom-task.md)  
 Descreve como criar destinos de ponto de interrupção na tarefa personalizada.  
  
 [Desenvolver uma interface do usuário para uma tarefa personalizada](../../../integration-services/extending-packages-custom-objects/task/developing-a-user-interface-for-a-custom-task.md)  
 Descreve como criar uma interface de usuário que seja exibida no [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer para configurar propriedades na tarefa personalizada.  
  
## <a name="related-sections"></a>Seções relacionadas  
  
### <a name="information-common-to-all-custom-objects"></a>Informações comuns a todos os objetos personalizados  
 Para obter informações comuns a todos os tipos de objetos personalizados que você pode criar no [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], consulte os tópicos a seguir:  
  
 [Desenvolvendo objetos personalizados para o Integration Services](../../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)  
 Descreve as etapas básicas para implementar todos os tipos de objetos personalizados no [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)].  
  
 [Persistência de objetos personalizados](../../../integration-services/extending-packages-custom-objects/persisting-custom-objects.md)  
 Descreve a persistência personalizada e explica quando ela é necessária.  
  
 [Compilando, implantando e depurando objetos personalizados](../../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)  
 Descreve as técnicas para compilar, assinar, implantar e depurar objetos personalizados.  
  
### <a name="information-about-other-custom-objects"></a>Informações sobre outros objetos personalizados  
 Para obter informações sobre os outros tipos de objetos personalizados que você pode criar no [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], consulte os tópicos a seguir:  
  
 [Desenvolver um gerenciador de conexões personalizado](../../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md)  
 Aborda como programar gerenciadores de conexões personalizados.  
  
 [Desenvolver um provedor de log personalizado](../../../integration-services/extending-packages-custom-objects/log-provider/developing-a-custom-log-provider.md)  
 Aborda como programar provedores de log personalizados.  
  
 [Desenvolver um enumerador ForEach personalizado](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/developing-a-custom-foreach-enumerator.md)  
 Aborda como programar enumeradores personalizados.  
  
 [Desenvolver um componente de fluxo de dados personalizado](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)  
 Aborda como programar origens, transformações e destinos de fluxos de dados personalizados.  
  
## <a name="see-also"></a>Consulte Também  
 [Estender o pacote com a tarefa Script](../../../integration-services/extending-packages-scripting/task/extending-the-package-with-the-script-task.md)   
 [Comparar soluções de script e objetos personalizados](../../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)  
  
  
