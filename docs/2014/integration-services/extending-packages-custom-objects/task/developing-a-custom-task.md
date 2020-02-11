---
title: Desenvolver uma tarefa personalizada | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: 7f597ee3a063da534267f7d4674a024a8fcc02f1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62896137"
---
# <a name="developing-a-custom-task"></a>Desenvolvendo uma tarefa personalizada
  O [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] usa tarefas para executar unidades de trabalho como suporte à extração, transformação e carregamento de dados. O [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] inclui várias tarefas que executam as ações usadas mais frequentemente, da execução de uma instrução SQL ao download de um arquivo de um site de FTP. Se as tarefas incluídas e as ações suportadas não satisfizerem seus requisitos completamente, você poderá criar uma tarefa personalizada.  
  
 Para criar uma tarefa personalizada, é preciso criar uma classe que herde da classe base <xref:Microsoft.SqlServer.Dts.Runtime.Task>, aplicar o atributo <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute> em sua nova classe e substituir os métodos e propriedades importantes da classe base, incluindo o método <xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A>.  
  
## <a name="in-this-section"></a>Nesta seção  
 Esta seção descreve como criar, configurar e codificar uma tarefa personalizada e sua interface de usuário personalizada opcional.  
  
 [Criar uma tarefa personalizada](creating-a-custom-task.md)  
 Descreve a primeira etapa, que é criar a tarefa personalizada.  
  
 [Codificar uma tarefa personalizada](coding-a-custom-task.md)  
 Descreve como codificar os métodos principais de uma tarefa personalizada.  
  
 [Conectar-se a fontes de dados em uma tarefa personalizada](connecting-to-data-sources-in-a-custom-task.md)  
 Descreve como conectar uma tarefa personalizada a uma fonte de dados.  
  
 [Gerar e definir eventos em uma tarefa personalizada](raising-and-defining-events-in-a-custom-task.md)  
 Descreve como gerar eventos e definir eventos personalizados da tarefa personalizada.  
  
 [Adicionar suporte para depuração em uma tarefa personalizada](adding-support-for-debugging-in-a-custom-task.md)  
 Descreve como criar destinos de ponto de interrupção na tarefa personalizada.  
  
 [Desenvolver uma interface do usuário para uma tarefa personalizada](developing-a-user-interface-for-a-custom-task.md)  
 Descreve como criar uma interface de usuário que seja exibida no [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer para configurar propriedades na tarefa personalizada.  
  
## <a name="related-sections"></a>Seções relacionadas  
  
### <a name="information-common-to-all-custom-objects"></a>Informações comuns a todos os objetos personalizados  
 Para obter informações comuns a todos os tipos de objetos personalizados que você pode criar no [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], consulte os tópicos a seguir:  
  
 [Desenvolvendo objetos personalizados para o Integration Services](../developing-custom-objects-for-integration-services.md)  
 Descreve as etapas básicas para implementar todos os tipos de objetos personalizados no [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)].  
  
 [Persistência de objetos personalizados](../persisting-custom-objects.md)  
 Descreve a persistência personalizada e explica quando ela é necessária.  
  
 [Compilando, implantando e depurando objetos personalizados](../building-deploying-and-debugging-custom-objects.md)  
 Descreve as técnicas para compilar, assinar, implantar e depurar objetos personalizados.  
  
### <a name="information-about-other-custom-objects"></a>Informações sobre outros objetos personalizados  
 Para obter informações sobre os outros tipos de objetos personalizados que você pode criar no [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], consulte os tópicos a seguir:  
  
 [Desenvolver um gerenciador de conexões personalizado](../connection-manager/developing-a-custom-connection-manager.md)  
 Aborda como programar gerenciadores de conexões personalizados.  
  
 [Desenvolver um provedor de log personalizado](../log-provider/developing-a-custom-log-provider.md)  
 Aborda como programar provedores de log personalizados.  
  
 [Desenvolver um enumerador ForEach personalizado](../foreach-enumerator/developing-a-custom-foreach-enumerator.md)  
 Aborda como programar enumeradores personalizados.  
  
 [Desenvolver um componente de fluxo de dados personalizado](../data-flow/developing-a-custom-data-flow-component.md)  
 Aborda como programar origens, transformações e destinos de fluxos de dados personalizados.  
  
![Ícone de Integration Services (pequeno)](../../media/dts-16.gif "Ícone do Integration Services (pequeno)")  **Mantenha-se atualizado com Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte Também  
 [Estender o pacote com a tarefa Script](../../extending-packages-scripting/task/extending-the-package-with-the-script-task.md)   
 [Comparar soluções de script e objetos personalizados](../../extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)  
  
  
