---
title: Trabalhando com notificações de consulta | Microsoft Docs
description: Trabalhando com notificações de consulta no driver de OLE DB para SQL Server
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], query notifications
- rowsets [SQL Server], notifications
- OLE DB Driver for SQL Server, query notifications
- notifications [OLE DB Driver for SQL Server]
- query notifications [SQL Server], OLE DB Driver for SQL Server
- canceling rowset changes
- IRowsetNotify interface
- MSOLEDBSQL, query notifications
- OLE DB Driver for SQL Server, query notifications
- consumer notification for rowset changes [OLE DB Driver for SQL Server]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 29aaab523b3a754c65b1b7a0312ceb5ea122f2d3
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419322"
---
# <a name="working-with-query-notifications"></a>Trabalhando com notificações de consulta

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

As notificações de consulta foram [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] introduzidas no driver e OLE DB para SQL Server. Baseadas na infraestrutura do SQL Service Broker, introduzida no SQL Server 2005 (9.x), as notificações de consulta permitem que os aplicativos sejam notificados em caso de alteração nos dados. Esse recurso é particularmente útil para aplicativos que fornecem um cache de informações de um banco de dados, como um aplicativo Web, e precisam ser notificados quando os dados de origem são alterados.

Usando notificações de consulta, você pode solicitar notificações dentro de um período de tempo limite especificado quando os dados subjacentes de uma consulta são alterados. A solicitação especifica as opções de notificação, que incluem o nome do serviço, o texto da mensagem e o valor do tempo limite do servidor. As notificações são entregues através de uma fila do Service Broker na qual os aplicativos podem sondar as notificações disponíveis.

A sintaxe da cadeia de caracteres das opções de notificação de consulta é:

`service=<service-name>[;(local database=<database> | broker instance=<broker instance>)]`

 Por exemplo:

`service=mySSBService;local database=mydb`

As assinaturas de notificação sobreviver Alémm o processo que as inicia. Isso ocorre porque um aplicativo pode criar uma assinatura de notificação e, em seguida, encerrar. A assinatura permanece válida e a notificação será feita se os dados forem alterados no tempo limite especificado na criação da assinatura. Uma notificação é identificada pela consulta executada, as opções de notificação e o texto da mensagem. Você pode cancelá-lo definindo seu valor de tempo limite como zero.

As notificações só são enviadas uma vez. Para ser notificado continuamente sobre alterações de dados, crie uma nova assinatura executando novamente a consulta depois que cada notificação for processada.

O driver de OLE DB para aplicativos SQL Server normalmente recebe notificações usando [!INCLUDE[tsql](../../../includes/tsql-md.md)] o comando [Receive](../../../t-sql/statements/receive-transact-sql.md) . Ele usa esse comando para ler notificações da fila associada ao serviço especificado nas opções de notificação.

> [!NOTE]
> Os nomes de tabela devem ser qualificados nas consultas para as quais a notificação é requerida. Por exemplo, `dbo.myTable`. Os nomes de tabela devem ser qualificados com nomes de duas partes. A assinatura é considerada inválida se nomes com três ou quatro partes são usados.

A infraestrutura de notificação baseia-se em um recurso de fila introduzido no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Em geral, as notificações geradas no servidor são enviadas através dessas filas para serem processadas posteriormente.

Para usar notificações de consulta, uma fila e um serviço devem existir no servidor. Eles podem ser criados usando o [!INCLUDE[tsql](../../../includes/tsql-md.md)] comando, semelhante ao seguinte:

```sql
CREATE QUEUE myQueue
CREATE SERVICE myService ON QUEUE myQueue
([https://schemas.microsoft.com/SQL/Notifications/PostQueryNotification])
```

> [!NOTE]
> O serviço deve usar o contrato predefinido, como mostrado acima.

## <a name="ole-db-driver-for-sql-server"></a>OLE DB Driver for SQL Server

O driver OLE DB para SQL Server dá suporte a notificações de consumidor na modificação do conjunto de linhas. O consumidor recebe uma notificação em cada fase da modificação do conjunto de linhas e em qualquer tentativa de alteração.

> [!NOTE]
> Passar uma consulta de notificação ao servidor com **ICommand::Execute** é a única maneira válida de assinar notificações de consulta com o OLE DB Driver for SQL Server.

### <a name="dbpropsetsqlserverrowset-property-set"></a>Conjunto de propriedades DBPROPSET_SQLSERVERROWSET

