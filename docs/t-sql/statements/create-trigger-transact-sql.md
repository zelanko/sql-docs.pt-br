---
title: CREATE TRIGGER (Transact-SQL) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE TRIGGER
- TRIGGER
- CREATE_TRIGGER_TSQL
- TRIGGER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- recursive DML triggers [SQL Server]
- CREATE TRIGGER statement
- multiple triggers
- deferred name resolution, DML triggers
- DML triggers, creating
- nested triggers
- server-scoped triggers
- DDL triggers, creating
- triggers [SQL Server], creating
- database-scoped triggers [SQL Server]
ms.assetid: edeced03-decd-44c3-8c74-2c02f801d3e7
caps.latest.revision: 140
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 56011e892d5fbc5862f3d7c279bc297c3d0ac04c
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="create-trigger-transact-sql"></a>CREATE TRIGGER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Cria um gatilho DML, DDL ou de logon. Um gatilho é um tipo especial de procedimento armazenado que é executado automaticamente quando um evento ocorre no servidor de banco de dados. Os gatilhos DML são executados quando um usuário tenta modificar dados através de um evento DML (linguagem de manipulação de dados). Os eventos DML são instruções INSERT, UPDATE ou DELETE em uma tabela ou exibição. Esses gatilhos são disparados quando qualquer evento válido é acionado, independentemente de quaisquer linhas da tabela serem afetadas ou não. Para obter mais informações, consulte [DML Triggers](../../relational-databases/triggers/dml-triggers.md).  
  
 Os gatilhos DDL são executados em resposta a diversos eventos DDL (linguagem de definição de dados). Esses eventos correspondem, basicamente, a instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE, ALTER e DROP e determinados procedimentos armazenados do sistema que executam operações do tipo DDL. Os gatilhos de logon são disparados em resposta ao evento LOGON que é gerado quando as sessões de um usuário estão sendo estabelecidas. Gatilhos podem ser criados diretamente no [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções ou de métodos de assemblies que são criados no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] common language runtime (CLR) e carregados em uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite criar vários gatilhos para qualquer instrução específica.  
  
> [!IMPORTANT]  
>  Um código mal-intencionado dentro de gatilhos pode ser executado sob privilégios escalonados. Para obter mais informações sobre como reduzir essa ameaça, consulte [gerenciar segurança do gatilho](../../relational-databases/triggers/manage-trigger-security.md).  
  
> [!NOTE]  
>  A integração do CLR do .NET Framework para SQL Server é discutida neste tópico. Integração CLR não se aplica ao banco de dados do SQL Azure.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- SQL Server Syntax  
-- Trigger on an INSERT, UPDATE, or DELETE statement to a table or view (DML Trigger)  
  
CREATE [ OR ALTER ] TRIGGER [ schema_name . ]trigger_name   
ON { table | view }   
[ WITH <dml_trigger_option> [ ,...n ] ]  
{ FOR | AFTER | INSTEAD OF }   
{ [ INSERT ] [ , ] [ UPDATE ] [ , ] [ DELETE ] }   
[ WITH APPEND ]  
[ NOT FOR REPLICATION ]   
AS { sql_statement  [ ; ] [ ,...n ] | EXTERNAL NAME <method specifier [ ; ] > }  
  
<dml_trigger_option> ::=  
    [ ENCRYPTION ]  
    [ EXECUTE AS Clause ]  
  
<method_specifier> ::=  
    assembly_name.class_name.method_name  
  
```  
  
```  
-- SQL Server Syntax  
-- Trigger on an INSERT, UPDATE, or DELETE statement to a 
-- table (DML Trigger on memory-optimized tables)  
  
CREATE [ OR ALTER ] TRIGGER [ schema_name . ]trigger_name   
ON { table }   
[ WITH <dml_trigger_option> [ ,...n ] ]  
{ FOR | AFTER }   
{ [ INSERT ] [ , ] [ UPDATE ] [ , ] [ DELETE ] }   
AS { sql_statement  [ ; ] [ ,...n ] }  
  
<dml_trigger_option> ::=  
    [ NATIVE_COMPILATION ]  
    [ SCHEMABINDING ]  
    [ EXECUTE AS Clause ]  
  
```  
  
```  
-- Trigger on a CREATE, ALTER, DROP, GRANT, DENY, 
-- REVOKE or UPDATE statement (DDL Trigger)  
  
CREATE [ OR ALTER ] TRIGGER trigger_name   
ON { ALL SERVER | DATABASE }   
[ WITH <ddl_trigger_option> [ ,...n ] ]  
{ FOR | AFTER } { event_type | event_group } [ ,...n ]  
AS { sql_statement  [ ; ] [ ,...n ] | EXTERNAL NAME < method specifier >  [ ; ] }  
  
<ddl_trigger_option> ::=  
    [ ENCRYPTION ]  
    [ EXECUTE AS Clause ]  
  
```  
  
```  
-- Trigger on a LOGON event (Logon Trigger)  
  
CREATE [ OR ALTER ] TRIGGER trigger_name   
ON ALL SERVER   
[ WITH <logon_trigger_option> [ ,...n ] ]  
{ FOR| AFTER } LOGON    
AS { sql_statement  [ ; ] [ ,...n ] | EXTERNAL NAME < method specifier >  [ ; ] }  
  
