---
title: ALTER TRIGGER (Transact-SQL) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 05/08/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER TRIGGER
- ALTER_TRIGGER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DDL triggers, modifying
- triggers [SQL Server], modifying
- modifying triggers
- ALTER TRIGGER statement
- DML triggers, modifying
ms.assetid: 2a99c7c1-ac2f-4637-aa7c-3d1bf514e500
caps.latest.revision: 74
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1ae43399e1154e326ccee3d8760d59c71b73de5b
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="alter-trigger-transact-sql"></a>ALTER TRIGGER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Modifica a definição de um gatilho DML, DDL ou de logon que foi criado anteriormente pela instrução CREATE TRIGGER. Os gatilhos são criados com o uso de CREATE TRIGGER. Eles podem ser criados diretamente no [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções ou de métodos de assemblies que são criados no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] common language runtime (CLR) e carregados em uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações sobre os parâmetros que são usados na instrução ALTER TRIGGER, consulte [CREATE TRIGGER &#40; Transact-SQL &#41; ](../../t-sql/statements/create-trigger-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- SQL Server Syntax  
-- Trigger on an INSERT, UPDATE, or DELETE statement to a table or view (DML Trigger)  

ALTER TRIGGER schema_name.trigger_name   
ON  ( table | view )   
[ WITH <dml_trigger_option> [ ,...n ] ]  
 ( FOR | AFTER | INSTEAD OF )   
{ [ DELETE ] [ , ] [ INSERT ] [ , ] [ UPDATE ] }   
[ NOT FOR REPLICATION ]   
AS { sql_statement [ ; ] [ ...n ] | EXTERNAL NAME <method specifier>   
[ ; ] }   
  
<dml_trigger_option> ::=  
    [ ENCRYPTION ]  
    [ <EXECUTE AS Clause> ]  
  
<method_specifier> ::=  
    assembly_name.class_name.method_name  
  
-- Trigger on an INSERT, UPDATE, or DELETE statement to a table 
-- (DML Trigger on memory-optimized tables)  

ALTER TRIGGER schema_name.trigger_name   
ON  ( table  )   
[ WITH <dml_trigger_option> [ ,...n ] ]  
 ( FOR | AFTER )   
{ [ DELETE ] [ , ] [ INSERT ] [ , ] [ UPDATE ] }   
AS { sql_statement [ ; ] [ ...n ] }   
  
<dml_trigger_option> ::=  
    [ NATIVE_COMPILATION ]  
    [ SCHEMABINDING ]  
    [ <EXECUTE AS Clause> ]  
  
-- Trigger on a CREATE, ALTER, DROP, GRANT, DENY, REVOKE, 
-- or UPDATE statement (DDL Trigger)  
  
ALTER TRIGGER trigger_name   
ON { DATABASE | ALL SERVER }   
[ WITH <ddl_trigger_option> [ ,...n ] ]  
{ FOR | AFTER } { event_type [ ,...n ] | event_group }   
AS { sql_statement [ ; ] | EXTERNAL NAME <method specifier>   
[ ; ] }  
}   
  
<ddl_trigger_option> ::=  
    [ ENCRYPTION ]  
    [ <EXECUTE AS Clause> ]  
  
<method_specifier> ::=  
    assembly_name.class_name.method_name  
  
-- Trigger on a LOGON event (Logon Trigger)  

ALTER TRIGGER trigger_name   
ON ALL SERVER   
[ WITH <logon_trigger_option> [ ,...n ] ]  
{ FOR| AFTER } LOGON   
AS { sql_statement  [ ; ] [ ,...n ] | EXTERNAL NAME < method specifier >  
  [ ; ] }  
  
<logon_trigger_option> ::=  
    [ ENCRYPTION ]  
    [ EXECUTE AS Clause ]  
  
<method_specifier> ::=  
    assembly_name.class_name.method_name  
```  
  
```  
-- Windows Azure SQL Database Syntax   
-- Trigger on an INSERT, UPDATE, or DELETE statement to a table or view (DML Trigger)   
  
