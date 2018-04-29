---
title: Gerenciador de conexões SMTP | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: connection-manager
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.designer.smtpconnection.f1
helpviewer_keywords:
- connections [Integration Services], SMTP
- SMTP connection manager [Integration Services]
- connection managers [Integration Services], SMTP
ms.assetid: 3795d442-714b-4bbb-9acd-75bf277a468a
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ec3b8528955446f54f870fb134006cf0b5cdd86c
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="smtp-connection-manager"></a>Gerenciador de conexões SMTP
  Um gerenciador de conexões SMTP permite que um pacote conecte-se a um servidor SMTP. A tarefa Enviar Email incluída pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa um gerenciador de conexões SMTP.  
  
 Ao utilizar o Microsoft Exchange como servidor SMTP, você talvez precise configurar o gerenciador de conexões SMTP para utilizar a Autenticação do Windows. Os servidores Exchange podem ser configurados para não permitir conexões SMTP não autenticadas.  
  
## <a name="configuration-the-smtp-connection-manager"></a>Configuração do gerenciador de conexões SMTP  
 Quando você adiciona um gerenciador de conexões SMTP a um pacote, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria um gerenciador de conexões que será resolvido para uma conexão SMTP em tempo de execução, define as propriedades do gerenciador de conexões e adiciona o gerenciador de conexões à coleção **Connections** no pacote. A propriedade **ConnectionManagerType** do gerenciador de conexões está definida como **SMTP**.  
  
 Você pode configurar um gerenciador de conexões SMTP das seguintes maneiras:  
  
-   Fornecendo uma sequência de conexão.  
  
-   Especificando o nome de um servidor SMTP.  
  
-   Especificando o método de autenticação a ser usado.  
  
    > [!IMPORTANT]  
    >  O gerenciador de conexões SMTP dá suporte apenas para autenticação anônima e Autenticação do Windows. Ele não suporta a autenticação básica.  
  
-   Especificando se é necessário criptografar a comunicação utilizando o SSL ao enviar mensagens de email.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , consulte [Editor do Gerenciador de Conexões de SMTP](../../integration-services/connection-manager/smtp-connection-manager-editor.md).  
  
 Para obter informações sobre como configurar um gerenciador de conexões programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Adicionando conexões programaticamente](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="smtp-connection-manager-editor"></a>Editor do Gerenciador de Conexões SMTP
  Use a caixa de diálogo **Editor do Gerenciador de Conexões SMTP** para especificar um servidor SMTP.  
  
 Para saber mais sobre o Gerenciador de Conexões SMTP, consulte [SMTP Connection Manager](../../integration-services/connection-manager/smtp-connection-manager.md).  
  
### <a name="options"></a>Opções  
 **Nome**  
 Forneça um nome exclusivo para o gerenciador de conexões.  
  
 **Descrição**  
 Descreva o gerenciador de conexões. Como prática recomendável, descreva o gerenciador de conexões em termos de objetivo, para tornar os pacotes autodocumentados e mais fáceis de manter.  
  
 **Servidor SMTP**  
 Forneça o nome do servidor SMTP.  
  
 **Usar Autenticação do Windows**  
 Selecione para enviar email usando um servidor SMTP que usa a Autenticação do Windows para autenticar o acesso ao servidor.  
  
> [!IMPORTANT]  
>  O gerenciador de conexões SMTP dá suporte apenas para autenticação anônima e Autenticação do Windows. Ele não suporta a autenticação básica.  
  
> [!NOTE]  
>  Ao utilizar o Microsoft Exchange como servidor SMTP, talvez seja preciso definir **Usar Autenticação do Windows** como **True**. Os servidores do Exchange podem ser configurados para não permitir conexões SMTP não autenticadas.  
  
 **Habilitar SSL (Secure Sockets Layer)**  
 Selecione para criptografar a comunicação utilizando a SSL (Secure Sockets Layer) ao enviar mensagens de email.  
  