<logon_trigger_option> ::=  
    [ ENCRYPTION ]  
    [ EXECUTE AS Clause ]  
  
```  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Windows Azure SQL Database Syntax   
-- Trigger on an INSERT, UPDATE, or DELETE statement to a table or view (DML Trigger)  
  
CREATE [ OR ALTER ] TRIGGER [ schema_name . ]trigger_name   
ON { table | view }   
 [ WITH <dml_trigger_option> [ ,...n ] ]   
{ FOR | AFTER | INSTEAD OF }   
{ [ INSERT ] [ , ] [ UPDATE ] [ , ] [ DELETE ] }   
  AS { sql_statement  [ ; ] [ ,...n ] [ ; ] > }  
  
<dml_trigger_option> ::=   
        [ EXECUTE AS Clause ]  
  
```  
  
```  
-- Windows Azure SQL Database Syntax  
-- Trigger on a CREATE, ALTER, DROP, GRANT, DENY, 
-- REVOKE, or UPDATE STATISTICS statement (DDL Trigger)   
  
CREATE [ OR ALTER ] TRIGGER trigger_name   
ON { DATABASE }   
 [ WITH <ddl_trigger_option> [ ,...n ] ]   
{ FOR | AFTER } { event_type | event_group } [ ,...n ]   
AS { sql_statement  [ ; ] [ ,...n ]  [ ; ] }  
  
<ddl_trigger_option> ::=   
    [ EXECUTE AS Clause ]  
```  
  