ALTER TRIGGER schema_name. trigger_name   
ON (table | view )   
 [ WITH <dml_trigger_option> [ ,...n ] ]   
 ( FOR | AFTER | INSTEAD OF )   
{ [ DELETE ] [ , ] [ INSERT ] [ , ] [ UPDATE ] }   
AS { sql_statement [ ; ] [...n ] }   
  
<dml_trigger_option> ::=   
    [ <EXECUTE AS Clause> ]   
  
-- Trigger on a CREATE, ALTER, DROP, GRANT, DENY, REVOKE, or UPDATE statement (DDL Trigger)   
  
ALTER TRIGGER trigger_name   
ON { DATABASE }   
 [ WITH <ddl_trigger_option> [ ,...n ] ]   
{ FOR | AFTER } { event_type [ ,...n ] | event_group }   
AS { sql_statement   
[ ; ] }  
}   
  
<ddl_trigger_option> ::=   
    [ <EXECUTE AS Clause> ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *schema_name*  
 É o nome do esquema ao qual o gatilho DML pertence. Os gatilhos DML são definidos no escopo do esquema da tabela ou na exibição na qual são criados. *esquema**name* é opcional somente se o gatilho DML e sua tabela correspondente ou exibição pertence ao esquema padrão. *schema_name* não pode ser especificado para gatilhos DDL ou de logon.  
  
 *trigger_name*  
 É o gatilho existente a ser modificado.  
  
 *tabela* | *exibição*  
 É a tabela ou a exibição na qual o gatilho DML é executado. A especificação do nome totalmente qualificado da tabela ou da exibição é opcional.  
  
 DATABASE  
 Aplica o escopo de um gatilho DDL ao banco de dados atual. Se especificado, o gatilho é acionado sempre que *event_type* ou *event_group* ocorre no banco de dados atual.  
  
 ALL SERVER  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Aplica o escopo de um gatilho DDL ou de logon ao servidor atual. Se especificado, o gatilho é acionado sempre que *event_type* ou *event_group* ocorrer em qualquer lugar no servidor atual.  
  
 WITH ENCRYPTION  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Criptografa as entradas de sys.syscommentssys.sql_modules que contêm o texto da instrução ALTER TRIGGER. O uso de WITH ENCRYPTION impede que o gatilho seja publicado como parte da replicação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. WITH ENCRYPTION não pode ser especificado para gatilhos CLR.  
  
> [!NOTE]  
>  Se um gatilho for criado com o uso de WITH ENCRYPTION, ele deverá ser especificado novamente na instrução ALTER TRIGGER para que essa opção permaneça ativada.  
  
 EXECUTE AS  
 Especifica o contexto de segurança no qual o gatilho é executado. Permite controlar a conta de usuário do que a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa para validar permissões em quaisquer objetos de banco de dados que são referenciadas pelo gatilho.  
  
 Para obter mais informações, veja [Cláusula EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md).  
  
 NATIVE_COMPILATION  
 Indica que o gatilho é compilado nativamente.  
  
 Essa opção é necessária para os gatilhos em tabelas com otimização de memória.  
  
 SCHEMABINDING  
 Garante que as tabelas referenciadas por um gatilho não podem ser descartadas ou alteradas.  
  
 Essa opção é necessária para os gatilhos em tabelas com otimização de memória e não há suporte para gatilhos em tabelas tradicionais.  
  
 AFTER  
 Especifica que o gatilho será acionado apenas depois que a instrução SQL disparadora for executada com êxito. Todas as verificações de restrição e ações referenciais em cascata também devem ter obtido êxito antes que este gatilho seja acionado.  
  
 AFTER é o padrão se apenas a palavra-chave FOR for especificada.  
  
 Os gatilhos DML AFTER podem ser definidos apenas em tabelas.  
  
 INSTEAD OF  
 Especifica que o gatilho DML será executado no lugar da instrução SQL de gatilho, substituindo assim as ações das instruções de gatilho. INSTEAD OF não pode ser especificado para gatilhos DDL ou de logon.  
  
 No máximo, um gatilho INSTEAD OF por instrução INSERT, UPDATE ou DELETE pode ser definido em uma tabela ou exibição. Entretanto, você pode definir exibições sobre exibições, onde cada uma tem seu próprio gatilho INSTEAD OF.  
  
 Os gatilhos INSTEAD OF não são permitidos em exibições criadas com o uso de WITH CHECK OPTION. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gera um erro quando um gatilho INSTEAD OF é adicionado a uma exibição para a qual WITH CHECK OPTION foi especificado. O usuário deve remover essa opção usando ALTER VIEW antes de definir o gatilho INSTEAD OF.  
  
 { [ DELETE ] [ , ] [ INSERT ] [ , ] [ UPDATE ] } | { [INSERT ] [ , ] [ UPDATE ] }  
 Especifica as instruções de modificação de dados que, quando tentadas em relação a esta tabela ou exibição, ativam o gatilho DML. É necessário especificar pelo menos uma opção. É permitida qualquer combinação delas em qualquer ordem na definição do gatilho. Se mais de uma opção for especificada, separe-as com vírgulas.  
  
 Para gatilhos INSTEAD OF, a opção DELETE não é permitida em tabelas que tenham um relacionamento referencial que especifique uma ação ON DELETE em cascata. Da mesma maneira, a opção UPDATE não é permitida em tabelas que tenham um relacionamento referencial que especifique uma ação ON UPDATE em cascata. Para obter mais informações, veja [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md).  
  
 *event_type*  
 É o nome de um evento da linguagem [!INCLUDE[tsql](../../includes/tsql-md.md)] que, após a execução, faz com que um gatilho DDL seja acionado. Os eventos válidos para gatilhos DDL estão listados no [eventos DDL](../../relational-databases/triggers/ddl-events.md).  
  
 *event_group*  
 É o nome de um agrupamento predefinido de eventos da linguagem [!INCLUDE[tsql](../../includes/tsql-md.md)]. O gatilho DDL será acionado após a execução de qualquer [!INCLUDE[tsql](../../includes/tsql-md.md)] evento de linguagem que pertence a *event_group*. Grupos de eventos válidos para gatilhos DDL são listados na [grupos de eventos DDL](../../relational-databases/triggers/ddl-event-groups.md). Após a conclusão da execução, ALTER TRIGGER *event_group* também atuará como uma macro adicionando os tipos de evento abrangidos por ele à exibição de catálogo trigger_events.  
  
 NOT FOR REPLICATION  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Indica que o gatilho não deve ser executado quando um agente de replicação modificar a tabela envolvida no gatilho.  
  
 *sql_statement*  
 São as condições e as ações do gatilho.  
  
 Para gatilhos em tabelas com otimização de memória, o único *sql_statement* permitido no nível superior é um bloco ATÔMICO. O T-SQL permitido dentro do bloco ATÔMICO é limitado pelo T-SQL permitido dentro de PROC. nativos.  
  
 NOME externo \<method_specifier >  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica o método de um assembly a ser associado ao gatilho. O método não deve usar nenhum argumento e deve retornar nulo. *class_name* deve ser um válido [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identificador e deve existir como uma classe no assembly com visibilidade do assembly. A classe não pode ser aninhada.  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações sobre ALTER TRIGGER, consulte comentários em [CREATE TRIGGER &#40; Transact-SQL &#41; ](../../t-sql/statements/create-trigger-transact-sql.md).  
  
> [!NOTE]  
>  As opções EXTERNAL_NAME e ON_ALL_SERVER não estão disponíveis em um banco de dados independente.  
  
## <a name="dml-triggers"></a>Gatilhos DML  
 ALTER TRIGGER oferece suporte a exibições atualizáveis manualmente por meio de gatilhos INSTEAD OF em tabelas e exibições. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aplica ALTER TRIGGER da mesma maneira para todos os tipos de gatilhos (AFTER, INSTEAD-OF).  
  
 Os primeiro e o último gatilhos AFTER a serem executados em uma tabela podem ser especificados usando sp_settriggerorder. Apenas um primeiro e um último gatilho AFTER podem ser especificados em uma tabela. Se houver outros gatilhos AFTER na mesma tabela, eles serão executados aleatoriamente.  
  
 Se uma instrução ALTER TRIGGER alterar um primeiro ou último gatilho, o primeiro ou o último atributo definido no gatilho modificado será descartado e o valor da ordem deverá ser redefinido usando-se sp_settriggerorder.  
  
 Um gatilho AFTER é executado apenas depois que a instrução SQL disparadora for executada com êxito. Essa execução com êxito inclui todas as verificações de restrição e ações referenciais em cascata associadas ao objeto atualizado ou excluído. A operação do gatilho AFTER verifica os efeitos da instrução disparadora e também todas as ações UPDATE e DELETE referenciais em cascata causadas pela instrução disparadora.  
  
 Quando uma ação DELETE para uma tabela filha ou de referência for o resultado de CASCADE em DELETE da tabela pai e um gatilho INSTEAD OF em DELETE estiver definido nessa tabela filha, o gatilho será ignorado e a ação DELETE será executada.  
  
## <a name="ddl-triggers"></a>Gatilhos DDL  
 Diferentemente dos gatilhos DML, os gatilhos DDL não têm seu escopo definido para esquemas. Portanto, não é possível usar OBJECT_ID, OBJECT_NAME, OBJECTPROPERTY e OBJECTPROPERTY(EX) ao consultar metadados sobre gatilhos DDL. Use as exibições do catálogo em vez disso. Para obter mais informações, consulte [obter informações sobre gatilhos DDL](../../relational-databases/triggers/get-information-about-ddl-triggers.md).  
  
## <a name="logon-triggers"></a>Gatilhos de logon  
 O [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] não oferece suporte a gatilhos em eventos de logon.  
  
## <a name="permissions"></a>Permissões  
 A alteração de um gatilho DML exige permissão ALTER na tabela ou exibição na qual o gatilho está definido.  
  
 A alteração de um gatilho DDL definido com escopo no servidor (ON ALL SERVER) ou de um gatilho de logon exige permissão CONTROL SERVER no servidor. A alteração de um gatilho DDL definido com escopo no banco de dados (ON DATABASE) exige permissão ALTER ANY DATABASE DDL TRIGGER no banco de dados atual.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria um gatilho DML no banco de dados AdventureWorks 2012, que imprime uma mensagem definida pelo usuário para o cliente quando um usuário tenta adicionar ou alterar dados no `SalesPersonQuotaHistory` tabela. Em seguida, o gatilho é modificado usando `ALTER TRIGGER` para aplicar o gatilho apenas em atividades `INSERT`. Esse gatilho é útil porque lembra ao usuário que atualiza ou insere linhas nessa tabela que também notifique o departamento `Compensation` .  
  
```  
CREATE TRIGGER Sales.bonus_reminder  
ON Sales.SalesPersonQuotaHistory  
WITH ENCRYPTION  
AFTER INSERT, UPDATE   
AS RAISERROR ('Notify Compensation', 16, 10);  
GO  

-- Now, change the trigger.  
ALTER TRIGGER Sales.bonus_reminder  
ON Sales.SalesPersonQuotaHistory  
AFTER INSERT  
AS RAISERROR ('Notify Compensation', 16, 10);  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [ENABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/enable-trigger-transact-sql.md)   
 [DISABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/disable-trigger-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_helptrigger &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptrigger-transact-sql.md)   
 [Criar um procedimento armazenado](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [sp_addmessage &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)   
 [Transações](../../relational-databases/native-client-ole-db-transactions/transactions.md)   
 [Obter informações sobre gatilhos DML](../../relational-databases/triggers/get-information-about-dml-triggers.md)   
 [Obter informações sobre gatilhos DDL](../../relational-databases/triggers/get-information-about-ddl-triggers.md)   
 [sys.triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)   
 [sys.trigger_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trigger-events-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)   
 [sys.server_triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md)   
 [sys.server_trigger_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-trigger-events-transact-sql.md)   
 [sys.server_sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-sql-modules-transact-sql.md)   
 [sys.server_assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-assembly-modules-transact-sql.md)   
 [Fazer alterações de esquema em bancos de dados de publicação](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)  
  
  

