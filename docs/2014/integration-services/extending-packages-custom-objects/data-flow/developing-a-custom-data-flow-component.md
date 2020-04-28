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
ms.openlocfilehash: 061daaa3b44c151a1f77b075bef66ef90570af98
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "78176334"
---
# <a name="developing-a-custom-data-flow-component"></a>Desenvolvendo um componente de fluxo de dados personalizado
  A tarefa de fluxo de dados consiste em componentes que se conectam a uma variedade de fontes de dados e, em seguida, transformam e roteiam esses dados em alta velocidade. O [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] fornece um modelo de objeto extensível que permite que os desenvolvedores criem origens, transformações e destinos personalizados que você pode usar no [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] e em pacotes implantados. Esta seção contém tópicos com orientações para desenvolvimento de componentes de fluxo de dados personalizados.

## <a name="in-this-section"></a>Nesta seção
 [Criando um componente de fluxo de dados personalizado](creating-a-custom-data-flow-component.md) Descreve as etapas iniciais na criação de um componente de fluxo de dados personalizado.

 [Métodos de tempo de design de um componente de fluxo de dados](design-time-methods-of-a-data-flow-component.md) Descreve os métodos de tempo de design para implementar em um componente de fluxo de dados personalizado.

 [Métodos de tempo de execução de um componente de fluxo de dados](run-time-methods-of-a-data-flow-component.md) Descreve os métodos de tempo de execução para implementar em um componente de fluxo de dados personalizado.

 [Plano de execução e alocação de buffer](execution-plan-and-buffer-allocation.md) Descreve o plano de execução de fluxo de dados e a alocação de buffers de dados.

 [Trabalhando com tipos de dados no fluxo de dados](working-with-data-types-in-the-data-flow.md) Explica como o fluxo de dados [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] mapeia tipos de dados para .NET Framework tipos de dados gerenciados.

 [Validando um componente de fluxo de dados](validating-a-data-flow-component.md) Explica os métodos usados para validar a configuração do componente e reconfigurar os metadados do componente.

 [Implementando metadados externos](implementing-external-metadata.md) Explica como usar colunas de metadados externos para validação de dados.

 [Gerando e definindo eventos em um componente de fluxo de dados](raising-and-defining-events-in-a-data-flow-component.md) Explica como gerar eventos personalizados e predefinidos.

 [Registrando e definindo entradas de log em um componente de fluxo de dados](logging-and-defining-log-entries-in-a-data-flow-component.md) Explica como criar e gravar em entradas de log personalizadas.

 [Usando saídas de erro em um componente de fluxo de dados](using-error-outputs-in-a-data-flow-component.md) Explica como redirecionar linhas de erro para uma saída alternativa.

 [Atualizando a versão de um componente de fluxo de dados](upgrading-the-version-of-a-data-flow-component.md) Explica como atualizar metadados de componente salvos quando uma nova versão do seu componente é usada pela primeira vez.

 [Desenvolvendo uma interface do usuário para um componente de fluxo de dados](developing-a-user-interface-for-a-data-flow-component.md) Explica como implementar um editor personalizado para um componente.

 [Desenvolvendo tipos específicos de componentes de fluxo de dados](../../extending-packages-custom-objects-data-flow-types/developing-specific-types-of-data-flow-components.md) Contém informações sobre como desenvolver os três tipos de componentes de fluxo de dados: fontes, transformações e destinos.

## <a name="reference"></a>Referência
 <xref:Microsoft.SqlServer.Dts.Pipeline>Contém as classes e interfaces usadas para criar componentes de fluxo de dados personalizados.

 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper>Contém as classes e as interfaces que compõem o modelo de objeto de tarefa de fluxo de dados e é usado para criar componentes de fluxo de dados personalizados ou criar uma tarefa de fluxo de dados.

 <xref:Microsoft.SqlServer.Dts.Pipeline.Design>Contém as classes e interfaces usadas para criar a interface do usuário para componentes de fluxo de dados.

 [Integration Services referência de erro e mensagem](../../integration-services-error-and-message-reference.md) Lista os códigos [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] de erro predefinidos com seus nomes simbólicos e descrições.

## <a name="related-sections"></a>Seções relacionadas

### <a name="information-common-to-all-custom-objects"></a>Informações comuns a todos os objetos personalizados
 Para obter informações comuns a todos os tipos de objetos personalizados que você pode criar no [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], consulte os tópicos a seguir:

 [Desenvolvendo objetos personalizados para Integration Services](../../extending-packages-custom-objects/developing-custom-objects-for-integration-services.md) Descreve as etapas básicas na implementação de todos os tipos de objetos [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]personalizados para o.

 [Persistência de objetos personalizados](../../extending-packages-custom-objects/persisting-custom-objects.md) Descreve a persistência personalizada e explica quando é necessário.

 [Criando, implantando e depurando objetos personalizados](../../extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md) Descreve as técnicas para criar, assinar, implantar e depurar objetos personalizados.

### <a name="information-about-other-custom-objects"></a>Informações sobre outros objetos personalizados
 Para obter informações sobre os outros tipos de objetos personalizados que você pode criar no [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], consulte os tópicos a seguir:

 [Desenvolvendo uma tarefa personalizada](../../extending-packages-custom-objects/task/developing-a-custom-task.md) Discute como programar tarefas personalizadas.

 [Desenvolvendo um Gerenciador de conexões personalizado](../../extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md) Discute como programar gerenciadores de conexões personalizados.

 [Desenvolvendo um provedor de log personalizado](../../extending-packages-custom-objects/log-provider/developing-a-custom-log-provider.md) Discute como programar provedores de log personalizados.

 [Desenvolvendo um enumerador foreach personalizado](../../extending-packages-custom-objects/foreach-enumerator/developing-a-custom-foreach-enumerator.md) Discute como programar enumeradores personalizados.

![Ícone de Integration Services (pequeno)](../../media/dts-16.gif "Ícone do Integration Services (pequeno)")  **Mantenha-se atualizado com Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.

## <a name="see-also"></a>Consulte Também
 [Estendendo o fluxo de dados com o componente Script] (.. /.. /Extending-Packages-scripting/data-Flow-script-Component/Extending-The-data-Flow-with-the-script-Component.MD [comparando soluções de script e objetos personalizados](../../extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)