## <a name="arguments"></a>Argumentos
OU ALTER  
 **Aplica-se a**: Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1). 
  
 Condicionalmente altera o disparador somente se ele já existe. 
  
 *schema_name*  
 É o nome do esquema ao qual o gatilho DML pertence. Os gatilhos DML são definidos no escopo do esquema da tabela ou na exibição na qual são criados. *schema_name* não pode ser especificado para gatilhos DDL ou de logon.  
  
 *trigger_name*  
 É o nome do gatilho. Um *trigger_name* devem estar de acordo com as regras de [identificadores](../../relational-databases/databases/database-identifiers.md), exceto que *trigger_name* não pode começar com # ou # #.  
  
 *tabela* | *exibição*  
 É a tabela ou exibição na qual o gatilho DML é executado e às vezes referenciado como a tabela de gatilho ou exibição de gatilho. Especifica o nome totalmente qualificado da tabela ou exibição é opcional. Uma exibição só pode ser referenciada por um gatilho INSTEAD OF. Gatilhos DML não podem ser definidos em tabelas temporárias locais ou globais.  
  
 DATABASE  
 Aplica o escopo de um gatilho DDL ao banco de dados atual. Se especificado, o gatilho é acionado sempre que *event_type* ou *event_group* ocorre no banco de dados atual.  
  
 ALL SERVER  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Aplica o escopo de um gatilho DDL ou de logon ao servidor atual. Se especificado, o gatilho é acionado sempre que *event_type* ou *event_group* ocorrer em qualquer lugar no servidor atual.  
  
 WITH ENCRYPTION  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Ofusca o texto da instrução CREATE TRIGGER. O uso de WITH ENCRYPTION impede que o gatilho seja publicado como parte da replicação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. WITH ENCRYPTION não pode ser especificado para gatilhos CLR.  
  
 EXECUTE AS  
 Especifica o contexto de segurança no qual o gatilho é executado. Permite controlar a conta de usuário que a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa para validar permissões em quaisquer objetos do banco de dados referidos pelo gatilho.  
  
 Essa opção é necessária para os gatilhos em tabelas com otimização de memória.  
  
 Para obter mais informações, consulte[cláusula EXECUTE AS &#40; Transact-SQL &#41; ](../../t-sql/statements/execute-as-clause-transact-sql.md).  
  
 NATIVE_COMPILATION  
 Indica que o gatilho é compilado nativamente.  
  
 Essa opção é necessária para os gatilhos em tabelas com otimização de memória.  
  
 SCHEMABINDING  
 Garante que as tabelas referenciadas por um gatilho não podem ser descartadas ou alteradas.  
  
 Essa opção é necessária para os gatilhos em tabelas com otimização de memória e não há suporte para gatilhos em tabelas tradicionais.  
  
 FOR | AFTER  
 AFTER especifica que o gatilho DML é disparado apenas quando todas as operações especificadas na instrução SQL de gatilho são executadas com êxito. Todas as verificações de restrição e ações referenciais em cascata também devem obter êxito para que este gatilho seja disparado.  
  
 AFTER é o padrão quando FOR é a única palavra-chave especificada.  
  
 Gatilhos AFTER não podem ser definidos em exibições.  
  
 INSTEAD OF  
 Especifica que o gatilho DML é executado *em vez de* disparar a instrução SQL, portanto, substituindo as ações das instruções de gatilho. INSTEAD OF não pode ser especificado para gatilhos DDL ou de logon.  
  
 No máximo, um gatilho INSTEAD OF por instrução INSERT, UPDATE ou DELETE pode ser definido em uma tabela ou exibição. Entretanto, você pode definir exibições sobre exibições, onde cada uma tem seu próprio gatilho INSTEAD OF.  
  
 Os gatilhos INSTEAD OF não são permitidos em exibições atualizáveis que usam WITH CHECK OPTION. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gera um erro quando um gatilho INSTEAD OF é adicionado a uma WITH CHECK OPTION de exibição atualizável especificado. O usuário deve remover essa opção usando ALTER VIEW antes de definir o gatilho INSTEAD OF.  
  
 {[EXCLUIR] [,] [INSERIR] [,] [ATUALIZAÇÃO]}  
 Especifica as instruções de modificação de dados que, quando tentadas nessa tabela ou exibição, ativam o gatilho DML. É necessário especificar pelo menos uma opção. É permitida qualquer combinação dessas opções em qualquer ordem na definição do gatilho.  
  
 Para gatilhos INSTEAD OF, a opção DELETE não é permitida em tabelas que tenham um relacionamento referencial que especifique uma ação ON DELETE em cascata. Da mesma maneira, a opção UPDATE não é permitida em tabelas que tenham um relacionamento referencial que especifique uma ação ON UPDATE em cascata.  
  
 WITH APPEND  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].  
  
 Especifica que um gatilho adicional de um tipo existente deve ser adicionado. WITH APPEND não pode ser usado com gatilhos INSTEAD OF ou se o gatilho AFTER for explicitamente declarado. WITH APPEND só pode ser usado quando FOR é especificado, sem INSTEAD OF ou AFTER, por razões de compatibilidade com versões anteriores. WITH APPEND não poderá ser especificado se EXTERNAL NAME for especificado (quer dizer, se o gatilho for um gatilho CLR).  
  
 *event_type*  
 É o nome de um evento da linguagem [!INCLUDE[tsql](../../includes/tsql-md.md)] que, após a execução, faz com que um gatilho DDL seja acionado. Os eventos válidos para gatilhos DDL estão listados no [eventos DDL](../../relational-databases/triggers/ddl-events.md).  
  
 *event_group*  
 É o nome de um agrupamento predefinido de eventos da linguagem [!INCLUDE[tsql](../../includes/tsql-md.md)]. O gatilho DDL será acionado após a execução de qualquer [!INCLUDE[tsql](../../includes/tsql-md.md)] evento de linguagem que pertence a *event_group*. Grupos de eventos válidos para gatilhos DDL são listados na [grupos de eventos DDL](../../relational-databases/triggers/ddl-event-groups.md).  
  
 Depois de CREATE TRIGGER concluiu a execução, *event_group* também atuará como uma macro adicionando os tipos de evento abrangidos por ele à exibição de catálogo trigger_events.  
  
 NOT FOR REPLICATION  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Indica que o gatilho não deve ser executado quando um agente de replicação modifica a tabela envolvida no gatilho.  
  
 *sql_statement*  
 São as condições e as ações do gatilho. As condições de gatilho especificam critérios adicionais que determinam se os eventos DML, DDL ou de logon fazem com que as ações de gatilho sejam executadas.  
  
 As ações de gatilho especificadas nas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] entram em vigor quando a operação é tentada.  
  
 Os gatilhos podem incluir qualquer número e tipo de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)], com exceções. Para obter mais informações, consulte Comentários. Um gatilho é criado para verificar ou alterar dados com base em uma instrução de definição ou modificação de dados. Ele não deve retornar dados ao usuário. O [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções em um gatilho frequentemente incluem [linguagem de controle de fluxo](~/t-sql/language-elements/control-of-flow.md).  
  
 Gatilhos DML usam as tabelas de (conceituais) lógicas inseridas e excluídas. Eles são estruturalmente semelhantes à tabela na qual o gatilho é definido, ou seja, a tabela na qual a ação do usuário é tentada. As tabelas inseridas e excluídas mantém os valores antigos ou novos valores das linhas que podem ser alteradas pela ação do usuário. Por exemplo, para recuperar todos os valores na tabela `deleted`, use:  
  
```  
SELECT * FROM deleted;  
```  
  
 Para obter mais informações, consulte [usar as tabelas inseridas e excluídas](../../relational-databases/triggers/use-the-inserted-and-deleted-tables.md).  
  
 Gatilhos DDL e logon capturam informações sobre o evento de disparo usando o [EVENTDATA &#40; Transact-SQL &#41; ](../../t-sql/functions/eventdata-transact-sql.md) função. Para obter mais informações, consulte [usar a função EVENTDATA](../../relational-databases/triggers/use-the-eventdata-function.md).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]permite a atualização de **texto**, **ntext**, ou **imagem** colunas em vez de disparam em tabelas ou exibições.  
  
> [!IMPORTANT]  
>  **ntext**, **texto**, e **imagem** tipos de dados serão removidos em uma versão futura do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar esses tipos de dados em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que os utilizam atualmente. Em vez disso, use [nvarchar(max)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md), [varchar(max)](../../t-sql/data-types/char-and-varchar-transact-sql.md)e [varbinary(max)](../../t-sql/data-types/binary-and-varbinary-transact-sql.md) . Gatilhos AFTER e INSTEAD OF dão suporte **varchar (max)**, **nvarchar (max)**, e **varbinary (max)** dados nas tabelas inseridas e excluídas.  
  
 Para gatilhos em tabelas com otimização de memória, o único *sql_statement* permitido no nível superior é um bloco ATÔMICO. O T-SQL permitido dentro do bloco ATÔMICO é limitado pelo T-SQL permitido dentro de PROC. nativos.  
  
 \<method_specifier > **aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Para um gatilho CLR, especifica o método de associação de um assembly ao gatilho. O método não deve usar nenhum argumento e deve retornar nulo. *class_name* deve ser um válido [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identificador e deve existir como uma classe no assembly com visibilidade do assembly. Se a classe tiver um nome qualificado de namespace que use '.' para separar partes do namespace, o nome da classe deverá ser delimitado com [ ] ou " ". A classe não pode ser aninhada.  
  
> [!NOTE]  
>  Por padrão, a capacidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em executar código CLR está desligada. Você pode criar, modificar e descartar objetos de banco de dados que referenciam módulos de código gerenciado, mas essas referências não serão executadas em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a menos que o [opção clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) é habilitada usando [SP _ configurar](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
## <a name="remarks-dml-triggers"></a>Comentários de gatilhos DML  
 Os gatilhos DML são usados com frequência para impor as regras de negócio e a integridade dos dados. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece DRI (declarative referential integrity, integridade referencial declarativa) por meio das instruções ALTER TABLE e CREATE TABLE. Entretanto, DRI não fornece integridade referencial em todos os bancos de dados. A integridade referencial refere-se às regras sobre as relações entre as chaves primárias e estrangeiras de tabelas. Para impor a integridade referencial, use as restrições PRIMARY KEY e FOREIGN KEY em ALTER TABLE e CREATE TABLE. Se houver restrições na tabela de gatilhos, elas serão verificadas após a execução do gatilho INSTEAD OF e antes da execução do gatilho AFTER. Se as restrições forem violadas, as ações do gatilho INSTEAD OF serão revertidas e o gatilho AFTER não será disparado.  
  
 Os primeiro e o último gatilhos AFTER a serem executados em uma tabela podem ser especificados usando sp_settriggerorder. Somente um primeiro e um último gatilho AFTER para cada operação INSERT, UPDATE e DELETE podem ser especificados em uma tabela. Se houver outros gatilhos AFTER na mesma tabela, eles serão executados aleatoriamente.  
  
 Se uma instrução ALTER TRIGGER alterar um primeiro ou último gatilho, o primeiro ou o último atributo definido no gatilho modificado será descartado e o valor da ordem deverá ser redefinido usando-se sp_settriggerorder.  
  
 Um gatilho AFTER é executado apenas depois que a instrução SQL disparadora for executada com êxito. Essa execução com êxito inclui todas as verificações de restrição e ações referenciais em cascata associadas ao objeto atualizado ou excluído. Um gatilho AFTER não acionará recursivamente um gatilho INSTEAD OF na mesma tabela.  
  
 Se um gatilho INSTEAD OF definido em uma tabela executar uma instrução na tabela que em geral acionaria o gatilho INSTEAD OF novamente, o gatilho não será chamado de forma recorrente. Em vez disso, a instrução será processada como se a tabela não tivesse o gatilho INSTEAD OF e iniciará a cadeia de operações de restrição e de execuções do gatilho AFTER. Por exemplo, se um gatilho for definido como INSTEAD OF INSERT para uma tabela, e o gatilho executar uma instrução INSTEAD OF na mesma tabela, a instrução INSERT executada pelo gatilho INSTEAD OF não chamará o gatilho novamente. A instrução INSERT executada pelo gatilho inicia o processo de efetuar as ações de restrição e acionar todos os gatilhos AFTER INSERT definidos para a tabela.  
  
 Se um gatilho INSTEAD OF definido em uma exibição executar uma instrução na exibição que em geral acionaria o gatilho INSTEAD OF novamente, ele não será chamado de forma recorrente. Pelo contrário, a instrução será solucionada como as modificações nas tabelas de base subjacentes à exibição. Nesse caso, a definição da exibição deve cumprir todas as restrições de uma exibição atualizável. Para uma definição de exibições atualizáveis, consulte [modificar dados por meio de um modo de exibição](../../relational-databases/views/modify-data-through-a-view.md).  
  
 Por exemplo, se um gatilho for definido como INSTEAD OF UPDATE, para uma exibição, e o gatilho executar uma instrução UPDATE referenciando a mesma exibição, a instrução INSERT executada pelo gatilho INSTEAD OF não chamará o gatilho novamente. A instrução UPDATE executada pelo gatilho será processada na exibição como se ela não tivesse um gatilho INSTEAD OF. As colunas alteradas pela UPDATE devem ser solucionadas como uma única tabela base. Toda modificação em uma tabela base subjacente inicia a cadeia de aplicações de restrição, e aciona os gatilhos AFTER INSERT definidos para a tabela.  
  
### <a name="testing-for-update-or-insert-actions-to-specific-columns"></a>Testando as ações UPDATE ou INSERT para colunas específicas  
 É possível criar um gatilho [!INCLUDE[tsql](../../includes/tsql-md.md)] para executar determinadas ações com base em modificações UPDATE ou INSERT para colunas específicas. Use [Update ()](../../t-sql/functions/update-trigger-functions-transact-sql.md) ou [COLUMNS_UPDATED](../../t-sql/functions/columns-updated-transact-sql.md) no corpo do gatilho para essa finalidade. UPDATE() testa as tentativas UPDATE ou INSERT em uma coluna. COLUMNS_UPDATED testa ações UPDATE ou INSERT que são executadas em várias colunas e retorna um padrão de bit que indica quais colunas foram inseridas ou atualizadas.  
  
### <a name="trigger-limitations"></a>Limitações de gatilhos  
 CREATE TRIGGER deve ser a primeira instrução no lote e pode ser aplicada apenas a uma tabela.  
  
 Um gatilho é criado apenas no banco de dados atual; entretanto, ele pode referenciar objetos fora do banco de dados atual.  
  
 Se o nome de esquema do gatilho for especificado para qualificá-lo, qualifique o nome de tabela da mesma maneira.  
  
 A mesma ação de gatilho pode ser definida para mais de uma ação de usuário (por exemplo, INSERT e UPDATE) na mesma instrução CREATE TRIGGER.  
  
 Os gatilhos INSTEAD OF DELETE/UPDATE não podem ser definidos em uma tabela que tenha uma chave estrangeira com uma cascata na ação DELETE/UPDATE definida.  
  
 Qualquer instrução SET pode ser especificada em um gatilho. A opção SET selecionada permanece em vigor durante a execução do gatilho e depois é revertida para sua configuração anterior.  
  
 Quando um gatilho é disparado, os resultados são retornados ao aplicativo de chamada, da mesma forma que com procedimentos armazenados. Para evitar que os resultados sejam retornado ao aplicativo por causa de um gatilho disparado, não inclua instruções SELECT que retornem resultados ou instruções que executem atribuição de variável em um gatilho. Um gatilho que inclua instruções SELECT que retornem resultados ao usuário ou instruções que executam atribuição de variável requer um tratamento especial; os resultados retornados devem ser gravados em todos os aplicativos nos quais as modificações na tabela de gatilhos são permitidas. Se uma atribuição de variável tiver de ocorrer em um gatilho, use a instrução SET NOCOUNT no início do gatilho para evitar o retorno de algum conjunto de resultados.  
  
 Embora a instrução TRUNCATE TABLE seja de fato uma instrução DELETE, ela não ativa um gatilho porque a operação não registra exclusões de linha individuais. Entretanto, somente esses usuários com permissões para executar uma instrução TRUNCATE TABLE precisam se preocupar em evitar inadvertidamente um gatilho DELETE dessa maneira.  
  
 A instrução WRITETEXT, se registrada ou não registrada, não ativa um gatilho.  
  
 As seguintes instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] não são permitidas em um gatilho DML:  
  
||||  
|-|-|-|  
|ALTER DATABASE|CREATE DATABASE|DROP DATABASE|  
|RESTORE DATABASE|RESTORE LOG|RECONFIGURE|  
  
 Além disso, as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir não são permitidas em um gatilho DML usado em uma tabela ou exibição que seja alvo da ação de gatilho.  
  
||||  
|-|-|-|  
|CREATE INDEX (incluindo CREATE SPATIAL INDEX e CREATE XML INDEX)|ALTER INDEX|DROP INDEX|  
|DBCC DBREINDEX|ALTER PARTITION FUNCTION|DROP TABLE|  
|ALTER TABLE quando usado faz o seguinte:<br /><br /> Adiciona, modifica ou descarta colunas.<br /><br /> Alterna partições.<br /><br /> Adiciona ou descarta restrições PRIMARY KEY ou UNIQUE.|||  
  
> [!NOTE]  
>  Como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não oferece suporte a gatilhos definidos pelo usuário em tabelas do sistema, não é recomendável criá-los.  
  
## <a name="remarks-ddl-triggers"></a>Comentários de gatilhos DDL  
 Os gatilhos DDL, assim como os gatilhos padrão, executam procedimentos armazenados em resposta a um evento. Contudo, diferentemente dos gatilhos padrão, eles não são executados em resposta a instruções UPDATE, INSERT ou DELETE em uma tabela ou exibição. Em vez disso, eles são executados em resposta a instruções DDL (linguagem de definição de dados). Isso inclui instruções CREATE, ALTER, DROP, GRANT, DENY, REVOKE e UPDATE STATISTICS. Determinados procedimentos armazenados do sistema que executam operações do tipo DDL também podem disparar gatilhos DDL.  
  
> [!IMPORTANT]  
>  Teste os gatilhos DDL para determinar suas respostas à execução de procedimentos armazenados do sistema. Por exemplo, a instrução CREATE TYPE e o sp_addtype e sp_rename procedimentos armazenados acionarão um gatilho DDL criado em um evento CREATE_TYPE.  
  
 Para obter mais informações sobre gatilhos DDL, consulte [gatilhos DDL](../../relational-databases/triggers/ddl-triggers.md).  
  
 Os gatilhos DDL não são disparados em resposta a eventos que afetem tabelas temporárias locais ou globais e procedimentos armazenados.  
  
 Diferentemente dos gatilhos DML, os gatilhos DDL não têm seu escopo definido para esquemas. Portanto, funções como OBJECT_ID, OBJECT_NAME, OBJECTPROPERTY e OBJECTPROPERTYEX não podem ser usadas para consultar metadados sobre gatilhos DDL. Use as exibições do catálogo em vez disso. Para obter mais informações, consulte [obter informações sobre gatilhos DDL](../../relational-databases/triggers/get-information-about-ddl-triggers.md).  
  
> [!NOTE]  
>  Gatilhos DDL com escopo de servidor aparecem no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] do Pesquisador de **gatilhos** pasta. Essa pasta está localizada na pasta **Server Objects** . Gatilhos DDL com escopo de banco de dados aparecem no **gatilhos de banco de dados** pasta. Essa pasta fica localizada na pasta **Programmability** do banco de dados correspondente.  
  
## <a name="logon-triggers"></a>Gatilhos de logon  
 Os gatilhos de logon executam procedimentos armazenados em resposta a um evento LOGON. Esse evento ocorre quando é estabelecida uma sessão de usuário com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os gatilhos de logon são acionados após o término da fase de autenticação, mas antes da sessão de usuário ser realmente estabelecida. Logo, todas as mensagens originadas no gatilho que chegariam, normalmente, ao usuário, como mensagens de erro e mensagens da instrução PRINT, são desviadas para o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [gatilhos de Logon](../../relational-databases/triggers/logon-triggers.md).  
  
 Os gatilhos de logon não são acionados quando a autenticação falha.  
  
 Não há suporte para transações distribuídas em um gatilho de logon. O erro 3969 é retornado quando um gatilho de logon contendo uma transação distribuída é disparado.  
  
### <a name="disabling-a-logon-trigger"></a>Desabilitando um gatilho de logon  
 Um gatilho de logon pode, efetivamente, impedir conexões com o [!INCLUDE[ssDE](../../includes/ssde-md.md)] para todos os usuários, incluindo membros da função de servidor fixa **sysadmin** . Quando um gatilho de logon está impedindo conexões, os membros da função de servidor fixa **sysadmin** podem se conectar usando a conexão de administrador dedicada ou iniciando o [!INCLUDE[ssDE](../../includes/ssde-md.md)] no modo de configuração mínima (-f). Para obter mais informações, consulte [Database Engine Service Startup Options](../../database-engine/configure-windows/database-engine-service-startup-options.md).  
  
## <a name="general-trigger-considerations"></a>Considerações gerais sobre gatilhos  
  
### <a name="returning-results"></a>Retornando resultados  
 A habilidade de retornar resultados de gatilhos será removida na próxima versão do SQL Server. Os gatilhos que retornam conjuntos de resultados podem causar um comportamento inesperado em aplicativos que não são projetados para trabalhar com eles. Evite retornar conjuntos de resultados de gatilhos em novos trabalhos de desenvolvimento e planeje a modificação de aplicativos que atualmente fazem isso. Para impedir que os gatilhos retornem conjuntos de resultados, defina o [gatilhos opção disallow results from](../../database-engine/configure-windows/disallow-results-from-triggers-server-configuration-option.md) como 1.  
  
 Os gatilhos de logon sempre impedem que conjuntos de resultados sejam retornados e esse comportamento não é configurável. Se um gatilho de logon gerar um conjunto de resultados, o gatilho falhará ao ser executado e a tentativa de logon que o disparou será negada.  
  
### <a name="multiple-triggers"></a>Vários gatilhos  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite que vários gatilhos sejam criados para cada evento DML, DDL ou LOGON. Por exemplo, se CREATE TRIGGER FOR UPDATE for executado para uma tabela que já tenha um gatilho UPDATE, um gatilho update adicional será criado. Nas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], somente um gatilho para cada evento de modificação de dados UPDATE, DELETE ou INSERT é permitido para cada tabela.  
  
### <a name="recursive-triggers"></a>Gatilhos recursivos  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também permite invocação recursiva de gatilhos quando a configuração RECURSIVE_TRIGGERS é habilitada através do uso de ALTER DATABASE.  
  
 Os gatilhos recursivos permitem que os seguintes tipos de recursão ocorram:  
  
-   Recursão indireta  
  
     Com a recursão indireta, um aplicativo atualiza a tabela T1. Isso dispara o gatilho TR1, atualizando a tabela T2. Nesse cenário, o gatilho T2 e é acionado e atualizações da tabela T1.  
  
-   Recursão direta  
  
     Com a recursão direta, as atualizações de aplicativo da tabela T1. Isso dispara o gatilho TR1, atualizando a tabela T1. Porque a tabela T1 foi atualizada, o gatilho TR1 é disparado novamente, e assim por diante.  
  
 O exemplo a seguir usa as duas recursões de gatilho, direta e indireta suponha que dois gatilhos de atualização, TR1 e TR2, são definidos na tabela T1. Gatilho TR1 atualiza a tabela T1 recursivamente. Uma instrução UPDATE executa cada TR1 e TR2 uma vez. Além disso, a execução de TR1 dispara a execução de TR1 (recursivamente) e TR2. As tabelas inseridas e excluídas de um gatilho específico contêm linhas que correspondem somente à instrução UPDATE que invocou o gatilho.  
  
> [!NOTE]  
>  O comportamento anterior só ocorrerá se a configuração RECURSIVE_TRIGGERS for habilitada através do uso de ALTER DATABASE. Não há nenhuma ordem definida na qual vários gatilhos definidos para um evento específico sejam executados. Cada gatilho deve ser autossuficiente.  
  
 Desabilitar a configuração RECURSIVE_TRIGGERS evita apenas recursões diretas. Para desabilitar a recursão indireta também, defina os gatilhos aninhados servidor opção como 0 usando sp_configure.  
  
 Se qualquer um dos gatilhos executar uma ROLLBACK TRANSACTION, independentemente do nível de aninhamento, nenhum outro gatilho será executado.  
  
### <a name="nested-triggers"></a>Gatilhos aninhados  
 Os gatilhos podem ser aninhados até no máximo 32 níveis. Se um gatilho alterar uma tabela na qual haja outro gatilho, o segundo gatilho será ativado e poderá chamar um terceiro gatilho e assim por diante. Se qualquer gatilho na cadeia iniciar um loop infinito, o nível de aninhamento será excedido e o gatilho será cancelado. Quando um gatilho [!INCLUDE[tsql](../../includes/tsql-md.md)] executa um código gerenciado fazendo referência a uma rotina, tipo ou agregação CLR, essa referência também conta como um nível no limite de aninhamento de nível 32. Os métodos invocados do código gerenciado não contam em relação a esse limite.  
  
 Para desabilitar gatilhos aninhados, defina a opção nested triggers de sp_configure para 0 (desativado). A configuração padrão permite gatilhos aninhados. Se os gatilhos aninhados estiverem desativados, os gatilhos recursivos também serão desabilitados, independentemente da configuração RECURSIVE_TRIGGERS definida através do uso de ALTER DATABASE.  
  
 O primeiro gatilho AFTER aninhado dentro de um INSTEAD OF o gatilho é disparado mesmo se o **gatilhos aninhados** opção de configuração do servidor é definida como 0. Porém, nessa configuração, os gatilhos AFTER posteriores não são disparados. Recomendamos que você examine seus aplicativos para gatilhos aninhados para determinar se os aplicativos estão em conformidade com as regras de negócio em relação a esse comportamento quando o **gatilhos aninhados** opção de configuração do servidor é definida como 0, e, em seguida, faça as modificações apropriadas.  
  
### <a name="deferred-name-resolution"></a>Resolução de nome adiada  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite que procedimentos armazenados, gatilhos e lotes [!INCLUDE[tsql](../../includes/tsql-md.md)] referenciem tabelas que não existem em tempo de compilação. Essa capacidade é chamada de resolução de nome adiada.  
  
## <a name="permissions"></a>Permissões  
 A criação de um gatilho DML requer a permissão ALTER na tabela ou exibição na qual o gatilho é criado.  
  
 A criação de um gatilho DDL com escopo no servidor (ON ALL SERVER) ou um gatilho de logon requer a permissão CONTROL SERVER no servidor. A criação de um gatilho DDL com escopo no banco de dados (ON DATABASE) requer a permissão ALTER ANY DATABASE DDL TRIGGER no banco de dados atual.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-a-dml-trigger-with-a-reminder-message"></a>A. Usando um gatilho DML com uma mensagem de lembrete  
 O gatilho DML a seguir imprime uma mensagem para o cliente quando alguém tenta adicionar ou alterar dados na tabela `Customer` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
CREATE TRIGGER reminder1  
ON Sales.Customer  
AFTER INSERT, UPDATE   
AS RAISERROR ('Notify Customer Relations', 16, 10);  
GO  
```  
  
### <a name="b-using-a-dml-trigger-with-a-reminder-e-mail-message"></a>B. Usando um gatilho DML com uma mensagem de email de lembrete  
 O exemplo a seguir envia uma mensagem de email a uma pessoa especificada (`MaryM`) quando a tabela `Customer` é alterada.  
  
```  
CREATE TRIGGER reminder2  
ON Sales.Customer  
AFTER INSERT, UPDATE, DELETE   
AS  
   EXEC msdb.dbo.sp_send_dbmail  
        @profile_name = 'AdventureWorks2012 Administrator',  
        @recipients = 'danw@Adventure-Works.com',  
        @body = 'Don''t forget to print a report for the sales force.',  
        @subject = 'Reminder';  
GO  
```  
  
### <a name="c-using-a-dml-after-trigger-to-enforce-a-business-rule-between-the-purchaseorderheader-and-vendor-tables"></a>C. Usando um gatilho DML AFTER para impor uma regra de negócio entre as tabelas PurchaseOrderHeader e Vendor  
 Como as restrições CHECK só podem referenciar as colunas nas quais a restrição de nível de coluna ou de nível de tabela é definida, qualquer restrição de tabela cruzada (neste caso, as regras de negócio) deverá ser definida como gatilho.  
  
 O exemplo a seguir cria um gatilho DML no banco de dados AdventureWorks2012. Esse gatilho verifica se a avaliação de crédito para o fornecedor é satisfatória (não 5) quando é feita uma tentativa para inserir uma nova ordem de compra para o `PurchaseOrderHeader` tabela. Para obter a classificação de crédito do fornecedor, a tabela `Vendor` deve ser referenciada. Se a classificação de crédito for muito baixa, uma mensagem será exibida e a inserção não será executada.  
  
```  
-- This trigger prevents a row from being inserted in the Purchasing.PurchaseOrderHeader 
-- table when the credit rating of the specified vendor is set to 5 (below average).  
  
CREATE TRIGGER Purchasing.LowCredit ON Purchasing.PurchaseOrderHeader  
AFTER INSERT  
AS  
IF EXISTS (SELECT *  
           FROM Purchasing.PurchaseOrderHeader AS p   
           JOIN inserted AS i   
           ON p.PurchaseOrderID = i.PurchaseOrderID   
           JOIN Purchasing.Vendor AS v   
           ON v.BusinessEntityID = p.VendorID  
           WHERE v.CreditRating = 5  
          )  
BEGIN  
RAISERROR ('A vendor''s credit rating is too low to accept new  
purchase orders.', 16, 1);  
ROLLBACK TRANSACTION;  
RETURN   
END;  
GO  
  
-- This statement attempts to insert a row into the PurchaseOrderHeader table  
-- for a vendor that has a below average credit rating.  
-- The AFTER INSERT trigger is fired and the INSERT transaction is rolled back.  
  
INSERT INTO Purchasing.PurchaseOrderHeader (RevisionNumber, Status, EmployeeID,  
VendorID, ShipMethodID, OrderDate, ShipDate, SubTotal, TaxAmt, Freight)  
VALUES (  
2  
,3  
,261  
,1652  
,4  
,GETDATE()  
,GETDATE()  
,44594.55  
,3567.564  
,1114.8638 );  
GO  
  
```  
  
### <a name="d-using-a-database-scoped-ddl-trigger"></a>D. Usando um gatilho DDL no escopo do banco de dados  
 O exemplo a seguir usa um gatilho DDL para evitar que qualquer sinônimo em um banco de dados seja descartado.  
  
```  
CREATE TRIGGER safety   
ON DATABASE   
FOR DROP_SYNONYM  
AS   
   RAISERROR ('You must disable Trigger "safety" to drop synonyms!',10, 1)  
   ROLLBACK  
GO  
DROP TRIGGER safety  
ON DATABASE;  
GO  
```  
  
### <a name="e-using-a-server-scoped-ddl-trigger"></a>E. Usando um gatilho DDL no escopo do servidor  
 O exemplo a seguir usa um gatilho DDL para imprimir uma mensagem se qualquer evento CREATE DATABASE ocorrer na instância do servidor atual e usa a função `EVENTDATA` para recuperar o texto da instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] correspondente. Para obter mais exemplos que usam EVENTDATA em gatilhos DDL, consulte [usar a função EVENTDATA](../../relational-databases/triggers/use-the-eventdata-function.md).  
  
**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
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
  
### <a name="f-using-a-logon-trigger"></a>F. Usando um gatilho de logon  
 O exemplo de gatilho de logon a seguir nega uma tentativa de fazer logon no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como um membro do *login_test* logon se já houver três sessões de usuário em execução em que o logon.  
  
**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
USE master;  
GO  
CREATE LOGIN login_test WITH PASSWORD = '3KHJ6dhx(0xVYsdf' MUST_CHANGE,  
    CHECK_EXPIRATION = ON;  
GO  
GRANT VIEW SERVER STATE TO login_test;  
GO  
CREATE TRIGGER connection_limit_trigger  
ON ALL SERVER WITH EXECUTE AS 'login_test'  
FOR LOGON  
AS  
BEGIN  
IF ORIGINAL_LOGIN()= 'login_test' AND  
    (SELECT COUNT(*) FROM sys.dm_exec_sessions  
            WHERE is_user_process = 1 AND  
                original_login_name = 'login_test') > 3  
    ROLLBACK;  
END;  
  
```  
  
### <a name="g-viewing-the-events-that-cause-a-trigger-to-fire"></a>G. Exibindo os eventos que fazem um gatilho ser acionado  
 O exemplo a seguir consulta as exibições do catálogo `sys.triggers` e `sys.trigger_events` para determinar quais eventos de linguagem [!INCLUDE[tsql](../../includes/tsql-md.md)] fazem o gatilho `safety` ser acionado. `safety` é criado no exemplo anterior.  
  
```  
SELECT TE.*  
FROM sys.trigger_events AS TE  
JOIN sys.triggers AS T ON T.object_id = TE.object_id  
WHERE T.parent_class = 0 AND T.name = 'safety';  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [COLUMNS_UPDATED &#40; Transact-SQL &#41;](../../t-sql/functions/columns-updated-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [ENABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/enable-trigger-transact-sql.md)   
 [DISABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/disable-trigger-transact-sql.md)   
 [TRIGGER_NESTLEVEL &#40; Transact-SQL &#41;](../../t-sql/functions/trigger-nestlevel-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)   
 [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)   
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptrigger &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptrigger-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [sp_settriggerorder &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-settriggerorder-transact-sql.md)   
 [Atualizar &#40; &#41; &#40; Transact-SQL &#41;](../../t-sql/functions/update-trigger-functions-transact-sql.md)   
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
  
  



