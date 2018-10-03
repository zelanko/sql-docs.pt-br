---
title: Desenvolver um enumerador ForEach personalizado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.topic: reference
helpviewer_keywords:
- custom foreach enumerators [Integration Services]
- custom foreach enumerators [Integration Services], about custom foreach enumerators
- foreach enumerators [Integration Services]
ms.assetid: bffe26e0-1b9a-47ad-bae6-6b708cb4cf4f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 07df48880932c5e40c2ce8923b87d5c5ddbef876
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48085016"
---
# <a name="developing-a-custom-foreach-enumerator"></a>Desenvolvendo um enumerador de ForEach personalizado
  O [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] usa enumeradores foreach para iterar sobre os itens de uma coleção e executar as mesmas tarefas para cada elemento. O [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] inclui vários enumeradores foreach que dão suporte às coleções mais usadas, como todos os arquivos de uma pasta, todas as tabelas de um banco de dados ou todos os elementos de uma lista armazenada em uma variável de pacote. Se os enumeradores de foreach e as coleções fornecidos não satisfizerem seus requisitos completamente, você poderá criar um enumerador de foreach personalizado.  
  
 Para criar um enumerador de foreach personalizado, é preciso criar uma classe que herde da classe base <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator>, aplicar o atributo <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute> em sua nova classe e substituir os métodos e propriedades importantes da classe base, incluindo o método <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A>.  
  
## <a name="in-this-section"></a>Nesta seção  
 Esta seção descreve como criar, configurar e codificar um enumerador foreach personalizado e sua interface de usuário personalizada.  
  
 [Criar um enumerador Foreach personalizado](creating-a-custom-foreach-enumerator.md)  
 Descreve como criar as classes para um projeto de enumerador foreach personalizado.  
  
 [Codificar um enumerador Foreach personalizado](coding-a-custom-foreach-enumerator.md)  
 Descreve como implementar um enumerador de foreach personalizado anulando os métodos e propriedades da classe base.  
  
 [Desenvolver uma interface do usuário para um enumerador ForEach personalizado](developing-a-user-interface-for-a-custom-foreach-enumerator.md)  
 Descreve como implementar a classe de interface do usuário e o formulário usado para configurar o enumerador foreach personalizado.  
  
## <a name="related-topics"></a>Tópicos relacionados  
  
### <a name="information-common-to-all-custom-objects"></a>Informações comuns a todos os objetos personalizados  
 Para obter informações comuns a todos os tipos de objetos personalizados que você pode criar no [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], consulte os tópicos a seguir:  
  
 [Desenvolvendo objetos personalizados para o Integration Services](../developing-custom-objects-for-integration-services.md)  
 Descreve as etapas básicas para implementar todos os tipos de objetos personalizados para [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)].  
  
 [Persistência de objetos personalizados](../persisting-custom-objects.md)  
 Descreve a persistência personalizada e explica quando ela é necessária.  
  
 [Compilando, implantando e depurando objetos personalizados](../building-deploying-and-debugging-custom-objects.md)  
 Descreve as técnicas para compilar, assinar, implantar e depurar objetos personalizados.  
  
### <a name="information-about-other-custom-objects"></a>Informações sobre outros objetos personalizados  
 Para obter informações sobre os outros tipos de objetos personalizados que você pode criar no [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], consulte os tópicos a seguir:  
  
 [Desenvolver uma tarefa personalizada](../task/developing-a-custom-task.md)  
 Aborda como programar tarefas personalizadas.  
  
 [Desenvolver um gerenciador de conexões personalizado](../connection-manager/developing-a-custom-connection-manager.md)  
 Aborda como programar gerenciadores de conexões personalizados.  
  
 [Desenvolver um provedor de log personalizado](../log-provider/developing-a-custom-log-provider.md)  
 Aborda como programar provedores de log personalizados.  
  
 [Desenvolver um componente de fluxo de dados personalizado](../data-flow/developing-a-custom-data-flow-component.md)  
 Aborda como programar origens, transformações e destinos de fluxos de dados personalizados.  
  
![Ícone do Integration Services (pequeno)](../../media/dts-16.gif "ícone do Integration Services (pequeno)")**mantenha-se para cima até o momento com o Integration Services** <br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
  
