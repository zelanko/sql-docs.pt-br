---
title: CREATE TRIGGER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: mathoma
ms.technology: t-sql
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
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 737f337369b04c59d34bb8ab4335a2491e843927
ms.sourcegitcommit: a13256f484eee2f52c812646cc989eb0ce6cf6aa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/25/2019
ms.locfileid: "56802392"
---
# <a name="create-trigger-transact-sql"></a>CREATE TRIGGER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]


Cria um gatilho DML, DDL ou de logon. Um gatilho é um tipo especial de procedimento armazenado executado automaticamente quando um evento ocorre no servidor de banco de dados. Os gatilhos DML são executados quando um usuário tenta modificar dados por meio de um evento DML (linguagem de manipulação de dados). Os eventos DML são instruções INSERT, UPDATE ou DELETE em uma tabela ou exibição. Esses gatilhos são disparados quando qualquer evento válido é acionado, sejam as linhas da tabela afetadas ou não. Para obter mais informações, consulte [DML Triggers](../../relational-databases/triggers/dml-triggers.md).  
  
Os gatilhos DDL são executados em resposta a diversos eventos DDL (linguagem de definição de dados). Esses eventos correspondem, basicamente, a instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE, ALTER e DROP e determinados procedimentos armazenados do sistema que executam operações do tipo DDL. 

Os gatilhos de logon são disparados em resposta ao evento LOGON gerado quando a sessão de um usuário está sendo estabelecida. Crie gatilhos diretamente de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] ou de métodos de assemblies criados no CLR (Common Language Runtime) do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e carregados em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite criar vários gatilhos para qualquer instrução específica.  
  
> [!IMPORTANT]  
>  Um código mal-intencionado dentro de gatilhos pode ser executado sob privilégios escalonados. Para obter mais informações sobre como reduzir essa ameaça, veja [Gerenciar segurança do gatilho](../../relational-databases/triggers/manage-trigger-security.md).  
  
> [!NOTE]  
>  A integração do CLR do .NET Framework ao SQL Server é discutida neste artigo. A integração CLR não se aplica ao Banco de Dados SQL do Azure.  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
-- Azure SQL Database Syntax   
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
-- Azure SQL Database Syntax  
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
OR ALTER  
**Aplica-se ao**: Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando pelo [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1). 
  
Altera condicionalmente o gatilho somente se ele já existir. 
  
*schema_name*  
O nome do esquema ao qual o gatilho DML pertence. Os gatilhos DML são definidos no escopo do esquema da tabela ou na exibição em que são criados. *schema_name* não pode ser especificado para gatilhos DDL ou de logon.  
  
*trigger_name*  
O nome do gatilho. Um *nome_do_gatilho* deve seguir as regras de [identificadores](../../relational-databases/databases/database-identifiers.md), exceto que *nome_do_gatilho* não pode começar com # nem ##.  
  
*table* | *view*  
A tabela ou a exibição em que o gatilho DML é executado. Essa tabela ou exibição às vezes é referenciada como tabela de gatilho ou exibição de gatilho. Especificar o nome totalmente qualificado da tabela ou da exibição é opcional. Só é possível referenciar uma exibição por um gatilho INSTEAD OF. Não é possível definir gatilhos DML em tabelas temporárias locais ou globais.  
  
DATABASE  
Aplica o escopo de um gatilho DDL ao banco de dados atual. Se especificado, o gatilho será disparado sempre que *event_type* ou *event_group* ocorrer no banco de dados atual.  
  
ALL SERVER  
**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
Aplica o escopo de um gatilho DDL ou de logon ao servidor atual. Se for especificado, o gatilho será disparado sempre que *event_type* ou *event_group* ocorrer em qualquer local no servidor atual.  
  
WITH ENCRYPTION  
**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
Obscurece o texto da instrução CREATE TRIGGER. O uso de WITH ENCRYPTION impede que o gatilho seja publicado como parte da replicação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. WITH ENCRYPTION não pode ser especificado para gatilhos CLR.  
  
EXECUTE AS  
Especifica o contexto de segurança no qual o gatilho é executado. Permite controlar a conta de usuário que a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa para validar permissões em quaisquer objetos do banco de dados referidos pelo gatilho.  
  
