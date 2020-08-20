---
description: CREATE QUEUE (Transact-SQL)
title: CREATE QUEUE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/25/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- QUEUE_TSQL
- CREATE QUEUE
- QUEUE
- CREATE_QUEUE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE QUEUE statement
- internal activation [Service Broker]
- stored procedure activation [Service Broker]
- message retention [Service Broker]
- unavailable queues [Service Broker]
- activation stored procedures [Service Broker]
- queues [Service Broker], creating
ms.assetid: fce80faf-2bdc-475d-8ca1-31438ed41fb0
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e472951762704fbb616dd10effe7d7920aef4efe
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88496851"
---
# <a name="create-queue-transact-sql"></a>CREATE QUEUE (Transact-SQL)

[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

Cria uma fila nova em um banco de dados. Enfileira mensagens de repositório. Quando uma mensagem chega para um serviço, o [!INCLUDE[ssSB](../../includes/sssb-md.md)] coloca a mensagem na fila associada ao serviço.

![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>Sintaxe

```syntaxsql
CREATE QUEUE <object>
   [ WITH
     [ STATUS = { ON | OFF } [ , ] ]
     [ RETENTION = { ON | OFF } [ , ] ]
     [ ACTIVATION (
         [ STATUS = { ON | OFF } , ]
           PROCEDURE_NAME = <procedure> ,
           MAX_QUEUE_READERS = max_readers ,
           EXECUTE AS { SELF | 'user_name' | OWNER }
            ) [ , ] ]
     [ POISON_MESSAGE_HANDLING (
         [ STATUS = { ON | OFF } ] ) ]
    ]
     [ ON { filegroup | [ DEFAULT ] } ]
[ ; ]

<object> ::=
{ database_name.schema_name.queue_name | schema_name.queue_name | queue_name }

<procedure> ::=
{ database_name.schema_name.stored_procedure_name | schema_name.stored_procedure_name | stored_procedure_name }

```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos

*database_name* (objeto) É o nome do banco de dados no qual criar a nova fila. *database_name* precisa especificar o nome de um banco de dados existente. Quando *database_name* não é fornecido, a fila é criada no banco de dados atual.

*schema_name* (objeto) É o nome do esquema ao qual a nova fila pertence. O esquema considera como padrão o esquema padrão para o usuário que executa a instrução. Se a instrução CREATE QUEUE for executada por um membro da função de servidor fixa sysadmin ou por um membro das funções de banco de dados fixas db_dbowner ou db_ddladmin no banco de dados especificado por *database_name*, *schema_name* poderá especificar um esquema diferente do que está associado ao logon da conexão atual. Caso contrário, o *schema_name* deverá ser o esquema padrão do usuário que executa a instrução.

*queue_name* É o nome da fila a ser criada. Esse nome deve satisfazer as diretrizes para identificadores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

STATUS (Fila) Especifica se a fila está disponível (ON) ou não disponível (OFF). Quando a fila estiver indisponível, nenhuma mensagem pode ser adicionada à fila ou removida dela. Você pode criar a fila em um estado indisponível para evitar que as mensagens cheguem à fila até que a fila seja tornada disponível com uma instrução ALTER QUEUE. Se esta cláusula for omitida, o padrão será ON e a fila estará disponível.

RETENTION Especifica a configuração de retenção para a fila. Se RETENTION = ON, todas as mensagens enviadas ou recebidas em conversas que usem essa fila serão retidas na fila até que as conversas tenham terminado. Isso lhe permite reter mensagens para propósitos de auditoria ou executar transações de compensação se um erro acontecer. Se essa cláusula não for especificada, a configuração de retenção considerará OFF como padrão.

> [!NOTE]
> Definindo RETENÇÃO = ON pode diminuir o desempenho. Essa configuração só deveria ser usada se for requerida para o aplicativo.

ACTIVATION Especifica informações sobre qual procedimento armazenado que você tem de começar a processar mensagens nesta fila.

STATUS (Ativação) Especifica se o [!INCLUDE[ssSB](../../includes/sssb-md.md)] inicia o procedimento armazenado. Quando o STATUS = ON, a fila começa o procedimento armazenado especificado com PROCEDURE_NAME quando o número de procedimentos atualmente sendo executados for menos que MAX_QUEUE_READERS e quando as mensagens chegarem à fila mais rápido do que os procedimentos armazenados recebam as mensagens. Quando o STATUS = OFF, a fila não inicia o procedimento armazenado. Se essa cláusula não for especificada, o padrão será ON.

PROCEDURE_NAME = \<procedure> Especifica o nome do procedimento armazenado para começar a processar as mensagens nessa fila. Esse valor deve ser um identificador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

*database_name*(procedimento) É o nome do banco de dados que contém o procedimento armazenado.

*schema_name*(procedimento) É o nome do esquema que contém o procedimento armazenado.

*procedure_name* É o nome do procedimento armazenado.

MAX_QUEUE_READERS =*max_readers* Especifica o número máximo de instâncias do procedimento armazenado de ativação que a fila inicia ao mesmo tempo. O valor de *max_readers* precisa ser um número entre **0** e **32767**.

EXECUTE AS Especifica a conta do usuário do banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sob a qual é executado o procedimento armazenado de ativação. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve poder verificar as permissões deste usuário no momento em que a fila inicia o procedimento armazenado. Para um usuário de domínio, o servidor deverá estar conectado ao domínio quando o procedimento armazenado for iniciado ou a ativação falhará. Para um usuário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o servidor sempre pode verificar as permissões.

SELF Especifica que o procedimento armazenado é executado como o usuário atual. (O principal do banco de dados que executa esta instrução CREATE QUEUE.)

'*user_name*' É o nome do usuário que o procedimento armazenado usa para ser executado. O parâmetro *user_name* deve ser um usuário [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] válido especificado como um identificador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O usuário atual precisa ter a permissão IMPERSONATE para o *user_name* especificado.

OWNER Especifica que o procedimento armazenado é executado como o proprietário da fila.

POISON_MESSAGE_HANDLING Especifica se a manipulação de mensagens suspeitas está habilitada para a fila. O padrão é ON.

A fila que tiver a manipulação de mensagens suspeitas definida como OFF, não será desabilitada após cinco reversões consecutivas de transações. Isso permite que um sistema personalizado de manipulação de mensagens suspeitas seja definido pelo aplicativo.

ON *filegroup |* [**DEFAULT**] Especifica o grupo de arquivos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no qual criar esta fila. Use o parâmetro *filegroup* para identificar um grupo de arquivos ou o identificador DEFAULT para usar o grupo de arquivos padrão para o banco de dados do Service Broker. No contexto desta cláusula, DEFAULT não é uma palavra-chave e deve ser delimitado como um identificador. Quando nenhum grupo de arquivos for especificado, a fila usará o grupo de arquivos padrão para o banco de dados.

## <a name="remarks"></a>Comentários

Uma fila pode ser o destino de uma instrução SELECT. Entretanto, os conteúdos de uma fila só podem ser modificados usando instruções que operam em conversas do [!INCLUDE[ssSB](../../includes/sssb-md.md)], tais como SEND, RECEIVE e END CONVERSATION. Uma fila não pode ser o destino de uma instrução INSERT, UPDATE, DELETE ou TRUNCATE.

Uma fila pode não ser um objeto temporário. Portanto, nomes de fila que começam com **#** não são válidos.

Criando uma fila em um estado inativo lhe permite ter a infraestrutura pronta para um serviço antes de permitir que as mensagens sejam recebidas na fila.

O [!INCLUDE[ssSB](../../includes/sssb-md.md)] não parará os procedimentos armazenados de ativação quando não houver nenhuma mensagem na fila. Um procedimento armazenado de ativação deveria sair quando nenhuma mensagem estiver disponível na fila por um período de tempo curto.

As permissões para um procedimento armazenado de ativação são verificadas quando o [!INCLUDE[ssSB](../../includes/sssb-md.md)] iniciar o procedimento armazenado, não quando a fila for criada. A instrução CREATE QUEUE não verifica que o usuário especificado na cláusula EXECUTE AS tem permissão para executar o procedimento armazenado especificado na cláusula PROCEDURE NAME.

Quando uma fila não está disponível, o [!INCLUDE[ssSB](../../includes/sssb-md.md)] mantém as mensagens para os serviços que usam a fila na transmissão para o banco de dados. A exibição do catálogo sys.transmission_queue fornece uma exibição da fila de transmissão.

Uma fila é um objeto possuído por esquema. As filas aparecem na exibição do catálogo sys.objects.

A tabela a seguir lista as colunas em uma fila.

|Nome da coluna|Tipo de dados|Descrição|
|-----------------|---------------|-----------------|
|status|**tinyint**|Status da mensagem. A instrução RECEIVE retorna todas as mensagens que têm um status igual a **1**. Se a retenção de mensagens estiver ativada, o status será definido como 0. Se a retenção de mensagens estiver desativada, a mensagem será excluída da fila. As mensagens na fila podem conter um dos seguintes valores:<br /><br /> **0** = Mensagem recebida retida<br /><br /> **1** = Pronta para receber<br /><br /> **2** = Ainda não concluída<br /><br /> **3** = Mensagem enviada retida|
|priority|**tinyint**|O nível de prioridade atribuído a essa mensagem.|
|queuing_order|**bigint**|Número da ordem da mensagem na fila.|
|conversation_group_id|**uniqueidentifier**|O identificador do grupo de conversa a que pertence essa mensagem.|
|conversation_handle|**uniqueidentifier**|Tratamento para a conversa da qual essa mensagem faz parte.|
|message_sequence_number|**bigint**|Número de sequência da mensagem na conversa.|
|service_name|**nvarchar(512)**|O nome do serviço a que se destina a conversa.|
|service_id|**int**|Identificador de objeto do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do serviço para o qual a conversa é destinada.|
|service_contract_name|**nvarchar(256)**|O nome do contrato que a conversa segue.|
|service_contract_id|**int**|Identificador de objeto do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do contrato que a conversa segue.|
|message_type_name|**nvarchar(256)**|O nome do tipo de mensagem a que descreve a mensagem.|
|message_type_id|**int**|Identificador de objeto do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do tipo de mensagem que descreve a mensagem.|
|validation|**nchar(2)**|Validação usada para a mensagem.<br /><br /> E = Vazio<br /><br /> N=None<br /><br /> X=XML|
|message_body|**varbinary(max)**|O conteúdo da mensagem.|
|message_id|**uniqueidentifier**|Identificador exclusivo para a mensagem.|

## <a name="permissions"></a>Permissões

A permissão para criar uma fila usa os membros das funções de banco de dados fixas `db_ddladmin` ou `db_owner`, ou a função de servidor fixa `sysadmin`.

A permissão `REFERENCES` para uma fila assume como padrão o proprietário da fila, os membros das funções de banco de dados fixas `db_ddladmin` ou `db_owner`, ou os membros da função de servidor fixa `sysadmin`.

A permissão `RECEIVE` para uma fila assume como padrão o proprietário da fila, os membros da função de banco de dados fixa `db_owner` ou os membros da função de servidor fixa `sysadmin`.

## <a name="examples"></a>Exemplos

### <a name="a-creating-a-queue-with-no-parameters"></a>a. Criando uma fila sem parâmetros

O exemplo seguinte cria uma fila que está disponível para receber mensagens. Nenhum procedimento armazenado de ativação é especificado para a fila.

```sql
CREATE QUEUE ExpenseQueue ;
```

### <a name="b-creating-an-unavailable-queue"></a>B. Criando uma fila indisponível

O exemplo seguinte cria uma fila que está indisponível para receber mensagens. Nenhum procedimento armazenado de ativação é especificado para a fila.

```sql
CREATE QUEUE ExpenseQueue WITH STATUS=OFF ;
```

### <a name="c-creating-a-queue-and-specify-internal-activation-information"></a>C. Criando uma fila e especificando informações de ativação internas

O exemplo seguinte cria uma fila que está disponível para receber mensagens. A fila inicia o procedimento armazenado `expense_procedure` quando uma mensagem entrar na fila. O procedimento armazenado executa como o usuário `ExpenseUser`. A fila inicia um máximo de `5` instâncias do procedimento armazenado.

```sql
CREATE QUEUE ExpenseQueue
    WITH STATUS=ON,
    ACTIVATION (
        PROCEDURE_NAME = expense_procedure
        , MAX_QUEUE_READERS = 5
        , EXECUTE AS 'ExpenseUser' ) ;
```

### <a name="d-creating-a-queue-on-a-specific-filegroup"></a>D. Criando uma fila em um grupo de arquivos específico

O exemplo a seguir cria uma fila no grupo de arquivos `ExpenseWorkFileGroup`.

```sql
CREATE QUEUE ExpenseQueue
    ON ExpenseWorkFileGroup ;
```

### <a name="e-creating-a-queue-with-multiple-parameters"></a>E. Criando uma fila com vários parâmetros

O exemplo a seguir cria uma fila no grupo de arquivos `DEFAULT`. A fila está indisponível. As mensagens são retidas na fila até que a conversa a que elas pertençam termine. Quando a fila for deixada disponível por ALTER QUEUE, a fila inicia o procedimento armazenado `2008R2.dbo.expense_procedure` para processar as mensagens. O procedimento armazenado executa como o usuário que executou a instrução `CREATE QUEUE`. A fila inicia um máximo de `10` instâncias do procedimento armazenado.

```sql
CREATE QUEUE ExpenseQueue
    WITH STATUS = OFF
      , RETENTION = ON
      , ACTIVATION (
          PROCEDURE_NAME = AdventureWorks2012.dbo.expense_procedure
          , MAX_QUEUE_READERS = 10
          , EXECUTE AS SELF )
    ON [DEFAULT];
```

## <a name="see-also"></a>Consulte Também

- [ALTER QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-queue-transact-sql.md)
- [CREATE SERVICE &#40;Transact-SQL&#41;](../../t-sql/statements/create-service-transact-sql.md)
- [DROP QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-queue-transact-sql.md)
- [RECEIVE &#40;Transact-SQL&#41;](../../t-sql/statements/receive-transact-sql.md)
- [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)
