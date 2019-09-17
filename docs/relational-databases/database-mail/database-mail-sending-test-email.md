---
title: Enviar um email de teste com o Database Mail | Microsoft Docs
ms.custom: ''
ms.date: 04/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- architecture [SQL Server], Database Mail
- Database Mail [SQL Server], architecture
- Database Mail [SQL Server], components
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d8412a87703577595f0408de3b9cf26520160fdf
ms.sourcegitcommit: 2da98f924ef34516f6ebf382aeb93dab9fee26c1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/03/2019
ms.locfileid: "70228457"
---
# <a name="send-a-test-email-with-database-mail"></a>Enviar um email de teste com o Database Mail  
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

Use a caixa de diálogo Enviar Email de Teste para testar a possibilidade de enviar emails usando um perfil específico.

## <a name="permissions"></a>Permissões

Você deve ser membro da função de servidor fixa sysadmin para usar a caixa de diálogo Enviar Email de Teste. Usuários que não sejam membros da função de servidor fixa sysadmin podem testar o Database Mail usando o procedimento [sp_send_dbmail](../system-stored-procedures/sp-send-dbmail-transact-sql.md).

## <a name="procedure"></a>Procedimento

1. Usando o Pesquisador de Objetos no [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md), conecte-se a uma instância do Mecanismo de Banco de Dados do SQL Server em que o Database Mail está configurado, expanda Gerenciamento, clique com o botão direito do mouse em Database Mail e, em seguida, selecione Enviar Email de Teste. Se não existir nenhum perfil de Database Mail, uma caixa de diálogo solicitará que o usuário crie um perfil e abra o Assistente para Configuração do Database Mail.
1. Na caixa de diálogo **Enviar Email de Teste** de <instance name>, na caixa Perfil do Database Mail, selecione o perfil que deseja testar.
1. Na caixa **Para**, digite o nome do email do destinatário do email de teste.
1. Na caixa **Assunto**, digite a linha do assunto do email de teste. Altere o assunto padrão para identificar melhor seu email para a solução de problemas.
1. Na caixa **Corpo**, digite a corpo da mensagem do email de teste. Altere o assunto padrão para identificar melhor seu email para a solução de problemas.
1. Selecione **Enviar Email de Teste** para enviar o email de teste à fila do Database Mail.
1. O envio do email de teste faz com que se abra a caixa de diálogo Email de Teste do Database Mail. Anote o número exibido na caixa Email enviado. Trata-se da mailitem_id da mensagem de teste. Selecione OK.
1. Na Barra de Ferramentas, selecione Nova Consulta para abrir a janela do Editor de Consultas. Execute a seguinte instrução T-SQL para determinar o status da mensagem de email de teste:

    ```sql
    SELECT * FROM msdb.dbo.sysmail_allitems 
    WHERE mailitem_id = <the mailitem_id from the previous step> ;
    ```

    A coluna sent_status indica se a mensagem de email de teste foi enviada.

1. Se ocorrerem erros, execute a seguinte instrução para exibir a mensagem de erro:

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

    ```sql
    SELECT * FROM msdb.dbo.sysmail_event_log 
    WHERE mailitem_id = <the mailitem_id from the previous step> ;
    ```


##  <a name="RelatedContent"></a> Confira também 
  
-   [Objetos de configuração do Database Mail](../../relational-databases/database-mail/database-mail-configuration-objects.md)
-   [Objetos do sistema de mensagens do Database Mail](../../relational-databases/database-mail/database-mail-messaging-objects.md)
-   [Programa externo do Database Mail](../../relational-databases/database-mail/database-mail-external-program.md)
-   [Log e auditoria do Database Mail](../../relational-databases/database-mail/database-mail-log-and-audits.md)
-   [Configurar o SQL Server Agent Mail para usar o Database Mail](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)
  
  
