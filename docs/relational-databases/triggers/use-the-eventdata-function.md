---
title: "Usar a função EVENTDATA | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-ddl
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- EVENTDATA function
- DDL triggers, EVENTDATA function
ms.assetid: 675b8320-9c73-4526-bd2f-91ba42c1b604
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5cb1a29cd7638f5ec9a4248f615381fe6da721b9
ms.lasthandoff: 04/11/2017

---
# <a name="use-the-eventdata-function"></a>Usar a função EVENTDATA
  As informações sobre um evento que aciona um disparador DDL são capturadas por meio da função EVENTDATA. Essa função retorna um valor **xml** . O esquema XML contém informações sobre o seguinte:  
  
-   A hora do evento.  
  
-   A ID de processo do sistema (SPID) da conexão no momento da execução do gatilho.  
  
-   O tipo de evento que acionou o gatilho.  
  
 Dependendo do tipo de evento, o esquema poderá conter ainda outras informações, como o banco de dados em que o evento ocorreu, o objeto em relação ao qual ele ocorreu e a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] do evento. Para obter mais informações, consulte [DDL Triggers](../../relational-databases/triggers/ddl-triggers.md).  
  
 Por exemplo, o seguinte disparador DDL é criado no banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] :  
  
```  
CREATE TRIGGER safety   
ON DATABASE   
FOR CREATE_TABLE   
AS   
    PRINT 'CREATE TABLE Issued.'  
    SELECT EVENTDATA().value('(/EVENT_INSTANCE/TSQLCommand/CommandText)[1]','nvarchar(max)')  
   RAISERROR ('New tables cannot be created in this database.', 16, 1)   
   ROLLBACK  
;  
```  
  
 Em seguida, é executada a seguinte instrução `CREATE TABLE` :  
  
 `CREATE TABLE NewTable (Column1 int);`  
  
 A instrução `EVENTDATA()` no gatilho DDL captura o texto da instrução `CREATE TABLE` , que não é permitida. Isso é feito pelo uso de uma instrução XQuery nos dados **xml** gerados por EVENTDATA e pela recuperação do elemento \<CommandText>. Para obter mais informações, veja [Referência da linguagem XQuery &#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md).  
  
> [!CAUTION]  
>  A EVENTDATA captura os dados de eventos CREATE_SCHEMA, bem como o <schema_element> da definição CREATE SCHEMA correspondente, se houver. Além disso, EVENTDATA reconhece a definição <schema_element>como um evento separado. Portanto, um disparador DDL criado em ambos os eventos CREATE SCHEMA e um evento representado pelo <schema_element> da definição CREATE SCHEMA podem retornar os mesmos dados de evento duas vezes, como os dados de `TSQLCommand`. Por exemplo, considere um disparador DDL criado em ambos os eventos CREATE_SCHEMA e CREATE_TABLE e a execução do seguinte lote:  
>   
>  `CREATE SCHEMA s`  
>   
>  `CREATE TABLE t1 (col1 int)`  
>   
>  Se o aplicativo recuperar os dados de `TSQLCommand` do evento CREATE_TABLE, lembre-se de que esses dados podem aparecer duas vezes: primeiro, quando ocorre o evento CREATE_SCHEMA e, outra vez, quando ocorre o evento CREATE_TABLE. Evite criar disparadores DDL em ambos os eventos CREATE_SCHEMA e nos textos de <schema_element> de quaisquer definições CREATE SCHEMA correspondentes ou crie lógica em seu aplicativo para que o mesmo evento não seja processado duas vezes.  
  
## <a name="alter-table-and-alter-database-events"></a>Eventos ALTER TABLE e ALTER DATABASE  
 Os dados de eventos para os eventos ALTER_TABLE e ALTER_DATABASE também incluem os nomes e os tipos de outros objetos afetados pela instrução DDL e pela ação executada nesses objetos. Os dados do evento ALTER_TABLE incluem os nomes das colunas, as limitações os aciondores afetados pela instrução ALTER TABLE e a ação (criar, alterar, descartar, habilitar ou desabilitar) executada nesses objetos. Os dados do evento ALTER_DATABASE incluem os nomes de qualquer arquivo ou grupos de arquivos afetados pela instução ALTER DATABASE e a ação (criar, alterar, descartar) executada nos objetos afetados.  
  
 Por exemplo, crie o seguinte gatilho DDL no banco de dados de exemplo Adventure Works:  
  
```  
CREATE TRIGGER ColumnChanges  
ON DATABASE   
FOR ALTER_TABLE  
AS  
-- Detect whether a column was created/altered/dropped.  
SELECT EVENTDATA().value('(/EVENT_INSTANCE/TSQLCommand/CommandText)[1]', 'nvarchar(max)')  
RAISERROR ('Table schema cannot be modified in this database.', 16, 1);  
ROLLBACK;  
```  
  
 Então execute a instrução ALTER TABLE seguinte que viola uma restrição:  
  
```  
ALTER TABLE Person.Address ALTER COLUMN ModifiedDate date;   
```  
  
 A instrução EVENTDATA() no gatilho DDL captura o texto da instrução `ALTER TABLE` , que não é permitida.  
  
## <a name="example"></a>Exemplo  
 Você pode usar a função EVENTDATA para criar um log de eventos. No exemplo a seguir, é criada uma tabela para armazenar informações de evento. Em seguida, é criado um disparador DDL no banco de dados atual que popula a tabela com as seguintes informações, sempre que ocorre algum evento DDL em nível de banco de dados:  
  
-   A hora do evento (usando a função GETDATE).  
  
-   O usuário de banco de dados em relação ao qual ocorreu o evento (usando a função CURRENT_USER).  
  
-   O tipo de evento.  
  
-   A instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] que capturou o evento.  
  
 Outra vez, os últimos dois itens são capturados com o XQuery nos dados **xml** gerados por EVENTDATA.  
  
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
--Test the trigger  
CREATE TABLE TestTable (a int)  
DROP TABLE TestTable ;  
GO  
SELECT * FROM ddl_log ;  
GO  
```  
  
> [!NOTE]  
>  Para retornar dados de evento, recomenda-se usar o método **value()** do XQuery em vez do método **query()** . O método **query()** retorna instâncias XML e CRLF (retorno de carro e alimentação de linha) com escape com E comercial na saída, enquanto o método **value()** renderiza instâncias CRLF invisíveis na saída.  
  
 Um exemplo similar de disparador DDL é fornecido com o banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Para obter o exemplo, localize a pasta Gatilhos de Banco de Dados, usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Esta pasta está localizada na pasta **Programação** do banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] . Clique com o botão direito do mouse em **ddlDatabseTriggerLog** e selecione **Script de Gatilho de Banco de Dados como**. Por padrão, o gatilho DDL **ddlDatabseTriggerLog** está desabilitado.  
  
## <a name="see-also"></a>Consulte também  
 [Eventos DDL](../../relational-databases/triggers/ddl-events.md)   
 [Grupos de eventos DDL](../../relational-databases/triggers/ddl-event-groups.md)  
  
  