Essa opção é necessária para os gatilhos em tabelas com otimização de memória.  
  
Para obter mais informações, veja [Cláusula EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md).  
  
NATIVE_COMPILATION  
Indica que o gatilho foi compilado nativamente.  
  
Essa opção é necessária para os gatilhos em tabelas com otimização de memória.  
  
SCHEMABINDING  
Garante que as tabelas referenciadas por um gatilho não possam ser removidas nem alteradas.  
  
Essa opção é obrigatória para gatilhos em tabelas com otimização de memória e não é compatível com gatilhos em tabelas tradicionais.  
  
FOR | AFTER  
AFTER especifica que o gatilho DML é disparado apenas quando todas as operações especificadas na instrução SQL de gatilho são iniciadas com êxito. Todas as verificações de restrição e ações referenciais em cascata também devem ter êxito para que esse gatilho seja disparado.  
  
AFTER é o padrão quando FOR é a única palavra-chave especificada.  
  
Não é possível definir gatilhos AFTER em exibições.  
  
INSTEAD OF  
Especifica que o gatilho DML será iniciado *em vez da* instrução SQL de gatilho, substituindo as ações das instruções de gatilho. Não é possível especificar INSTEAD OF para gatilhos DDL ou de logon.  
  
No máximo, você pode definir um gatilho INSTEAD OF por instrução INSERT, UPDATE ou DELETE em uma tabela ou exibição. Também pode definir exibições sobre exibições, onde cada uma tem seu próprio gatilho INSTEAD OF.  
  
Não é possível definir gatilhos INSTEAD OF em exibições atualizáveis que usam WITH CHECK OPTION. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Fazer isso gera um erro quando um gatilho INSTEAD OF é adicionado a uma WITH CHECK OPTION de exibição atualizável especificada. Remova essa opção usando ALTER VIEW antes de definir o gatilho INSTEAD OF.  
  
{ [ DELETE ] [ , ] [ INSERT ] [ , ] [ UPDATE ] }  
Especifica as instruções de modificação de dados que, quando tentadas nessa tabela ou exibição, ativam o gatilho DML. Especifique pelo menos uma opção. Use qualquer combinação dessas opções em qualquer ordem na definição do gatilho.  
  
Para gatilhos INSTEAD OF, a opção DELETE não é permitida em tabelas que tenham um relacionamento referencial que especifique uma ação ON DELETE em cascata. Da mesma maneira, a opção UPDATE não é permitida em tabelas que tenham um relacionamento referencial que especifique uma ação ON UPDATE em cascata.  
  
WITH APPEND  
**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].  
  
Especifica que um gatilho adicional de um tipo existente deve ser adicionado. WITH APPEND não poderá ser usado com gatilhos INSTEAD OF ou se o gatilho AFTER for explicitamente declarado. Por razões de compatibilidade com versões anteriores, WITH APPEND só pode ser usado quando FOR é especificado, sem INSTEAD OF ou AFTER. Não será possível especificar WITH APPEND se EXTERNAL NAME for usado (ou seja, se o gatilho for um gatilho CLR).  
  
*event_type*  
O nome de um evento da linguagem [!INCLUDE[tsql](../../includes/tsql-md.md)] que, após a inicialização, faz com que um gatilho DDL seja acionado. Os eventos válidos para gatilhos DDL são listados em [Eventos DDL](../../relational-databases/triggers/ddl-events.md).  
  
*event_group*  
O nome de um agrupamento predefinido de eventos da linguagem [!INCLUDE[tsql](../../includes/tsql-md.md)]. O gatilho DDL é disparado após a inicialização de qualquer evento de linguagem do [!INCLUDE[tsql](../../includes/tsql-md.md)] que pertence a *event_group*. Os grupos de eventos válidos para gatilhos DDL são listados em [Grupos de eventos DDL](../../relational-databases/triggers/ddl-event-groups.md).  
  
Depois que a execução de CREATE TRIGGER for concluída, o *event_group* também atuará como uma macro pela adição dos tipos de evento abrangidos por ele à exibição do catálogo sys.trigger_events.  
  
NOT FOR REPLICATION  
**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
Indica que o gatilho não deve ser executado quando um agente de replicação modifica a tabela envolvida no gatilho.  
  
