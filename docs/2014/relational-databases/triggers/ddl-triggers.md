---
title: Gatilhos DDL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- DDL triggers, about DDL triggers
ms.assetid: 1a4a6564-9820-4a14-9305-2c0e9ea37454
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b65cc412f2e9cb1ea2058a52ae8336c7827b9ca3
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37412735"
---
# <a name="ddl-triggers"></a>Gatilhos DDL
  Os gatilhos DDL são disparados em resposta a diversos eventos DDL (linguagem de definição de dados). Esses eventos correspondem principalmente a instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] que começam com as palavras-chave CREATE, ALTER, DROP, GRANT, DENY, REVOKE ou UPDATE STATISTICS. Determinados procedimentos armazenados do sistema que executam operações do tipo DDL também podem disparar gatilhos DDL.  
  
 Use gatilhos DDL quando quiser fazer o seguinte:  
  
-   Evitar determinadas alterações em seu esquema de banco de dados.  
  
-   Ocorrer algo no banco de dados em resposta a uma alteração em seu esquema de banco de dados.  
  
-   Registrar alterações ou eventos no esquema de banco de dados.  
  
> [!IMPORTANT]  
>  Teste seus gatilhos DDL para determinar suas respostas aos procedimentos armazenados do sistema que são executados. Por exemplo, a instrução CREATE TYPE e o procedimento armazenado **sp_addtype** dispararão um gatilho DDL criado em um evento CREATE_TYPE.  
  
## <a name="types-of-ddl-triggers"></a>Tipos de gatilhos DDL  
 Gatilho DDL Transact-SQL  
 Um tipo especial de procedimento armazenado [!INCLUDE[tsql](../../includes/tsql-md.md)] que executa uma ou mais instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] em resposta a um evento com escopo de servidor ou de banco de dados. Por exemplo, um Gatilho DDL poderá ser disparado se uma instrução como ALTER SERVER CONFIGURATION for executada ou se uma tabela for excluída usando DROP TABLE.  
  
 Gatilho DDL CLR  
 Em vez de executar um procedimento armazenado [!INCLUDE[tsql](../../includes/tsql-md.md)] , um gatilho CLR executa um ou mais métodos gravados em código gerenciado que são membros de um assembly criado no .NET Framework e carregado para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Os gatilhos DDL são disparados somente após a execução das instruções DDL que os dispararam. Os gatilhos DDL não podem ser usados como gatilhos INSTEAD OF. Os gatilhos DDL não são disparados em resposta a eventos que afetem tabelas temporárias locais ou globais e procedimentos armazenados.  
  
 Gatilhos DDL não criam especiais `inserted` e `deleted` tabelas.  
  
 As informações sobre um evento que dispara um gatilho DDL e as alterações subsequentes causadas pelo gatilho são capturadas por meio da função EVENTDATA.  
  
 Vários gatilhos a serem criados para cada evento DDL.  
  
 Diferentemente dos gatilhos DML, os gatilhos DDL não têm seu escopo definido para esquemas. Portanto, funções como OBJECT_ID, OBJECT_NAME, OBJECTPROPERTY e OBJECTPROPERTYEX não podem ser usadas para consultar metadados sobre gatilhos DDL. Use as exibições do catálogo em vez disso.  
  
 Os gatilhos DDL com escopo de servidor aparecem no Pesquisador de Objetos do SQL Server Management Studio na pasta **Triggers** . Essa pasta está localizada na pasta **Server Objects** . Os gatilhos DDL com escopo de banco de dados aparecem na pasta **Database Triggers** . Essa pasta fica localizada na pasta **Programmability** do banco de dados correspondente.  
  
> [!IMPORTANT]  
>  Um código mal-intencionado dentro de gatilhos pode ser executado sob privilégios escalonados. Para obter mais informações sobre como ajudar a reduzir essa ameaça, consulte [Gerenciar a segurança dos gatilhos](manage-trigger-security.md).  
  
## <a name="ddl-trigger-scope"></a>Escopo do gatilho DDL  
 Os gatilhos DDL podem ser disparados em resposta a um evento [!INCLUDE[tsql](../../includes/tsql-md.md)] processado no banco de dados ou no servidor atual. O escopo do gatilho depende do evento. Por exemplo, um gatilho DDL criado para ser acionado em resposta a um evento CREATE_TABLE poderá sê-lo sempre que um evento CREATE_TABLE ocorrer no banco de dados ou na instância do servidor. Um gatilho DDL criado para ser disparado em resposta a um evento CREATE_LOGIN só poderá sê-lo quando um evento CREATE_LOGIN ocorrer na instância do servidor.  
  
 No exemplo a seguir, o gatilho DDL `safety` será disparado sempre que um evento `DROP_TABLE` ou `ALTER_TABLE` ocorrer no banco de dados.  
  
```  
CREATE TRIGGER safety   
ON DATABASE   
FOR DROP_TABLE, ALTER_TABLE   
AS   
   PRINT 'You must disable Trigger "safety" to drop or alter tables!'   
   ROLLBACK;  
```  
  
 No exemplo a seguir, um gatilho DDL imprimirá uma mensagem caso ocorra algum evento `CREATE_DATABASE` na instância de servidor atual. O exemplo usa a função `EVENTDATA` para recuperar o texto da instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] correspondente. Para obter mais informações sobre como usar EVENTDATA com gatilhos DDL, consulte [Usar a função EVENTDATA](use-the-eventdata-function.md).  
  
