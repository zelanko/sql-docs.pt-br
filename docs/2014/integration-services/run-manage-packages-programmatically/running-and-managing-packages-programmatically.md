---
title: Executar e gerenciar pacotes programaticamente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 1a08c75e-ce8c-45ee-81bd-32248bbdb2b2
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 659952d44fa2c530a313a4f6bd29cfbfddf9d236
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37239146"
---
# <a name="running-and-managing-packages-programmatically"></a>Executando e gerenciando pacotes programaticamente
  Se precisar gerenciar e executar pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fora do ambiente de desenvolvimento, você poderá manipular pacotes programaticamente. Nesta abordagem, você tem uma série de opções:  
  
-   Carregar e executar um pacote existente sem modificação.  
  
-   Carregar um pacote existente, reconfigurá-lo (por exemplo, para outra fonte de dados) e executá-lo.  
  
-   Criar um pacote novo, adicionar e configurar os componentes, objeto por objeto e propriedade por propriedade, salvá-lo e executá-lo.  
  
 Você pode carregar e executar um pacote existente de um aplicativo cliente com a escrita de apenas algumas linhas de código.  
  
 Esta seção descreve e demonstra como executar um pacote existente programaticamente e como acessar a saída do fluxo de dados de outros aplicativos. Como opção de programação avançada, você pode criar programaticamente um pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] linha por linha conforme descrito no tópico [Criar pacotes programaticamente](../building-packages-programmatically/building-packages-programmatically.md).  
  
 Esta seção também discute outras tarefas administrativas que você pode executar programaticamente para gerenciar pacotes armazenados, pacotes em execução e funções do pacote.  
  
## <a name="running-packages-on-the-integration-services-server"></a>Executando pacotes no servidor do Integration Services  
 Quando você implanta pacotes no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], pode executar os pacotes programaticamente usando o namespace <xref:Microsoft.SqlServer.Management.IntegrationServices>. O assembly Microsoft.SqlServer.Management.IntegrationServices é compilado com o .NET Framework 3.5. Se você estiver compilando um aplicativo do .NET Framework 4.0, terá que adicionar a referência de assembly diretamente no seu arquivo de projeto.  
  
 Você também pode usar o namespace para implantar e gerenciar projetos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Para obter uma visão geral do namespace e dos trechos de códigos, consulte a entrada do blog [Prévia do modelo do objeto gerenciado do catálogo do SSIS](http://go.microsoft.com/fwlink/?LinkId=253122)em blogs.msdn.com.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Compreender as diferenças entre execução local e remota](../run-manage-packages-programmatically/understanding-the-differences-between-local-and-remote-execution.md)  
 Discute diferenças críticas entre a execução de um pacote localmente ou no servidor.  
  
 [Carregar e executar um pacote local programaticamente](../run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)  
 Descreve como executar um pacote existente de um aplicativo cliente no computador local.  
  
 [Carregar e executar um pacote remoto programaticamente](../run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)  
 Descreve como executar um pacote existente de um aplicativo cliente e como garantir que o pacote seja executado no servidor.  
  
 [Carregar a saída de um pacote local](../run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
 Descreve como executar um pacote no computador local e carregar a saída do fluxo de dados em um aplicativo cliente, utilizando o destino DataReader e o namespace DtsClient.  
  
 [Enumerar pacotes disponíveis programaticamente](../run-manage-packages-programmatically/enumerating-available-packages-programmatically.md)  
 Descreve como descobrir pacotes disponíveis que são gerenciados pelo serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [Gerenciar pacotes e pastas programaticamente](../run-manage-packages-programmatically/managing-packages-and-folders-programmatically.md)  
 Descreve como criar, renomear e excluir pacotes e pastas.  
  
 [Gerenciar de pacotes em execução programaticamente](../run-manage-packages-programmatically/managing-running-packages-programmatically.md)  
 Descreve como listar pacotes que estão em execução atualmente, examinar suas propriedades e interromper um pacote em execução.  
  
 [Gerenciar funções de pacote programaticamente &#40;Serviço SSIS&#41;](../run-manage-packages-programmatically/managing-package-roles-programmatically-ssis-service.md)  
 Descreve como obter ou definir informações sobre as funções atribuídas a um pacote ou pasta.  
  
## <a name="reference"></a>Referência  
 [Referência de mensagens e erros do Integration Services](../integration-services-error-and-message-reference.md)  
 Lista os códigos de erro predefinidos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] com seus nomes simbólicos e descrições.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Estender pacotes com scripts](../extending-packages-scripting/extending-packages-with-scripting.md)  
 Discute como estender o fluxo de controle usando a tarefa Script, e como estender o fluxo de dados usando o componente Script.  
  
 [Estendendo pacotes com objetos personalizados](../extending-packages-custom-objects/extending-packages-with-custom-objects.md)  
 Discute como criar tarefas personalizadas de programa, componentes de fluxo de dados e outros objetos de pacote para uso em vários pacotes.  
  
 [Compilar Pacotes Programaticamente](../building-packages-programmatically/building-packages-programmatically.md)  
 Discute como criar, configurar e salvar pacotes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] programaticamente.  
  
![Ícone do Integration Services (pequeno)](../media/dts-16.gif "ícone do Integration Services (pequeno)")**mantenha-se para cima até o momento com o Integration Services  **<br /> Para os downloads mais recentes, artigos, exemplos e vídeos da [!INCLUDE[msCoName](../../includes/msconame-md.md)], bem como soluções selecionadas pela comunidade, visite o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] página no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Integration Services](../sql-server-integration-services.md)  
  
  