*sql_statement*  
As condições e as ações do gatilho. As condições de gatilho especificam critérios adicionais que determinam se os eventos DML, DDL ou de logon fazem com que as ações de gatilho sejam executadas.  
  
As ações de gatilho especificadas nas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] entram em vigor quando a operação é tentada.  
  
Os gatilhos podem incluir qualquer número e tipo de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)], com exceções. Para obter mais informações, consulte Comentários. Um gatilho é criado para verificar ou alterar dados com base em uma instrução de definição ou modificação de dados. Ele não deve retornar dados ao usuário. As instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] em um gatilho frequentemente incluem [linguagem de controle de fluxo](~/t-sql/language-elements/control-of-flow.md).  
  
Gatilhos de DML usam as tabelas (conceituais) lógicas inseridas e excluídas. Eles são estruturalmente semelhantes à tabela em que o gatilho é definido, ou seja, a tabela em que a ação do usuário é tentada. As tabelas excluídas e inseridas contêm os valores antigos ou novos das linhas que podem ser alteradas pela ação do usuário. Por exemplo, para recuperar todos os valores na tabela `deleted`, use:  
  
```sql  
SELECT * FROM deleted;  
```  
  
Para obter mais informações, veja [Usar as tabelas inseridas e excluídas](../../relational-databases/triggers/use-the-inserted-and-deleted-tables.md).  
  
Gatilhos DDL e logon capturam informações sobre o evento de gatilho usando a função [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md). Para obter mais informações, veja [Usar a função EVENTDATA](../../relational-databases/triggers/use-the-eventdata-function.md).  
  
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite a atualização das colunas **text**, **ntext** ou **image** por meio do gatilho INSTEAD OF em tabelas ou exibições.  
  
> [!IMPORTANT]
>  Os tipos de dados **ntext**, **text** e **image** serão removidos em uma versão futura do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar esses tipos de dados em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que os utilizam atualmente. Em vez disso, use [nvarchar(max)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md), [varchar(max)](../../t-sql/data-types/char-and-varchar-transact-sql.md)e [varbinary(max)](../../t-sql/data-types/binary-and-varbinary-transact-sql.md) . Os gatilhos AFTER e INSTEAD OF dão ambos suporte a dados **varchar(MAX)**, **nvarchar(MAX)** e **varbinary(MAX)** nas tabelas inseridas e excluídas.  
  
Para gatilhos em tabelas com otimização de memória, a única *sql_statement* permitida no nível superior é um bloco ATOMIC. O T-SQL permitido dentro do bloco ATOMIC é limitado pelo T-SQL permitido dentro de procedimentos nativos.  
  
\< method_specifier > **Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
Para um gatilho CLR, especifica o método de associação de um assembly ao gatilho. O método não deve usar nenhum argumento e deve retornar nulo. *class_name* deve ser um identificador válido do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e deve existir como uma classe no assembly com visibilidade do assembly. Se a classe tiver um nome qualificado de namespace que use '.' para separar partes do namespace, o nome da classe deverá ser delimitado com [ ] ou " ". A classe não pode ser aninhada.  
  
