---
description: 'Database Mail: Email na fila, não entregue'
title: 'Database Mail: Email na fila, não entregue | Microsoft Docs'
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
ms.openlocfilehash: 8e70b32c2cee28acf4b886f0bf738f4ed8857619
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96128801"
---
# <a name="database-mail-mail-queued-not-delivered"></a>Database Mail: Email na fila, não entregue 
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

Este tópico descreve como solucionar o problema de mensagens de email enfileiradas com êxito, mas não entregues.

## <a name="diagnose-the-problem"></a>Diagnosticar o problema 

O programa externo do Database Mail registra em log a atividade de email no banco de dados **msdb**.

Primeiro, para confirmar que o Database Mail está habilitado, use a [Opção do Database Mail XPs](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md) do procedimento armazenado do sistema **sp_configure**, como no exemplo a seguir:

```sql 
EXEC sp_configure 'show advanced', 1;  
RECONFIGURE; 
EXEC sp_configure; 
GO
```

Em seguida, execute a seguinte instrução no banco de dados **msdb** para verificar o status da fila de emails:

```sql
sysmail_help_queue_sp @queue_type = 'Mail' ;
```

Para obter uma explicação detalhada das colunas, veja [sysmail_help_queue_sp (Transact-SQL)](../system-stored-procedures/sysmail-help-queue-sp-transact-sql.md#result-set).

Verifique a exibição **sysmail_event_log** para observar a atividade. A exibição deve conter uma entrada declarando que o programa externo do Database Mail foi iniciado. Se não houver nenhuma entrada na exibição **sysmail_event_log**, confira o sintoma [Mensagens na Fila, Nenhuma Entrada](database-mail-common-errors.md#database-mail-queued-no-entries-in-sysmail_event_log-or-windows-application-event-log) em **sysmail_event_log**. Se houver erros na exibição **sysmail_event_log**, solucione problemas do erro específico.

Se houver entradas na exibição **sysmail_event_log**, verifique a exibição **sysmail_allitems** quanto ao status das mensagens.

## <a name="message-status-unsent"></a>Status de mensagem não enviada 

O status de **não enviada** indica que o programa externo do [Database Mail](database-mail-external-program.md) ainda não processou a mensagem de email. O programa externo do Database Mail pode ter se atrasado no processamento das mensagens; a taxa com a qual o programa externo processa mensagens depende das condições da rede, do tempo limite de novas tentativas, do volume de mensagens e da capacidade do servidor SMTP. Se o problema persistir, considere usar mais de um perfil para distribuir mensagens entre mais de um servidor SMTP.

Verifique a data de modificação mais recente das mensagens entregues com êxito. Se a última entrega com êxito tiver ocorrido já há algum tempo, examine a exibição sysmail_event_log para verificar se o programa externo foi iniciado com êxito pelo Service Broker. Se a última tentativa não tiver iniciado o programa externo, verifique se o Programa Externo do Database Mail está localizado no diretório correto e se a conta de serviço do SQL Server tem permissão para executar o executável.

   > [!NOTE]
   > Para excluir mensagens antigas não enviadas, aguarde até que as mensagens não entregáveis sejam as mais antigas na fila e use [sysmail_delete_mailitems_sp](../system-stored-procedures/sysmail-delete-mailitems-sp-transact-sql.md) para excluí-las.

## <a name="message-status-retrying"></a>Status da mensagem tentando novamente

O status de tentando novamente indica que o Database Mail tentou entregar a mensagem ao servidor SMTP, mas não teve êxito. Normalmente, isso é causado por uma interrupção da rede, uma falha do servidor SMTP ou uma conta incorretamente configurada do Database Mail. A mensagem dever ter êxito ou falha e postar uma mensagem no log de eventos.

## <a name="message-status-sent"></a>Status de mensagem enviada

O status de **enviada** indica que o programa externo do Database Mail teve êxito na entrega da mensagem de email ao servidor SMTP. Se a mensagem não chegar ao seu destino, é porque o servidor SMTP a aceitou do Database Mail, mas não a entregou ao destinatário final. Verifique os logs do servidor SMTP ou contate o administrador do mesmo. Você também pode testar o servidor de email SMTP usando outro cliente, como o Outlook Express.

## <a name="message-status-failed"></a>Status de mensagem de falha

O status de falha indica que o programa externo do Database Mail não pôde entregar a mensagem ao servidor SMTP. Neste caso, a exibição **sysmail_event_log** conterá as informações detalhadas do programa externo. Para uma consulta de exemplo que une **sysmail_faileditems** e **sysmail_event_log** para recuperar mensagens de erro detalhadas, veja [Verificar o status de mensagens de email enviadas com o Database Mail](check-the-status-of-e-mail-messages-sent-with-database-mail.md). As causas mais comuns de falha são endereço de destino incorreto ou problemas de rede que impedem o programa externo de acessar uma ou mais contas de failover. Problemas no servidor SMTP também podem fazê-lo rejeitar emails. Usando o Assistente para Configuração do Database Mail, altere o **Nível de Registros em Log** para **Detalhado** e envie um email de teste para investigar o ponto de falha.



##  <a name="see-also"></a><a name="RelatedContent"></a> Confira também
  
-  [Visão geral do Database Mail](database-mail.md)

  
  
