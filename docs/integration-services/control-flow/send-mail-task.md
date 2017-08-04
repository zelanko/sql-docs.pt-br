---
title: Tarefa enviar email | Microsoft Docs
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
- sql13.dts.designer.sendmailtask.f1
helpviewer_keywords:
- mail [Integration Services]
- Send Mail task
- e-mail [Integration Services]
- messages [Integration Services]
- sending messages
ms.assetid: fe0b7cbc-fe8e-4fe2-95b4-2953efff5869
caps.latest.revision: 51
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c3e47e4a5ae297202ba43679fba393421880a7ea
ms.openlocfilehash: fd6f7a19c1b553ee06013a4a24fbbf26a759a6cd
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="send-mail-task"></a>Tarefa Enviar Email
  A tarefa Enviar Email envia uma mensagem de email. Usando a tarefa Enviar Email, um pacote pode enviar mensagens se as tarefas no fluxo de trabalho do pacote tiverem êxito ou falharem ou enviar mensagens em resposta a um evento que o pacote ativa em tempo de execução. Por exemplo, a tarefa pode notificar um administrador de banco de dados sobre o êxito ou a falha da tarefa Fazer Backup do Banco de Dados.  
  
 Você pode configurar a tarefa Enviar Email das seguintes formas:  
  
-   Fornecendo o texto da mensagem de email.  
  
-   Fornecendo uma linha de assunto para a mensagem de email.  
  
-   Definindo o nível de prioridade da mensagem. A tarefa dá suporte a três níveis de prioridade: normal, baixa e alta.  
  
-   Especificando os destinatários nas linhas Para, Cc e Cco. Se a tarefa especificar vários destinatários, eles serão separados por ponto-e-vírgulas.  
  
    > [!NOTE]  
    >  As linhas Para, Cc e Cco são limitadas a 256 caracteres cada, conforme os padrões da Internet.  
  
-   Incluindo anexos. Se a tarefa especificar vários anexos, eles serão separados pelo caractere barra vertical (|).  
  
    > [!NOTE]  
    >  Se um arquivo de anexo não existir quando o pacote for executado, ocorrerá um erro.  
  
-   Especificando o gerenciador de conexões SMTP a ser usado.  
  
    > [!IMPORTANT]  
    >  O gerenciador de conexões SMTP dá suporte apenas para autenticação anônima e Autenticação do Windows. Ele não suporta a autenticação básica.  
  
 O texto da mensagem pode ser uma cadeia de caracteres que você fornece, uma conexão com um arquivo que contém o texto ou o nome de uma variável que contém o texto. A tarefa usa um gerenciador de conexões de arquivos para se conectar a um arquivo. Para obter mais informações, consulte [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
 A tarefa usa um gerenciador de conexões SMTP para se conectar a um servidor de email. Para obter mais informações, consulte [SMTP Connection Manager](../../integration-services/connection-manager/smtp-connection-manager.md).  
  
## <a name="custom-logging-messages-available-on-the-send-mail-task"></a>Mensagens de log personalizadas disponíveis na tarefa Enviar Email  
 A tabela a seguir relaciona as entradas de log personalizadas para a tarefa Enviar Email. Para obter mais informações, consulte [Log do SSIS &#40;Integration Services&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
|Entrada de log|Description|  
|---------------|-----------------|  
|**SendMailTaskBegin**|Indica que a tarefa começou a enviar uma mensagem de email.|  
|**SendMailTaskEnd**|Indica que a tarefa terminou de enviar uma mensagem de email.|  
|**SendMailTaskInfo**|Fornece informações descritivas sobre a tarefa.|  
  
## <a name="configuring-the-send-mail-task"></a>Configurando a tarefa Enviar Email  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique em um dos tópicos a seguir:  
  
-   [Editor da Tarefa Enviar Email &#40;Página Geral&#41;](../../integration-services/control-flow/send-mail-task-editor-general-page.md)  
  
-   [Editor da Tarefa Enviar Email &#40;Página Email&#41;](../../integration-services/control-flow/send-mail-task-editor-mail-page.md)  
  
-   [Página Expressões](../../integration-services/expressions/expressions-page.md)  
  
 Para obter informações sobre como definir essas propriedades programaticamente, clique no tópico a seguir:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.SendMailTask.SendMailTask>  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
 Para obter informações sobre como definir essas propriedades no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , clique em [Definir as propriedades de uma tarefa ou de um contêiner](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b).  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   Artigo técnico sobre [Como enviar email com notificação de entrega em C#](http://go.microsoft.com/fwlink/?LinkId=237625)no site shareourideas.com  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas do Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Fluxo de Controle](../../integration-services/control-flow/control-flow.md)  
  
  