> [!NOTE]  
>  Por padrão, a capacidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em executar código CLR está desligada. Você pode criar, modificar e remover objetos do banco de dados que referenciam módulos de código gerenciado, mas essas referências não são executadas em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a menos que a [Opção clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) seja habilitada usando [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
## <a name="remarks-for-dml-triggers"></a>Comentários para gatilhos DML  
Os gatilhos DML são usados com frequência para impor as regras de negócio e a integridade dos dados. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece DRI (declarative referential integrity, integridade referencial declarativa) por meio das instruções ALTER TABLE e CREATE TABLE. Entretanto, DRI não fornece integridade referencial em todos os bancos de dados. A integridade referencial refere-se às regras sobre as relações entre as chaves primárias e estrangeiras de tabelas. Para impor a integridade referencial, use as restrições PRIMARY KEY e FOREIGN KEY em ALTER TABLE e CREATE TABLE. Se houver restrições na tabela de gatilhos, elas serão verificadas após a execução do gatilho INSTEAD OF e antes da execução do gatilho AFTER. Se as restrições forem violadas, as ações do gatilho INSTEAD OF serão revertidas e o gatilho AFTER não será disparado.  
  
É possível especificar o primeiro e o último gatilhos AFTER a serem executados em uma tabela usando sp_settriggerorder. Só é possível especificar um primeiro e um último gatilho AFTER para cada operação INSERT, UPDATE e DELETE em uma tabela. Se houver outros gatilhos AFTER na mesma tabela, eles serão executados aleatoriamente.  
  
Se uma instrução ALTER TRIGGER alterar um primeiro ou último gatilho, o primeiro ou o último atributo definido no gatilho modificado será descartado, e você terá que redefinir o valor da ordem usando sp_settriggerorder.  
  
Um gatilho AFTER é executado apenas depois que a instrução SQL disparadora é executada com êxito. Essa execução com êxito inclui todas as verificações de restrição e ações referenciais em cascata associadas ao objeto atualizado ou excluído. Um gatilho AFTER não aciona recursivamente um gatilho INSTEAD OF na mesma tabela.  
  
Se um gatilho INSTEAD OF definido em uma tabela executar uma instrução na tabela que em geral acionaria o gatilho INSTEAD OF novamente, o gatilho não será chamado de forma recorrente. Em vez disso, a instrução será processada como se a tabela não tivesse o gatilho INSTEAD OF e iniciará a cadeia de operações de restrição e de execuções do gatilho AFTER. Por exemplo, se um gatilho for definido como um gatilho INSTEAD OF INSERT para uma tabela. E o gatilho executar uma instrução INSTEAD OF na mesma tabela, a instrução INSERT iniciada pelo gatilho INSTEAD OF não chamará o gatilho novamente. A instrução INSERT iniciada pelo gatilho inicia o processo de execução de ações de restrição e acionamento de todos os gatilhos AFTER INSERT definidos para a tabela.  
  
Quando um gatilho INSTEAD OF definido em uma exibição executa uma instrução na exibição que em geral acionaria o gatilho INSTEAD OF novamente, ele não é chamado de forma recorrente. Pelo contrário, a instrução será solucionada como as modificações nas tabelas de base subjacentes à exibição. Nesse caso, a definição da exibição deve cumprir todas as restrições de uma exibição atualizável. Para uma definição de exibições atualizáveis, veja [Modificar dados por meio de uma exibição](../../relational-databases/views/modify-data-through-a-view.md).  
  
Por exemplo, se um gatilho for definido como um gatilho INSTEAD OF UPDATE para uma exibição. E o gatilho executar uma instrução UPDATE referenciando a mesma exibição, a instrução UPDATE iniciada pelo gatilho INSTEAD OF não chamará o gatilho novamente. A instrução UPDATE iniciada pelo gatilho será processada na exibição como se ela não tivesse um gatilho INSTEAD OF. As colunas alteradas pela UPDATE devem ser solucionadas como uma única tabela base. Toda modificação em uma tabela base subjacente inicia a cadeia de aplicações de restrição, e aciona os gatilhos AFTER INSERT definidos para a tabela.  
  
### <a name="testing-for-update-or-insert-actions-to-specific-columns"></a>Testando as ações UPDATE ou INSERT para colunas específicas  
É possível criar um gatilho [!INCLUDE[tsql](../../includes/tsql-md.md)] para executar determinadas ações com base em modificações UPDATE ou INSERT para colunas específicas. Use [UPDATE()](../../t-sql/functions/update-trigger-functions-transact-sql.md) ou [COLUMNS_UPDATED](../../t-sql/functions/columns-updated-transact-sql.md) no corpo do gatilho para esse fim. UPDATE() testa as tentativas UPDATE ou INSERT em uma coluna. COLUMNS_UPDATED testa para UPDATE ou INSERT as ações executadas em colunas várias. Essa função retorna um padrão de bits que indica quais colunas foram inseridas ou atualizadas.  
  
### <a name="trigger-limitations"></a>Limitações de gatilhos  
CREATE TRIGGER deve ser a primeira instrução no lote e pode ser aplicada apenas a uma tabela.  
  
Um gatilho é criado apenas no banco de dados atual; entretanto, ele pode referenciar objetos fora do banco de dados atual.  
  
Se o nome de esquema do gatilho for especificado para qualificá-lo, qualifique o nome de tabela da mesma maneira.  
  
A mesma ação de gatilho pode ser definida para mais de uma ação de usuário (por exemplo, INSERT e UPDATE) na mesma instrução CREATE TRIGGER.  
  
Os gatilhos INSTEAD OF DELETE/UPDATE não podem ser definidos em uma tabela que tenha uma chave estrangeira com uma cascata na ação DELETE/UPDATE definida.  
  
Qualquer instrução SET pode ser especificada em um gatilho. A opção SET selecionada permanece em vigor durante a execução do gatilho e depois é revertida para sua configuração anterior.  
  
Quando um gatilho é disparado, os resultados são retornados ao aplicativo de chamada, da mesma forma que com procedimentos armazenados. Para evitar que os resultados sejam retornados ao aplicativo devido a um gatilho disparado, não inclua instruções SELECT que retornem resultados ou instruções que executem atribuição de variável em um gatilho. Um gatilho que inclua instruções SELECT que retornem resultados ao usuário ou instruções que realizem atribuição de variável requer um tratamento especial. Você teria que gravar os resultados retornados em cada aplicativo, para os quais são permitidas modificações na tabela do gatilho. Se uma atribuição de variável tiver de ocorrer em um gatilho, use a instrução SET NOCOUNT no início do gatilho para evitar o retorno de algum conjunto de resultados.  
  
Embora a instrução TRUNCATE TABLE seja de fato uma instrução DELETE, ela não ativa um gatilho porque a operação não registra exclusões de linha individuais. Entretanto, somente usuários com permissões para executar uma instrução TRUNCATE TABLE precisam se preocupar em evitar inadvertidamente um gatilho DELETE dessa maneira.  
  
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

### <a name="optimizing-dml-triggers"></a>Otimizando gatilhos DML
Os gatilhos funcionam em transações (implícitas ou não) e, enquanto estiverem abertos, bloquearão recursos. O bloqueio permanecerá em vigor até que a transação seja confirmada (com COMMIT) ou rejeitada (com um ROLLBACK). Quanto mais um gatilho é executado, maior a probabilidade de outro processo ser bloqueado. Portanto, escreva gatilhos para diminuir a duração deles sempre que possível. Uma maneira de alcançar uma duração mais curta é liberar um gatilho quando uma instrução DML altera zero linha. 

Para liberar o gatilho para um comando que não altera nenhuma linha, empregue a variável de sistema [ROWCOUNT_BIG](../functions/rowcount-big-transact-sql.md). 

O seguinte trecho de código T-SQL mostra como liberar o gatilho para um comando que não altera nenhuma linha. Esse código deverá estar presente no início de cada gatilho DML:

```sql
IF (ROWCOUNT_BIG() = 0)
RETURN;
```
  
  
## <a name="remarks-for-ddl-triggers"></a>Comentários para gatilhos DDL  
Os gatilhos DDL, assim como os gatilhos padrão, iniciam procedimentos armazenados em resposta a um evento. Contudo, diferentemente dos gatilhos padrão, eles não são executados em resposta a instruções UPDATE, INSERT ou DELETE em uma tabela ou exibição. Em vez disso, eles são executados em resposta a instruções DDL (linguagem de definição de dados). Os tipos de instrução incluem CREATE, ALTER, DROP, GRANT, DENY, REVOKE e UPDATE STATISTICS. Determinados procedimentos armazenados do sistema que executam operações do tipo DDL também podem disparar gatilhos DDL.  
  
> [!IMPORTANT]  
>  Teste os gatilhos DDL para determinar suas respostas à execução de procedimentos armazenados do sistema. Por exemplo, a instrução CREATE TYPE e os procedimentos armazenados sp_addtype e sp_rename disparam um gatilho DDL que é criado em um evento CREATE_TYPE.  
  
Para obter mais informações sobre gatilhos DDL, veja [Gatilhos DDL](../../relational-databases/triggers/ddl-triggers.md).  
  
Os gatilhos DDL não são disparados em resposta a eventos que afetem tabelas temporárias locais ou globais e procedimentos armazenados.  
  
Diferentemente dos gatilhos DML, os gatilhos DDL não têm seu escopo definido para esquemas. Portanto, não é possível usar funções como OBJECT_ID, OBJECT_NAME, OBJECTPROPERTY e OBJECTPROPERTYEX para consultar metadados sobre gatilhos DDL. Use as exibições do catálogo em vez disso. Para obter mais informações, veja [Obter informações sobre gatilhos DDL](../../relational-databases/triggers/get-information-about-ddl-triggers.md).  
  
> [!NOTE]  
>  Gatilhos DDL no escopo do servidor aparecem no Pesquisador de Objetos do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] na pasta **Gatilhos**. Essa pasta está localizada na pasta **Server Objects** . Gatilhos DDL no escopo do banco de dados aparecem na pasta **Gatilhos de Banco de Dados**. Essa pasta fica localizada na pasta **Programmability** do banco de dados correspondente.  
  
