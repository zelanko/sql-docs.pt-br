---
title: Editor do Gerenciador de Conexão SMTP | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.smtpconnection.f1
helpviewer_keywords:
- SMTP Connection Manager Editor
ms.assetid: 2693de0d-b04d-4325-a856-ce667d2b8aa1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 527c8f647c963c2c1c03171eeb154a790ab1994a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66055555"
---
# <a name="smtp-connection-manager-editor"></a>Editor do Gerenciador de Conexões SMTP
  Use a caixa de diálogo **Editor do Gerenciador de Conexões SMTP** para especificar um servidor SMTP.  
  
 Para saber mais sobre o Gerenciador de Conexões SMTP, consulte [SMTP Connection Manager](connection-manager/smtp-connection-manager.md).  
  
## <a name="options"></a>Opções  
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
>  Ao usar o Microsoft Exchange como servidor SMTP, talvez você precise definir **usar autenticação do Windows** para `True`. Os servidores do Exchange podem ser configurados para não permitir conexões SMTP não autenticadas.  
  
 **Habilitar SSL (Secure Sockets Layer)**  
 Selecione para criptografar a comunicação utilizando a SSL (Secure Sockets Layer) ao enviar mensagens de email.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  