Para dar suporte a notificações de consulta por meio do OLE DB, o Driver do OLE DB para SQL Server adiciona as novas propriedades a seguir ao conjunto de propriedades `DBPROPSET_SQLSERVERROWSET`.

|Nome|Tipo|Descrição|
|----------|----------|-----------------|
|SSPROP_QP_NOTIFICATION_TIMEOUT|VT_UI4|O número de segundos que a notificação de consulta permanece ativa.<br /><br /> O padrão é 432.000 segundos (5 dias). O valor mínimo é 1 segundo e o valor máximo é 2^31-1 segundos.|
|SSPROP_QP_NOTIFICATION_MSGTEXT|VT_BSTR|O texto da mensagem da notificação. Esse texto é definido pelo usuário e não tem um formato predefinido.<br /><br /> Por padrão, a cadeia de caracteres fica vazia. Especifique uma mensagem usando de 1 a 2000 caracteres.|
|SSPROP_QP_NOTIFICATION_OPTIONS|VT_BSTR|As opções de notificação de consulta. Elas são especificadas em uma cadeia de caracteres com a sintaxe *name*=*value*. O usuário é responsável por criar o serviço e ler as notificações da fila.<br /><br /> O padrão é uma cadeia de caracteres vazia.|

A assinatura de notificação sempre é confirmada. Isso ocorre independentemente de a instrução ser executada em uma transação de usuário ou em confirmação automática ou se a transação na qual a instrução foi executada ou revertida. A notificação do servidor é acionada mediante uma das seguintes condições inválidas de notificação: alteração dos dados subjacentes ou do esquema ou quando o tempo limite expira; a que ocorrer primeiro. 

Os registros de notificação são excluídos assim que são disparados. Portanto, em caso de recebimento de notificações, o aplicativo deve realizar uma nova assinatura se você quiser obter mais atualizações.

Outra conexão ou thread pode verificar se há notificações na fila de destino. Por exemplo:

```sql
WAITFOR (RECEIVE * FROM MyQueue); -- Where MyQueue is the queue name.
```

> [!NOTE]
> `SELECT *`não exclui a entrada da fila. No entanto, `RECEIVE * FROM` o faz. Isso irá interromper um thread de servidor se a fila estiver vazia. Se houver entradas de fila no momento da chamada, elas serão retornadas imediatamente. Caso contrário, a chamada aguardará até que uma entrada de fila seja feita.

```sql
RECEIVE * FROM MyQueue
```

Essa instrução retornará imediatamente um conjunto de resultados vazio se a fila estiver vazia. Caso contrário, ele retorna todas as notificações de fila.

Se `SSPROP_QP_NOTIFICATION_MSGTEXT` e`SSPROP_QP_NOTIFICATION_OPTIONS` não forem nulos e não vazios, o cabeçalho TDS de notificações de consulta que contém as três propriedades definidas acima será enviado ao servidor. Isso ocorre após cada execução do comando. Se qualquer um deles for nulo (ou vazio), o cabeçalho não será enviado `DB_E_ERRORSOCCURRED` e gerado (ou `DB_S_ERRORSOCCURRED` será gerado, se as propriedades estiverem marcadas como opcionais). Em seguida, o valor de status `DBPROPSTATUS_BADVALUE`é definido como. A validação ocorrerá após execute e prepare. De modo semelhante, `DB_S_ERRORSOCCURED` será acionado quando as propriedades de notificação da consulta forem definidas para conexões com versões do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. O valor de status, nesse caso `DBPROPSTATUS_NOTSUPPORTED`, é.

Iniciar uma assinatura não garante que as mensagens seguintes sejam entregues com êxito. Além disso, nenhuma verificação é feita em relação à validade do nome de serviço especificado.

> [!NOTE]
> As instruções de preparação nunca farão com que a assinatura seja iniciada. A execução da instrução somente atingirá o início. As notificações de consulta não são afetadas pelo uso de serviços de OLE DB Core.

Para obter mais informações sobre `DBPROPSET_SQLSERVERROWSET` o conjunto de propriedades, consulte [Propriedades e comportamentos de conjunto de linhas](../../oledb/ole-db-rowsets/rowset-properties-and-behaviors.md).

## <a name="see-also"></a>Confira também

[Recursos do Driver do OLE DB para SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)