## <a name="logon-triggers"></a>Gatilhos de logon  
Os gatilhos de logon realizam procedimentos armazenados em resposta a um evento LOGON. Esse evento ocorre quando é estabelecida uma sessão de usuário com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os gatilhos de logon são acionados após o término da fase de autenticação, mas antes da sessão de usuário ser estabelecida. Portanto, todas as mensagens originadas no gatilho que chegariam, normalmente, ao usuário, como mensagens de erro e mensagens da instrução PRINT, são desviadas para o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, veja [Gatilhos de logon](../../relational-databases/triggers/logon-triggers.md).  
  
Os gatilhos de logon não são acionados quando a autenticação falha.  
  
Não há suporte para transações distribuídas em um gatilho de logon. O erro 3969 é retornado quando é disparado um gatilho de logon que contém uma transação distribuída.  
  
### <a name="disabling-a-logon-trigger"></a>Desabilitando um gatilho de logon  
Um gatilho de logon pode, efetivamente, impedir conexões com o [!INCLUDE[ssDE](../../includes/ssde-md.md)] para todos os usuários, incluindo membros da função de servidor fixa **sysadmin** . Quando um gatilho de logon está impedindo conexões, os membros da função de servidor fixa **sysadmin** podem se conectar usando a conexão de administrador dedicada ou iniciando o [!INCLUDE[ssDE](../../includes/ssde-md.md)] no modo de configuração mínima (-f). Para obter mais informações, consulte [Opções de inicialização do serviço Mecanismo de Banco de Dados](../../database-engine/configure-windows/database-engine-service-startup-options.md).  
  
