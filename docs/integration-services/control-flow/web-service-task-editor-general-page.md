---
title: "Editor da tarefa serviço da Web (página geral) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.webservicestask.general.f1
helpviewer_keywords:
- Web Service Task Editor
ms.assetid: 4d7df283-430d-4f0f-9dd4-5909554cd5eb
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2c65419846e21225c6b5fe41bc07cfbae6dffe01
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="web-service-task-editor-general-page"></a>Editor da Tarefa Serviço da Web (página Geral)
  Use a página **Geral** da caixa de diálogo **Editor da Tarefa Serviços da Web** para especificar um gerenciador de conexões HTTP, o local do arquivo WSDL (linguagem WSDL) usado pela tarefa, descrever a tarefa Serviços da Web e baixar o arquivo WSDL.  
  
 Para obter mais informações sobre essa tarefa, consulte [Tarefa Serviço da Web](../../integration-services/control-flow/web-service-task.md).  
  
## <a name="options"></a>Opções  
 **HTTPConnection**  
 Selecione um Gerenciador de conexão na lista ou clique em \< **nova conexão...** > para criar uma nova conexão Gerenciador.  
  
> [!IMPORTANT]  
>  O gerenciador de conexões HTTP dá suporte apenas para autenticação anônima e autenticação básica. Ele não suporta a Autenticação do Windows.  
  
 **Tópicos relacionados:** [Gerenciador de Conexões de HTTP](../../integration-services/connection-manager/http-connection-manager.md), [Editor do Gerenciador de Conexões de HTTP &#40;página Servidor&#41;](../../integration-services/connection-manager/http-connection-manager-editor-server-page.md)  
  
 **WSDLFile**  
 Digite o caminho totalmente qualificado de um arquivo WSDL que é local para o computador ou clique no botão Procurar **(…)** e localize esse arquivo.  
  
 Se o arquivo WSDL já foi baixado manualmente no computador, selecione-o. No entanto, se o arquivo WSDL ainda não tiver sido baixado, siga estas etapas:  
  
-   Crie um arquivo vazio que tenha a extensão de nome de arquivo ".wsdl".  
  
-   Selecione esse arquivo vazio para a opção **Arquivo WSDL** .  
  
-   Defina o valor de **OverwriteWSDLFile** como **True** para permitir que o arquivo vazio seja substituído pelo arquivo WSDL real.  
  
-   Clique em **Baixar WSDL** para baixar o arquivo WSDL real e substituir o arquivo vazio.  
  
    > [!NOTE]  
    >  A opção **Baixar WSDL** não será habilitada até que você forneça o nome de um arquivo local existente na caixa **Arquivo WSDL** .  
  
 **OverwriteWSDLFile**  
 Indique se o arquivo WSDL da tarefa Serviço da Web pode ser substituído.  
  
 Para baixar o arquivo WSDL usando o botão **Baixar WSDL** , defina esse valor como **True**.  
  
 **Nome**  
 Forneça um nome exclusivo para a tarefa Serviço da Web. Esse nome é usado como rótulo no ícone de tarefa.  
  
> [!NOTE]  
>  Os nomes das tarefas devem ser exclusivos em um pacote.  
  
 **Description**  
 Digite uma descrição para a tarefa Serviço da Web.  
  
 **Baixar WSDL**  
 Faça o download do arquivo WSDL.  
  
 Esse botão não estará habilitado até que você forneça o nome de um arquivo local existente na caixa **Arquivo WSDL** .  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Web Editor da tarefa de serviço &#40; entrada página &#41;](../../integration-services/control-flow/web-service-task-editor-input-page.md)   
 [Editor da tarefa serviço da Web &#40; página de saída &#41;](../../integration-services/control-flow/web-service-task-editor-output-page.md)   
 [Página Expressões](../../integration-services/expressions/expressions-page.md)  
  
  
