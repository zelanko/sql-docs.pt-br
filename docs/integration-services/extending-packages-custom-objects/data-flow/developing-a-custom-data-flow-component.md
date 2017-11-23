---
title: Desenvolvendo um componente de fluxo de dados personalizado | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-custom-objects
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow task [Integration Services], extending
- data flow [Integration Services], extending
- extending data flow task [Integration Services]
- components [Integration Services], data flow
ms.assetid: be126913-2a9a-41c9-9bf5-a7b0a0aea2f8
caps.latest.revision: 57
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: f25c74b52eaccb6c7b0e92cb7dace3d56f3cdd83
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="developing-a-custom-data-flow-component"></a>Desenvolvendo um componente de fluxo de dados personalizado
  A tarefa de fluxo de dados consiste em componentes que se conectam a uma variedade de fontes de dados e, em seguida, transformam e roteiam esses dados em alta velocidade. [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] fornece um modelo de objeto extensível que permite aos desenvolvedores criar fontes personalizadas, transformações e destinos que você pode usar em [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] e em pacotes implantados. Esta seção contém tópicos com orientações para desenvolvimento de componentes de fluxo de dados personalizados.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Criando um componente de fluxo de dados personalizados](../../../integration-services/extending-packages-custom-objects/data-flow/creating-a-custom-data-flow-component.md)  
 Descreve as etapas iniciais de criação de um componente de fluxo de dados personalizado.  
  
 [Métodos de tempo de design de um componente de fluxo de dados](../../../integration-services/extending-packages-custom-objects/data-flow/design-time-methods-of-a-data-flow-component.md)  
 Descreve os métodos de tempo de design para implementar em um componente de fluxo de dados personalizado.  
  
 [Métodos de tempo de execução de um componente de fluxo de dados](../../../integration-services/extending-packages-custom-objects/data-flow/run-time-methods-of-a-data-flow-component.md)  
 Descreve os métodos de tempo de execução para implementar em um componente de fluxo de dados personalizado.  
  
 [Plano de execução e alocação de Buffer](../../../integration-services/extending-packages-custom-objects/data-flow/execution-plan-and-buffer-allocation.md)  
 Descreve o plano de execução de fluxo de dados e a alocação de buffers de dados.  
  
 [Trabalhando com tipos de dados no fluxo de dados](../../../integration-services/extending-packages-custom-objects/data-flow/working-with-data-types-in-the-data-flow.md)  
 Explica como o fluxo de dados mapeia tipos de dados do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] para tipos de dados gerenciados do .NET Framework.  
  
 [Validando um componente de fluxo de dados](../../../integration-services/extending-packages-custom-objects/data-flow/validating-a-data-flow-component.md)  
 Explica os métodos usados para validar a configuração do componente e reconfigurar os metadados do componente.  
  
 [Implementando metadados externos](../../../integration-services/extending-packages-custom-objects/data-flow/implementing-external-metadata.md)  
 Explica como usar colunas de metadados externas para validação de dados.  
  
 [Gerando e definindo eventos em dados de um componente de fluxo](../../../integration-services/extending-packages-custom-objects/data-flow/raising-and-defining-events-in-a-data-flow-component.md)  
 Explica como gerar eventos predefinidos e personalizados.  
  
 [Componente de fluxo de log e definindo entradas de Log em dados](../../../integration-services/extending-packages-custom-objects/data-flow/logging-and-defining-log-entries-in-a-data-flow-component.md)  
 Explica como criar e gravar em entradas de log personalizadas.  
  
 [Usando saídas de erro em um componente de fluxo de dados](../../../integration-services/extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)  
 Explica como redirecionar linhas de erro a uma saída alternativa.  
  
 [Atualizar a versão de um componente de fluxo de dados](../../../integration-services/extending-packages-custom-objects/data-flow/upgrading-the-version-of-a-data-flow-component.md)  
 Explica como atualizar metadados de componentes salvos quando uma versão nova de seu componente é usada pela primeira vez.  
  
 [Desenvolvendo uma Interface de usuário para um componente de fluxo de dados](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-user-interface-for-a-data-flow-component.md)  
 Explica como implementar um editor personalizado para um componente.  
  
 [Desenvolvendo tipos específicos de dados de componentes de fluxo](../../../integration-services/extending-packages-custom-objects-data-flow-types/developing-specific-types-of-data-flow-components.md)  
 Contém informações sobre como desenvolver os três tipos de componentes de fluxo de dados: origens, transformações e destinos.  
  
## <a name="reference"></a>Referência  
 <xref:Microsoft.SqlServer.Dts.Pipeline>  
 Contém as classes e interfaces usadas para criar componentes de fluxo de dados personalizados.  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper>  
 Contém as classes e interfaces que constituem o modelo de objeto da tarefa de fluxo de dados, e é usado para criar componentes de fluxo de dados personalizados ou compilar uma tarefa de fluxo de dados.  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Design>  
 Contém as classes e interfaces usadas para criar a interface do usuário para componentes de fluxo de dados.  
  
 [Referência de mensagens e erros do Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)  
 Lista os códigos de erro predefinidos do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] com seus nomes simbólicos e descrições.  
  
## <a name="related-sections"></a>Seções relacionadas  
  
### <a name="information-common-to-all-custom-objects"></a>Informações comuns a todos os objetos personalizados  
 Para obter informações comuns a todos os tipos de objetos personalizados que você pode criar no [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], consulte os tópicos a seguir:  
  
 [Desenvolvendo objetos personalizados para o Integration Services](../../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)  
 Descreve as etapas básicas para implementar todos os tipos de objetos personalizados para [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)].  
  
 [Persistência de objetos personalizados](../../../integration-services/extending-packages-custom-objects/persisting-custom-objects.md)  
 Descreve a persistência personalizada e explica quando ela é necessária.  
  
 [Compilando, implantando e depurando objetos personalizados](../../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)  
 Descreve as técnicas para compilar, assinar, implantar e depurar objetos personalizados.  
  
### <a name="information-about-other-custom-objects"></a>Informações sobre outros objetos personalizados  
 Para obter informações sobre os outros tipos de objetos personalizados que você pode criar em [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], consulte os seguintes tópicos:  
  
 [Desenvolvendo uma tarefa personalizada](../../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)  
 Aborda como programar tarefas personalizadas.  
  
 [Desenvolvendo um Gerenciador de Conexão personalizado](../../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md)  
 Aborda como programar gerenciadores de conexões personalizados.  
  
 [Desenvolvendo um provedor de Log personalizado](../../../integration-services/extending-packages-custom-objects/log-provider/developing-a-custom-log-provider.md)  
 Aborda como programar provedores de log personalizados.  
  
 [Desenvolvendo um enumerador ForEach personalizado](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/developing-a-custom-foreach-enumerator.md)  
 Aborda como programar enumeradores personalizados.  
  
## <a name="see-also"></a>Consulte também  
 [Estendendo o fluxo de dados com o componente Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)   
 [Comparando soluções de script e objetos personalizados](../../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)  
  
  