## <a name="general-trigger-considerations"></a>Considerações gerais sobre gatilhos  
  
### <a name="returning-results"></a>Retornando resultados  
A habilidade de retornar resultados de gatilhos será removida na próxima versão do SQL Server. Os gatilhos que retornam conjuntos de resultados podem causar um comportamento inesperado em aplicativos que não são projetados para trabalhar com eles. Evite retornar conjuntos de resultados de gatilhos em novos trabalhos de desenvolvimento e planeje a modificação de aplicativos que atualmente fazem. Para evitar que os gatilhos retornem conjuntos de resultados, defina a opção [proibir resultados de gatilhos](../../database-engine/configure-windows/disallow-results-from-triggers-server-configuration-option.md) como 1.  
  
Os gatilhos de logon sempre impedem o retorno de conjuntos de resultados, e esse comportamento não é configurável. Se um gatilho de logon gerar um conjunto de resultados, o gatilho falhará ao ser iniciado e a tentativa de logon que o disparou será negada.  
  
### <a name="multiple-triggers"></a>Vários gatilhos  
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite a criação de vários gatilhos para cada evento DML, DDL ou LOGON. Por exemplo, se CREATE TRIGGER FOR UPDATE for executado para uma tabela que já tenha um gatilho UPDATE, um gatilho update adicional será criado. Nas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], somente um gatilho para cada evento de modificação de dados UPDATE, DELETE ou INSERT é permitido para cada tabela.  
  
### <a name="recursive-triggers"></a>Gatilhos recursivos  
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também oferece suporte à invocação recursiva de gatilhos quando a configuração RECURSIVE_TRIGGERS é habilitada por meio do uso de ALTER DATABASE.  
  
Os gatilhos recursivos permitem que os seguintes tipos de recursão ocorram:  
  
-   Recursão indireta  
  
     Com a recursão indireta, um aplicativo atualiza a tabela T1. Isso dispara o gatilho TR1, atualizando a tabela T2. O gatilho T2 é disparado e atualiza a tabela T1.  
  
