---
title: Executar e gerenciar pacotes programaticamente | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
ms.assetid: 1a08c75e-ce8c-45ee-81bd-32248bbdb2b2
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 88e5780ffb31d3f917245e423e8d88ad4033e3e9
ms.sourcegitcommit: 0638b228980998de9056b177c83ed14494b9ad74
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/14/2018
ms.locfileid: "51638303"
---
# <a name="running-and-managing-packages-programmatically"></a>Executando e gerenciando pacotes programaticamente
  Se precisar gerenciar e executar pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fora do ambiente de desenvolvimento, você poderá manipular pacotes programaticamente. Nesta abordagem, você tem uma série de opções:  
  
-   Carregar e executar um pacote existente sem modificação.  
  
-   Carregar um pacote existente, reconfigurá-lo (por exemplo, para outra fonte de dados) e executá-lo.  
  
-   Criar um pacote novo, adicionar e configurar os componentes, objeto por objeto e propriedade por propriedade, salvá-lo e executá-lo.  
  
 Você pode carregar e executar um pacote existente de um aplicativo cliente com a escrita de apenas algumas linhas de código.  
  
 Esta seção descreve e demonstra como executar um pacote existente programaticamente e como acessar a saída do fluxo de dados de outros aplicativos. Como opção de programação avançada, você pode criar programaticamente um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] linha por linha conforme descrito no tópico [Building Packages Programmatically](../../integration-services/building-packages-programmatically/building-packages-programmatically.md).  
  
 Esta seção também discute outras tarefas administrativas que você pode executar programaticamente para gerenciar pacotes armazenados, pacotes em execução e funções do pacote.  
  
## <a name="running-packages-on-the-integration-services-server"></a>Executando pacotes no servidor do Integration Services  
 Quando você implanta pacotes no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], pode executar os pacotes programaticamente usando o namespace <xref:Microsoft.SqlServer.Management.IntegrationServices>. O assembly Microsoft.SqlServer.Management.IntegrationServices é compilado com o .NET Framework 3.5. Se você estiver compilando um aplicativo do .NET Framework 4.0, terá que adicionar a referência de assembly diretamente no seu arquivo de projeto.  
  
 Você também pode usar o namespace para implantar e gerenciar projetos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para obter uma visão geral do namespace e dos snippets de códigos, consulte a entrada do blog [Prévia do modelo do objeto gerenciado do catálogo do SSIS](https://go.microsoft.com/fwlink/?LinkId=253122)em blogs.msdn.com.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Compreender as diferenças entre execução local e remota](../../integration-services/run-manage-packages-programmatically/understanding-the-differences-between-local-and-remote-execution.md)  
 Discute diferenças críticas entre a execução de um pacote localmente ou no servidor.  
  
 [Carregar e executar um pacote local programaticamente](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)  
 Descreve como executar um pacote existente de um aplicativo cliente no computador local.  
  
 [Carregar e executar um pacote remoto programaticamente](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)  
 Descreve como executar um pacote existente de um aplicativo cliente e como garantir que o pacote seja executado no servidor.  
  
 [Carregar a saída de um pacote local](../../integration-services/run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
 Descreve como executar um pacote no computador local e carregar a saída do fluxo de dados em um aplicativo cliente, utilizando o destino DataReader e o namespace DtsClient.  
  
 [Enumerar pacotes disponíveis programaticamente](../../integration-services/run-manage-packages-programmatically/enumerating-available-packages-programmatically.md)  
 Descreve como descobrir pacotes disponíveis que são gerenciados pelo serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 [Gerenciar pacotes e pastas programaticamente](../../integration-services/run-manage-packages-programmatically/managing-packages-and-folders-programmatically.md)  
 Descreve como criar, renomear e excluir pacotes e pastas.  
  
 [Gerenciar de pacotes em execução programaticamente](../../integration-services/run-manage-packages-programmatically/managing-running-packages-programmatically.md)  
 Descreve como listar pacotes que estão em execução atualmente, examinar suas propriedades e interromper um pacote em execução.  
  
 [Gerenciar funções de pacote programaticamente &#40;Serviço SSIS&#41;](../../integration-services/run-manage-packages-programmatically/managing-package-roles-programmatically-ssis-service.md)  
 Descreve como obter ou definir informações sobre as funções atribuídas a um pacote ou pasta.  
  
## <a name="reference"></a>Referência  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)  
 Lista os códigos de erro predefinidos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] com seus nomes simbólicos e descrições.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Estender pacotes com scripts](../../integration-services/extending-packages-scripting/extending-packages-with-scripting.md)  
 Discute como estender o fluxo de controle usando a tarefa Script, e como estender o fluxo de dados usando o componente Script.  
  
 [Estendendo pacotes com objetos personalizados](../../integration-services/extending-packages-custom-objects/extending-packages-with-custom-objects.md)  
 Discute como criar tarefas personalizadas de programa, componentes de fluxo de dados e outros objetos de pacote para uso em vários pacotes.  
  
 [Compilar Pacotes Programaticamente](../../integration-services/building-packages-programmatically/building-packages-programmatically.md)  
 Discute como criar, configurar e salvar pacotes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] programaticamente.  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)  
  
  