```  
IF EXISTS (SELECT * FROM sys.server_triggers  
    WHERE name = 'ddl_trig_database')  
DROP TRIGGER ddl_trig_database  
ON ALL SERVER;  
GO  
CREATE TRIGGER ddl_trig_database   
ON ALL SERVER   
FOR CREATE_DATABASE   
AS   
    PRINT 'Database Created.'  
    SELECT EVENTDATA().value('(/EVENT_INSTANCE/TSQLCommand/CommandText)[1]','nvarchar(max)')  
GO  
DROP TRIGGER ddl_trig_database  
ON ALL SERVER;  
GO  
  
```  
  
 A lista que mapeia as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] para os escopos que podem ser especificados para elas está disponível através dos links fornecidos na seção "Selecionando uma instrução DDL em particular para acionar um gatilho DDL", mais adiante, neste tópico.  
  
 Os gatilhos DDL com escopo de banco de dados são armazenados como objetos no banco de dados em que são criados. Os gatilhos DDL podem ser criados no banco de dados **mestre** e se comportam de forma idêntica àqueles criados em bancos de dados criados pelo usuário. Você pode obter informações sobre gatilhos DDL consultando a exibição de catálogo **sys.triggers** . Você pode consultar **sys.triggers** dentro do contexto do banco de dados em que foram criados os gatilhos ou especificar o nome do banco de dados como identificador, por exemplo, **master.sys.triggers**.  
  
 Os gatilhos DDL com escopo de servidor são armazenados como objetos no banco de dados **mestre** . É possível, contudo, obter informações sobre gatilhos DDL com escopo de servidor consultando a exibição de catálogo **sys.server_triggers** em qualquer contexto de banco de dados.  
  
## <a name="specifying-a-transact-sql-statement-or-group-of-statements"></a>Especificando uma instrução ou grupo de instruções Transact-SQL  
  
### <a name="selecting-a-particular-ddl-statement-to-fire-a-ddl-trigger"></a>Selecionando uma instrução DDL em particular para disparar um gatilho DDL  
 É possível designar os gatilhos DDL para que sejam disparados após a execução de uma ou mais instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] . No exemplo anterior, o gatilho `safety` é acionado mediante qualquer evento `DROP_TABLE` ou `ALTER_TABLE` . Para obter listas das instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] que podem ser especificadas para acionar um gatilho DDL e o escopo no qual o gatilho pode ser acionado, consulte [Eventos DDL](ddl-events.md).  
  
### <a name="selecting-a-predefined-group-of-ddl-statements-to-fire-a-ddl-trigger"></a>Selecionando um grupo predefinido de instruções DDL para acionar um gatilho DDL  
 Um gatilho DDL pode ser acionado mediante a execução de qualquer evento [!INCLUDE[tsql](../../includes/tsql-md.md)] pertencente a um grupo predefinido de eventos similares. Por exemplo, se desejar que um gatilho DDL seja acionado mediante a execução de uma instrução CREATE TABLE, ALTER TABLE ou DROP TABLE, você pode especificar FOR DDL_TABLE_EVENTS na instrução CREATE TRIGGER. Após a execução de CREATE TRIGGER, os eventos compreendidos pelo grupo de eventos serão adicionados à exibição de catálogo **sys.trigger_events** .  
  
 No [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], se um gatilho for criado em um grupo de eventos, **sys.trigger_events** não conterá informações sobre o grupo de eventos, o **sys.trigger_events** inclui informações somente sobre os eventos individuais compreendidos pelo grupo. No [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e em versões posteriores, o **sys.trigger_events** mantém metadados sobre o grupo de eventos no qual os gatilhos são criados e também sobre os eventos individuais que o grupo de eventos abrange. Portanto, as alterações nos eventos compreendidos pelos grupos de eventos no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e em versões posteriores não se aplicam aos gatilhos DDL criados nesses grupos de eventos no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
 Para obter uma lista de grupos predefinidos de instruções DDL disponíveis para gatilhos DDL, as instruções abarcadas pelos grupos de eventos e os escopos nos quais esses grupos de eventos podem ser programados, consulte [DDL Event Groups](ddl-event-groups.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Tarefa|Tópico|  
|----------|-----------|  
|Descreve como criar, modificar, excluir ou desabilitar gatilhos DDL.|[Implementar gatilhos DDL](implement-ddl-triggers.md)|  
|Descreve como criar um gatilho DDL CLR.|[Criar gatilhos CLR](create-clr-triggers.md)|  
|Descreve como retornar informações sobre gatilhos DDL.|[Obter informações sobre gatilhos DDL](get-information-about-ddl-triggers.md)|  
|Descreve como retornar informações sobre um evento que dispara um gatilho DDL por meio da função EVENTDATA.|[Usar a função EVENTDATA](use-the-eventdata-function.md)|  
|Descreve como gerenciar a segurança do gatilho.|[Gerenciar a segurança dos gatilhos](manage-trigger-security.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Gatilhos DML](dml-triggers.md)   
 [Gatilhos de logon](logon-triggers.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql)  
  
  