-   Recursão direta  
  
     Na recursão direta, o aplicativo atualiza a tabela T1. Isso dispara o gatilho TR1, atualizando a tabela T1. Uma vez que a tabela T1 foi atualizada, o gatilho TR1 é disparado novamente e assim por diante.  
  
O exemplo a seguir usa as duas recursões de gatilho, direta e indireta. Suponha que dois gatilhos de atualização, TR1 e TR2, sejam definidos na tabela T1. O gatilho TR1 atualiza a tabela T1 recursivamente. Uma instrução UPDATE executa TR1 e TR2 uma vez. Além disso, a execução de TR1 inicia a execução de TR1 (recursivamente) e de TR2. As tabelas inseridas e excluídas para um gatilho específico contêm linhas que correspondem somente à instrução UPDATE que invocou o gatilho.  
  
> [!NOTE]  
>  O comportamento anterior só ocorrerá se a configuração RECURSIVE_TRIGGERS for habilitada através do uso de ALTER DATABASE. Não há nenhuma ordem definida na qual vários gatilhos definidos para um evento específico sejam executados. Cada gatilho deve ser autossuficiente.  
  
Desabilitar a configuração RECURSIVE_TRIGGERS evita apenas recursões diretas. Para desabilitar a recursão indireta também, defina a opção de servidor de gatilhos aninhados como 0 usando sp_configure.  
  
Se qualquer um dos gatilhos executar uma ROLLBACK TRANSACTION, independentemente do nível de aninhamento, nenhum outro gatilho será executado.  
  
### <a name="nested-triggers"></a>Gatilhos aninhados  
É possível aninhar até no máximo 32 níveis. Se um gatilho alterar uma tabela em que haja outro gatilho, o segundo gatilho será ativado e poderá chamar um terceiro gatilho e assim por diante. Se qualquer gatilho na cadeia iniciar um loop infinito, o nível de aninhamento será excedido e o gatilho será cancelado. Quando um gatilho [!INCLUDE[tsql](../../includes/tsql-md.md)] inicia um código gerenciado fazendo referência a uma rotina, tipo ou agregação CLR, essa referência também conta como um nível no limite de aninhamento de nível 32. Os métodos invocados a partir do código gerenciado não são contados em relação a esse limite.  
  
Para desabilitar gatilhos aninhados, defina a opção de gatilhos aninhados de sp_configure como 0 (desativada). A configuração padrão oferece suporte a gatilhos aninhados. Se os gatilhos aninhados estiverem desativados, os gatilhos recursivos também serão desabilitados, apesar da configuração RECURSIVE_TRIGGERS definida por meio do uso de ALTER DATABASE.  
  
O primeiro gatilho AFTER aninhado dentro de um gatilho INSTEAD OF será disparado mesmo se a opção de configuração do servidor de **gatilhos aninhados** for 0. Porém, nessa configuração, os gatilhos AFTER posteriores não são disparados. Verifique se há gatilhos aninhados nos seus aplicativos a fim de determinar se os aplicativos seguem as regras de negócio quando a opção de configuração do servidor de **gatilhos aninhados** está definida como 0. Caso contrário, faça as modificações apropriadas.  
  
### <a name="deferred-name-resolution"></a>Resolução de nome adiada  
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite que procedimentos armazenados, gatilhos e lotes [!INCLUDE[tsql](../../includes/tsql-md.md)] referenciem tabelas que não existem em tempo de compilação. Essa capacidade é chamada de resolução de nome adiada.  
  
## <a name="permissions"></a>Permissões  
A criação de um gatilho DML requer a permissão ALTER na tabela ou exibição na qual o gatilho é criado.  
  
A criação de um gatilho DDL com escopo no servidor (ON ALL SERVER) ou um gatilho de logon requer a permissão CONTROL SERVER no servidor. A criação de um gatilho DDL com escopo no banco de dados (ON DATABASE) requer a permissão ALTER ANY DATABASE DDL TRIGGER no banco de dados atual.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-a-dml-trigger-with-a-reminder-message"></a>A. Usando um gatilho DML com uma mensagem de lembrete  
O gatilho DML a seguir imprime uma mensagem para o cliente quando alguém tenta adicionar ou alterar dados na tabela `Customer` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```sql  
CREATE TRIGGER reminder1  
ON Sales.Customer  
AFTER INSERT, UPDATE   
AS RAISERROR ('Notify Customer Relations', 16, 10);  
GO  
```  
  
