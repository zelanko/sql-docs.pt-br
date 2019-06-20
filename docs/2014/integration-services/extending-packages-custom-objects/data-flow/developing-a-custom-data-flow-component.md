---
title: Desenvolver um componente de fluxo de dados personalizado | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow task [Integration Services], extending
- data flow [Integration Services], extending
- extending data flow task [Integration Services]
- components [Integration Services], data flow
ms.assetid: be126913-2a9a-41c9-9bf5-a7b0a0aea2f8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6c174fe5cdf1ebe1dbc9b0350a01fb6e8027effa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768962"
---
# <a name="developing-a-custom-data-flow-component"></a>Desenvolvendo um componente de fluxo de dados personalizado
  A tarefa de fluxo de dados consiste em componentes que se conectam a uma variedade de fontes de dados e, em seguida, transformam e roteiam esses dados em alta velocidade. O [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] fornece um modelo de objeto extensível que permite que os desenvolvedores criem origens, transformações e destinos personalizados que você pode usar no [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] e em pacotes implantados. Esta seção contém tópicos com orientações para desenvolvimento de componentes de fluxo de dados personalizados.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Criar um componente de fluxo de dados personalizado](creating-a-custom-data-flow-component.md)  
 Descreve as etapas iniciais de criação de um componente de fluxo de dados personalizado.  
  
 [Métodos de tempo de design de um componente de fluxo de dados](design-time-methods-of-a-data-flow-component.md)  
 Descreve os métodos de tempo de design para implementar em um componente de fluxo de dados personalizado.  
  
 [Métodos de tempo de execução de um componente de fluxo de dados](run-time-methods-of-a-data-flow-component.md)  
 Descreve os métodos de tempo de execução para implementar em um componente de fluxo de dados personalizado.  
  
 [Plano de execução e alocação de buffer](execution-plan-and-buffer-allocation.md)  
 Descreve o plano de execução de fluxo de dados e a alocação de buffers de dados.  
  
 [Trabalhando com tipos de dados no fluxo de dados](working-with-data-types-in-the-data-flow.md)  
 Explica como o fluxo de dados mapeia tipos de dados do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] para tipos de dados gerenciados do .NET Framework.  
  
 [Validando um componente de fluxo de dados](validating-a-data-flow-component.md)  
 Explica os métodos usados para validar a configuração do componente e reconfigurar os metadados do componente.  
  
 [Implementando metadados externos](implementing-external-metadata.md)  
 Explica como usar colunas de metadados externas para validação de dados.  
  
 [Gerando e definindo eventos em um componente de fluxo de dados](raising-and-defining-events-in-a-data-flow-component.md)  
 Explica como gerar eventos predefinidos e personalizados.  
  
 [Registrando em log e definindo entradas de log em um componente de fluxo de dados](logging-and-defining-log-entries-in-a-data-flow-component.md)  
 Explica como criar e gravar em entradas de log personalizadas.  
  
 [Usando saídas de erro em um componente de fluxo de dados](using-error-outputs-in-a-data-flow-component.md)  
 Explica como redirecionar linhas de erro a uma saída alternativa.  
  
 [Atualizando a versão de um componente de fluxo de dados](upgrading-the-version-of-a-data-flow-component.md)  
 Explica como atualizar metadados de componentes salvos quando uma versão nova de seu componente é usada pela primeira vez.  
  
 [Desenvolvendo uma interface do usuário para um componente de fluxo de dados](developing-a-user-interface-for-a-data-flow-component.md)  
 Explica como implementar um editor personalizado para um componente.  
  
 [Desenvolvendo tipos específicos de componentes de fluxo de dados](../../extending-packages-custom-objects-data-flow-types/developing-specific-types-of-data-flow-components.md)  
 Contém informações sobre como desenvolver os três tipos de componentes de fluxo de dados: origens, transformações e destinos.  
  
## <a name="reference"></a>Referência  
 <xref:Microsoft.SqlServer.Dts.Pipeline>  
 Contém as classes e interfaces usadas para criar componentes de fluxo de dados personalizados.  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper>  
 Contém as classes e interfaces que constituem o modelo de objeto da tarefa de fluxo de dados, e é usado para criar componentes de fluxo de dados personalizados ou compilar uma tarefa de fluxo de dados.  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Design>  
 Contém as classes e interfaces usadas para criar a interface do usuário para componentes de fluxo de dados.  
  
 [Referência de mensagens e erros do Integration Services](../../integration-services-error-and-message-reference.md)  
 Lista os códigos de erro predefinidos do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] com seus nomes simbólicos e descrições.  
  
## <a name="related-sections"></a>Seções relacionadas  
  
### <a name="information-common-to-all-custom-objects"></a>Informações comuns a todos os objetos personalizados  
 Para obter informações comuns a todos os tipos de objetos personalizados que você pode criar no [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], consulte os tópicos a seguir:  
  
 [Desenvolvendo objetos personalizados para o Integration Services](../../extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)  
 Descreve as etapas básicas para implementar todos os tipos de objetos personalizados para [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)].  
  
 [Persistência de objetos personalizados](../../extending-packages-custom-objects/persisting-custom-objects.md)  
 Descreve a persistência personalizada e explica quando ela é necessária.  
  
 [Compilando, implantando e depurando objetos personalizados](../../extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)  
 Descreve as técnicas para compilar, assinar, implantar e depurar objetos personalizados.  
  
### <a name="information-about-other-custom-objects"></a>Informações sobre outros objetos personalizados  
 Para obter informações sobre os outros tipos de objetos personalizados que você pode criar no [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], consulte os tópicos a seguir:  
  
 [Desenvolver uma tarefa personalizada](../../extending-packages-custom-objects/task/developing-a-custom-task.md)  
 Aborda como programar tarefas personalizadas.  
  
 [Desenvolver um gerenciador de conexões personalizado](../../extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md)  
 Aborda como programar gerenciadores de conexões personalizados.  
  
 [Desenvolver um provedor de log personalizado](../../extending-packages-custom-objects/log-provider/developing-a-custom-log-provider.md)  
 Aborda como programar provedores de log personalizados.  
  
 [Desenvolver um enumerador ForEach personalizado](../../extending-packages-custom-objects/foreach-enumerator/developing-a-custom-foreach-enumerator.md)  
 Aborda como programar enumeradores personalizados.  
  
![Ícone do Integration Services (pequeno)](../../media/dts-16.gif "ícone do Integration Services (pequeno)")**mantenha-se para cima até o momento com o Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte também  
 [Estender o fluxo de dados com o componente Script] (.. /.. /Extending-Packages-Scripting/Data-Flow-script-Component/Extending-the-Data-Flow-with-the-script-Component.MD   
 [Comparar soluções de script e objetos personalizados](../../extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)  
  
  
