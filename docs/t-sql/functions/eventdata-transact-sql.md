---
title: EVENTDATA (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- EVENTDATA
- fn_event_data
- EVENTDATA_TSQL
- fn_event_data_TSQL
dev_langs: TSQL
helpviewer_keywords:
- server instance event data [SQL Server]
- event notifications [SQL Server], event status
- events [SQL Server], status infromation
- EVENTDATA function
- status information [SQL Server], events
- DDL triggers, returning event data
ms.assetid: 03a80e63-6f37-4b49-bf13-dc35cfe46c44
caps.latest.revision: "55"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 45f9d434e5833180320dcb3184fdcceec56c715c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="eventdata-transact-sql"></a>EVENTDATA (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna informações sobre eventos do servidor ou do banco de dados. EVENTDATA é chamado quando uma notificação de eventos é acionada, e os resultados são retornados ao agente de serviço especificado. EVENTDATA também pode ser usado no corpo de um gatilho DDL ou de logon.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
EVENTDATA( )  
```  
  
## <a name="remarks"></a>Comentários  
 EVENTDATA só retorna dados quando referenciado diretamente dentro de um gatilho DDL ou de logon. EVENTDATA retorna nulo se for chamado por outras rotinas, mesmo se essas rotinas forem chamadas por um gatilho DDL ou de logon.  
  
 Os dados retornados por EVENTDATA não serão válidos depois que uma transação que chamou EVENTDATA, implícita ou explicitamente, for confirmada ou revertida.  
  
> [!CAUTION]  
>  EVENTDATA retorna dados XML. Esses dados são enviados ao cliente como Unicode, que usa 2 bytes para cada caractere. Os pontos de código Unicode a seguir podem ser representados no XML que é retornado por EVENTDATA:  
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
>  Alguns caracteres que podem se aparecer em identificadores [!INCLUDE[tsql](../../includes/tsql-md.md)] e dados não são exprimíveis ou permissíveis em XML. Os caracteres ou os dados que tenham pontos de código não mostrados na lista anterior serão mapeados para um ponto de interrogação (?).  
  
 Para proteger a segurança de logons, quando instruções CREATE LOGIN ou ALTER LOGIN são executadas, as senhas não são exibidas.  
  
## <a name="schemas-returned"></a>Esquemas retornados  
 EVENTDATA retorna um valor do tipo **xml**. Por padrão, a definição de esquema de todos os eventos é instalada no seguinte diretório: [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]Tools\Binn\schemas\sqlserver\2006\11\events\events .xsd.  
  
 Como alternativa, o esquema de evento é publicado no [esquemas XML do Microsoft SQL Server](http://go.microsoft.com/fwlink/?LinkID=31850) página da Web.  
  
 Para extrair o esquema de qualquer evento específico, pesquise o esquema pelo Tipo Complexo `EVENT_INSTANCE_\<event_type>`. Por exemplo, para extrair o esquema do evento DROP_TABLE, pesquise o esquema por `EVENT_INSTANCE_DROP_TABLE`.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-querying-event-data-in-a-ddl-trigger"></a>A. Consultando dados de evento em um gatilho DDL  
 O exemplo a seguir cria um gatilho DDL para impedir que novas tabelas sejam criadas no banco de dados. A instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] que aciona o gatilho é capturada usando XQuery em relação aos dados XML gerados por EVENTDATA. Para obter mais informações, veja [Referência da linguagem XQuery &#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md).  
  
> [!NOTE]  
>  Quando você consulta o `\<TSQLCommand>` elemento usando **resultados em grade** em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], quebras de linha no texto do comando não são exibidos. Use **resultados em texto** em vez disso.  
  
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
>  Quando você quiser retornar dados de evento, recomendamos que você use o XQuery **Value ()** método em vez do **Query ()** método. O **Query ()** método retorna XML e com escape com e comercial carro e avanço de linha instâncias CR/LF () na saída, enquanto o **Value ()** método renderiza instâncias CR/LF invisíveis na saída.  
  
### <a name="b-creating-a-log-table-with-event-data-in-a-ddl-trigger"></a>B. Criando uma tabela de log com dados de evento em um gatilho DDL  
 O exemplo a seguir cria uma tabela para armazenar informações sobre todos os eventos no nível do banco de dados e popula a tabela com um gatilho DDL. O tipo do evento e a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] são capturados usando XQuery em relação aos dados XML gerados por `EVENTDATA`.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Usar a função EVENTDATA](../../relational-databases/triggers/use-the-eventdata-function.md)   
 [Gatilhos DDL](../../relational-databases/triggers/ddl-triggers.md)   
 [Notificações de eventos](../../relational-databases/service-broker/event-notifications.md)   
 [Gatilhos de logon](../../relational-databases/triggers/logon-triggers.md)  
  
  