### <a name="b-using-a-dml-trigger-with-a-reminder-e-mail-message"></a>b. Usando um gatilho DML com uma mensagem de email de lembrete  
O exemplo a seguir envia uma mensagem de email a uma pessoa especificada (`MaryM`) quando a tabela `Customer` é alterada.  
  
```sql  
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
Como as restrições CHECK só referenciam as colunas nas quais a restrição de nível de coluna ou de nível de tabela é definida, é preciso definir qualquer restrição de tabela cruzada (nesse caso, as regras de negócio) como gatilho.  
  
O exemplo a seguir cria um gatilho DML no banco de dados AdventureWorks2012. Esse gatilho realiza uma verificação para ter certeza de que a avaliação de crédito do fornecedor é satisfatória (não 5) quando há uma tentativa de inserir uma nova ordem de compra na tabela `PurchaseOrderHeader`. Para obter a classificação de crédito do fornecedor, a tabela `Vendor` deve ser referenciada. Se a classificação de crédito for muito baixa, uma mensagem será exibida e a inserção não será executada.  
  
```sql  
-- This trigger prevents a row from being inserted in the Purchasing.PurchaseOrderHeader 
-- table when the credit rating of the specified vendor is set to 5 (below average).  
  
CREATE TRIGGER Purchasing.LowCredit ON Purchasing.PurchaseOrderHeader  
AFTER INSERT  
AS  
IF (ROWCOUNT_BIG() = 0)
RETURN;
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
  
```sql  
CREATE TRIGGER safety   
ON DATABASE   
FOR DROP_SYNONYM  
AS   
IF (@@ROWCOUNT = 0)
RETURN;
   RAISERROR ('You must disable Trigger "safety" to drop synonyms!',10, 1)  
   ROLLBACK  
GO  
DROP TRIGGER safety  
ON DATABASE;  
GO  
```  
  
### <a name="e-using-a-server-scoped-ddl-trigger"></a>E. Usando um gatilho DDL no escopo do servidor  
O exemplo a seguir usa um gatilho DDL para imprimir uma mensagem se qualquer evento CREATE DATABASE ocorrer na instância do servidor atual e usa a função `EVENTDATA` para recuperar o texto da instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] correspondente. Para obter mais exemplos que usam EVENTDATA em gatilhos DDL, veja [Usar a função EVENTDATA](../../relational-databases/triggers/use-the-eventdata-function.md).  
  
**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```sql  
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
O exemplo de gatilho de logon a seguir nega uma tentativa de logon no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como um membro do logon *login_test* se já houver três sessões de usuário executadas com esse logon.  
  
**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```sql  
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
O exemplo a seguir consulta as exibições do catálogo `sys.triggers` e `sys.trigger_events` para determinar quais eventos de linguagem [!INCLUDE[tsql](../../includes/tsql-md.md)] fazem o gatilho `safety` ser acionado. O gatilho, `safety`, é criado no exemplo 'D', localizado acima.  
  
```sql  
SELECT TE.*  
FROM sys.trigger_events AS TE  
JOIN sys.triggers AS T ON T.object_id = TE.object_id  
WHERE T.parent_class = 0 AND T.name = 'safety';  
GO  
```  

    

## <a name="see-also"></a>Consulte Também  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [COLUMNS_UPDATED &#40;Transact-SQL&#41;](../../t-sql/functions/columns-updated-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [ENABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/enable-trigger-transact-sql.md)   
 [DISABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/disable-trigger-transact-sql.md)   
 [TRIGGER_NESTLEVEL &#40;Transact-SQL&#41;](../../t-sql/functions/trigger-nestlevel-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)   
 [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)   
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptrigger &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptrigger-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [sp_settriggerorder &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-settriggerorder-transact-sql.md)   
 [UPDATE&#40;&#41; &#40;Transact-SQL&#41;](../../t-sql/functions/update-trigger-functions-transact-sql.md)   
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
  
  


