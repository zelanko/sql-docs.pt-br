---
title: Tarefa Enviar Email | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sendmailtask.f1
- sql13.dts.designer.sendmailtask.general.f1
- sql13.dts.designer.sendmailtask.mail.f1
helpviewer_keywords:
- mail [Integration Services]
- Send Mail task
- e-mail [Integration Services]
- messages [Integration Services]
- sending messages
ms.assetid: fe0b7cbc-fe8e-4fe2-95b4-2953efff5869
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2504bc45e358ebbf35b279e07be511f7a6041956
ms.sourcegitcommit: 0638b228980998de9056b177c83ed14494b9ad74
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/14/2018
ms.locfileid: "51641283"
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
  
|Entrada de log|Descrição|  
|---------------|-----------------|  
|**SendMailTaskBegin**|Indica que a tarefa começou a enviar uma mensagem de email.|  
|**SendMailTaskEnd**|Indica que a tarefa terminou de enviar uma mensagem de email.|  
|**SendMailTaskInfo**|Fornece informações descritivas sobre a tarefa.|  
  
## <a name="configuring-the-send-mail-task"></a>Configurando a tarefa Enviar Email  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Página Expressões](../../integration-services/expressions/expressions-page.md)  
  
 Para obter informações sobre como definir essas propriedades programaticamente, clique no tópico a seguir:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.SendMailTask.SendMailTask>  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter informações sobre como definir essas propriedades no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , clique em [Definir as propriedades de uma tarefa ou de um contêiner](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b).  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   Artigo técnico sobre [Como enviar email com notificação de entrega em C#](https://go.microsoft.com/fwlink/?LinkId=237625)no site shareourideas.com  
  
## <a name="send-mail-task-editor-general-page"></a>Editor da Tarefa Enviar Email (página Geral)
  Use a página **Geral** da caixa de diálogo **Editor da Tarefa Enviar Email** para nomear e descrever a tarefa Enviar Email.  
  
### <a name="options"></a>Opções  
 **Nome**  
 Forneça um nome exclusivo para a tarefa Enviar Email. Esse nome é usado como rótulo no ícone de tarefa.  
  
 **Nota** Nomes de tarefa devem ser exclusivos no pacote.  
  
 **Descrição**  
 Digite uma descrição para a tarefa Enviar Email.  
  
## <a name="send-mail-task-editor-mail-page"></a>Editor da tarefa Enviar Email (página Email)
  Use a página **Email** da caixa de diálogo do **Editor da Tarefa Enviar Email** para especificar destinatários, o tipo de mensagem e a prioridade de uma mensagem. Você também pode anexar arquivos à mensagem. O texto da mensagem pode ser uma cadeia de caracteres fornecida por você, uma conexão com um arquivo que contém o texto ou o nome de uma variável que contém o texto.  
  
### <a name="options"></a>Opções  
 **SMTPConnection**  
 Selecione um gerenciador de conexões SMTP na lista ou clique em **\<Nova conexão…>** para criar um novo gerenciador de conexões.  
  
> [!IMPORTANT]  
>  O gerenciador de conexões SMTP dá suporte apenas para autenticação anônima e Autenticação do Windows. Ele não suporta a autenticação básica.  
  
 **Tópicos relacionados:** [Gerenciador de conexões SMTP](../../integration-services/connection-manager/smtp-connection-manager.md)  
  
 **De**  
 Especifique o endereço de email do remetente.  
  
 **Para**  
 Forneça os endereços de email dos destinatários, separados por ponto-e-vírgula.  
  
 **Cc**  
 Especifique os endereços de email de outras pessoas que também receberão cópias da mensagem, separando todos os emails por ponto-e-vírgula.  
  
 **Cco**  
 Especifique os endereços de email de outras pessoas que também receberão cópias da mensagem com cópia oculta (Cco), separando todos os emails por ponto-e-vírgula.  
  
 **Assunto**  
 Indique o assunto da mensagem de email.  
  
 **MessageSourceType**  
 Selecione o tipo de origem da mensagem. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Entrada Direta**|Defina a origem do texto da mensagem. Selecionar este valor faz com que seja exibida a opção dinâmica **MessageSource**.|  
|**Conexão do Arquivo**|Defina a origem do arquivo que contém o texto da mensagem. Selecionar este valor faz com que seja exibida a opção dinâmica **MessageSource**.|  
|**Variável**|Defina a origem de uma variável que contém o texto da mensagem. Selecionar este valor faz com que seja exibida a opção dinâmica **MessageSource**.|  
  
 **Prioridade**  
 Defina a prioridade da mensagem.  
  
 **Anexos**  
 Forneça os nomes de arquivo dos anexos à mensagem de email, separados por uma barra vertical (|).  
  
> [!NOTE]  
>  As linhas Para, Cc e Cco são limitadas a 256 caracteres, de acordo com os padrões da Internet.  
  
### <a name="messagesourcetype-dynamic-options"></a>Opções dinâmicas de MessageSourceType  
  
#### <a name="messagesourcetype--direct-input"></a>MessageSourceType = Entrada direta  
 **MessageSource**  
 Digite o texto da mensagem ou clique no botão Procurar (...) e digite a mensagem na caixa de diálogo **Origem da mensagem** .  
  
#### <a name="messagesourcetype--file-connection"></a>MessageSourceType = Conexão do arquivo  
 **MessageSource**  
 Selecione um gerenciador de conexões de arquivos na lista ou clique em \<**Nova conexão…**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
#### <a name="messagesourcetype--variable"></a>MessageSourceType = Variável  
 **MessageSource**  
 Selecione uma variável na lista ou clique em \<**Nova variável...**> para criar uma nova variável.  
  
 **Tópicos relacionados:** [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefas do Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Fluxo de Controle](../../integration-services/control-flow/control-flow.md)  
  
  
