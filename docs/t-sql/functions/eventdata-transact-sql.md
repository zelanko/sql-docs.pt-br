---
title: EVENTDATA (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- EVENTDATA
- fn_event_data
- EVENTDATA_TSQL
- fn_event_data_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- server instance event data [SQL Server]
- event notifications [SQL Server], event status
- events [SQL Server], status information
- EVENTDATA function
- status information [SQL Server], events
- DDL triggers, returning event data
ms.assetid: 03a80e63-6f37-4b49-bf13-dc35cfe46c44
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0ec1c2d952c334b1ccb394f5abb36ea91d5f1a87
ms.sourcegitcommit: 467b2c708651a3a2be2c45e36d0006a5bbe87b79
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53979842"
---
# <a name="eventdata-transact-sql"></a>EVENTDATA (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Essa função retorna informações sobre eventos do servidor ou do banco de dados. Quando uma notificação de evento é acionada e o agente de serviços especificado recebe os resultados, `EVENTDATA` é chamado. Um gatilho de logon ou DDL também dá suporte ao uso interno de `EVENTDATA`.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
EVENTDATA( )  
```  
  
## <a name="remarks"></a>Remarks  
`EVENTDATA` só retorna dados quando referenciado diretamente dentro de um gatilho DDL ou de logon. O `EVENTDATA` retorna null se outras rotinas o chamam, mesmo se um gatilho DDL ou logon chama essas rotinas.
  
Is dados retornados pelo `EVENTDATA` são inválidos após uma transação que

+ chamou `EVENTDATA` explicitamente
+ chamou `EVENTDATA` implicitamente
+ confirmações
+ é revertido  
  
> [!CAUTION]  
>  `EVENTDATA` retorna dados XML, enviados ao cliente como Unicode, que usam dois bytes para cada caractere. O `EVENTDATA` retorna o XML que pode representar esses pontos de código Unicode:  
>   
>  `0x0009`  
>   
>  `0x000A`  
>   
>  `0x000D`  
>   
>  `>= 0x0020 && <= 0xD7FF`  
>   
>  `>= 0xE000 && <= 0xFFFD`  
>   
>  O XML não pode expressar e não permitirá alguns caracteres que podem aparecer em identificadores [!INCLUDE[tsql](../../includes/tsql-md.md)] e dados. Os caracteres ou os dados que tenham pontos de código não mostrados na lista anterior serão mapeados para um ponto de interrogação (?).  
  
As senhas não são exibidos quando as instruções `CREATE LOGIN` ou `ALTER LOGIN` são executadas. Isso protege a segurança de logon.  
  
## <a name="schemas-returned"></a>Esquemas retornados  
EVENTDATA retorna um valor do tipo de dados **xml**. Por padrão, a definição de esquema para todos os eventos é instalada neste diretório: [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]Tools\Binn\schemas\sqlserver\2006\11\events\events.xsd.  
  
A página da Web [Esquemas XML do Microsoft SQL Server](https://go.microsoft.com/fwlink/?LinkID=31850) também tem o esquema de eventos.  
  
Para extrair o esquema de qualquer evento específico, pesquise o esquema pelo Tipo Complexo `EVENT_INSTANCE_<event_type>`. Por exemplo, para extrair o esquema do evento `DROP_TABLE`, pesquise o esquema por `EVENT_INSTANCE_DROP_TABLE`.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-querying-event-data-in-a-ddl-trigger"></a>A. Consultando dados de evento em um gatilho DDL  
Este exemplo cria um gatilho DDL que impede a criação de novas tabelas de banco de dados. O uso de XQuery em relação aos dados XML gerados por `EVENTDATA` captura a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] que aciona o gatilho. Confira [Referência da linguagem XQuery &#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md) para obter mais informações.  
  
> [!NOTE]  
>  Ao usar **Resultados em Grade** em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para consultar o elemento `<TSQLCommand>`, quebras de linha no texto do comando não aparecem. Em vez disso, use **Results to Text**.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TRIGGER safety   
ON DATABASE   
FOR CREATE_TABLE   
AS   
    PRINT 'CREATE TABLE Issued.'  
    SELECT EVENTDATA().value  
        ('(/EVENT_INSTANCE/TSQLCommand/CommandText)[1]','nvarchar(max)')  
   RAISERROR ('New tables cannot be created in this database.', 16, 1)   
   ROLLBACK  
;  
GO  
--Test the trigger.  
CREATE TABLE NewTable (Column1 int);  
GO  
--Drop the trigger.  
DROP TRIGGER safety  
ON DATABASE;  
GO  
```  
  
> [!NOTE]  
>  Para retornar dados de evento, use o método **value()** do XQuery em vez do método **query()** . O método **query()** retorna instâncias XML e CR/LF (Retorno de Carro e Alimentação de Linha) com escape com E comercial na saída, enquanto o método **value()** renderiza instâncias CR/LF invisíveis na saída.  
  
### <a name="b-creating-a-log-table-with-event-data-in-a-ddl-trigger"></a>b. Criando uma tabela de log com dados de evento em um gatilho DDL  
Este exemplo cria uma tabela para o armazenamento de informações sobre todos os eventos de nível de banco de dados e preenche a tabela com um gatilho DDL. O uso de XQuery em relação aos dados XML gerados por `EVENTDATA` captura o tipo de evento e a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE ddl_log (PostTime datetime, DB_User nvarchar(100), Event nvarchar(100), TSQL nvarchar(2000));  
GO  
CREATE TRIGGER log   
ON DATABASE   
FOR DDL_DATABASE_LEVEL_EVENTS   
AS  
DECLARE @data XML  
SET @data = EVENTDATA()  
INSERT ddl_log   
   (PostTime, DB_User, Event, TSQL)   
   VALUES   
   (GETDATE(),   
   CONVERT(nvarchar(100), CURRENT_USER),   
   @data.value('(/EVENT_INSTANCE/EventType)[1]', 'nvarchar(100)'),   
   @data.value('(/EVENT_INSTANCE/TSQLCommand)[1]', 'nvarchar(2000)') ) ;  
GO  
--Test the trigger.  
CREATE TABLE TestTable (a int);  
DROP TABLE TestTable ;  
GO  
SELECT * FROM ddl_log ;  
GO  
--Drop the trigger.  
DROP TRIGGER log  
ON DATABASE;  
GO  
--Drop table ddl_log.  
DROP TABLE ddl_log;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Usar a função EVENTDATA](../../relational-databases/triggers/use-the-eventdata-function.md)   
 [Gatilhos DDL](../../relational-databases/triggers/ddl-triggers.md)   
 [Notificações de eventos](../../relational-databases/service-broker/event-notifications.md)   
 [Gatilhos de logon](../../relational-databases/triggers/logon-triggers.md)  
  
  
