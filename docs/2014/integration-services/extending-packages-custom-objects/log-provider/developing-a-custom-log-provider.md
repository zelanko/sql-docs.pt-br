---
title: Desenvolver um provedor de logs personalizado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- SSIS packages, log providers
- custom log providers [Integration Services]
- SQL Server Integration Services packages, log providers
- log providers [Integration Services]
- packages [Integration Services], logs
- Integration Services packages, log providers
ms.assetid: 3f715b95-7074-4f5c-8ae2-246998052e78
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: af3478e254f01f7cf53d5a09b6febab3b1e85e8b
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78176289"
---
# <a name="developing-a-custom-log-provider"></a>Desenvolvendo um provedor de log personalizado
  O [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] tem recursos de log extensos que possibilitam capturar eventos que ocorrem durante a execução do pacote. O [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] inclui vários provedores de logs que permitem a criação e o armazenamento de logs em formatos como XML, texto, banco de dados ou no log de eventos do Windows. Se os provedores de log e os formatos de saída fornecidos não atenderem totalmente aos seus requisitos, você poderá criar um provedor de log personalizado.

 Para criar um provedor de log personalizado, é preciso criar uma classe que herde da classe base <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase>, aplicar o atributo <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute> à sua nova classe e substituir os métodos e as propriedades importantes da classe base, incluindo a propriedade <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.ConfigString%2A> e o método <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Log%2A>.

## <a name="in-this-section"></a>Nesta seção
 Esta seção descreve como criar, configurar e codificar um provedor de log personalizado.

 [Criando um provedor de log personalizado](creating-a-custom-log-provider.md) Descreve como criar as classes para um projeto de provedor de log personalizado.

 [Codificando um provedor de log personalizado](coding-a-custom-log-provider.md) Descreve como implementar um provedor de log personalizado substituindo os métodos e as propriedades da classe base.

 [Desenvolvendo uma interface do usuário para um provedor de log personalizado](developing-a-user-interface-for-a-custom-log-provider.md) Não há suporte para interfaces de usuário personalizadas para provedores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]log personalizados no.

## <a name="related-topics"></a>Tópicos Relacionados

### <a name="information-common-to-all-custom-objects"></a>Informações comuns a todos os objetos personalizados
 Para obter informações comuns a todos os tipos de objetos personalizados que você pode criar no [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], consulte os tópicos a seguir:

 [Desenvolvendo objetos personalizados para Integration Services](../developing-custom-objects-for-integration-services.md) Descreve as etapas básicas na implementação de todos os tipos de objetos [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]personalizados para o.

 [Persistência de objetos personalizados](../persisting-custom-objects.md) Descreve a persistência personalizada e explica quando é necessário.

 [Criando, implantando e depurando objetos personalizados](../building-deploying-and-debugging-custom-objects.md) Descreve as técnicas para criar, assinar, implantar e depurar objetos personalizados.

### <a name="information-about-other-custom-objects"></a>Informações sobre outros objetos personalizados
 Para obter informações sobre os outros tipos de objetos personalizados que você pode criar no [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], consulte os tópicos a seguir:

 [Desenvolvendo uma tarefa personalizada](../task/developing-a-custom-task.md) Discute como programar tarefas personalizadas.

 [Desenvolvendo um Gerenciador de conexões personalizado](../connection-manager/developing-a-custom-connection-manager.md) Discute como programar gerenciadores de conexões personalizados.

 [Desenvolvendo um enumerador foreach personalizado](../foreach-enumerator/developing-a-custom-foreach-enumerator.md) Discute como programar enumeradores personalizados.

 [Desenvolvendo um componente de fluxo de dados personalizado](../data-flow/developing-a-custom-data-flow-component.md) Discute como programar fontes de fluxo de dados personalizadas, transformações e destinos.

![Ícone de Integration Services (pequeno)](../../media/dts-16.gif "Ícone do Integration Services (pequeno)")  **Mantenha-se atualizado com Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.


