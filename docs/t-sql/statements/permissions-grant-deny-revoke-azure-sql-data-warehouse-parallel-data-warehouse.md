---
title: Permissões GRANT-DENY-REVOKE – SQL Data do Azure e Parallel Data Warehouses | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5a3b7424-408e-4cb0-8957-667ebf4596fc
author: VanMSFT
ms.author: vanto
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 7e2245de7cf96e7635098fff57013010e143e6a9
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/14/2019
ms.locfileid: "74095584"
---
# <a name="permissions-grant-deny-revoke-azure-sql-data-warehouse-parallel-data-warehouse"></a>Permissões: GRANT, DENY, REVOKE (SQL Data Warehouse do Azure, Parallel Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Use as instruções [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]**GRANT** e **DENY** para conceder ou negar uma permissão (como **UPDATE**) em um protegível (como um banco de dados, uma tabela, uma exibição etc.) de uma entidade de segurança (um logon, um usuário de banco de dados ou uma função de banco de dados). Use **REVOKE** para remover a concessão ou negar uma permissão.  
  
 As permissões no nível do servidor são aplicadas aos logons. As permissões no nível do banco de dados são aplicadas aos usuários de banco de dados e às funções de banco de dados.  
  
 Para ver quais permissões foram concedidas e negadas, consulte as exibições sys.server_permissions e sys.database_permissions. As permissões que não são concedidas ou negadas explicitamente a uma entidade de segurança podem ser herdadas por meio da associação a uma função que tenha permissões. As permissões das funções de banco de dados fixas não podem ser alteradas e não aparecem nas exibições sys.server_permissions e sys.database_permissions.  
  
-   **GRANT** concede explicitamente uma ou mais permissões.  
  
-   **DENY** nega explicitamente uma ou mais permissões à entidade de segurança.  
  
-   **REVOKE** remove as permissões **GRANT** ou **DENY** existentes.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Azure SQL Data Warehouse and Parallel Data Warehouse  
GRANT   
    <permission> [ ,...n ]  
    [ ON [ <class_type> :: ] securable ]   
    TO principal [ ,...n ]  
    [ WITH GRANT OPTION ]  
[;]  
  
DENY   
    <permission> [ ,...n ]  
    [ ON [ <class_type> :: ] securable ]   
    TO principal [ ,...n ]  
    [ CASCADE ]  
[;]  
  
REVOKE   
    <permission> [ ,...n ]  
    [ ON [ <class_type> :: ] securable ]   
    [ FROM | TO ] principal [ ,...n ]  
    [ CASCADE ]  
[;]  
  
<permission> ::=  
{ see the tables below }  
  
<class_type> ::=  
{  
      LOGIN  
    | DATABASE  
    | OBJECT  
    | ROLE  
    | SCHEMA  
    | USER  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 \<permission>[ **,** ...*n* ]  
 Uma ou mais permissões a serem concedidas, negadas ou revogadas.  
  
 ON [ \<class_type> :: ] *securable* A cláusula **ON** descreve o parâmetro protegível no qual as permissões grant, deny ou revoke serão concedidas.  
  
 \<class_type> O tipo de classe do protegível. Pode ser **LOGIN**, **DATABASE**, **OBJECT**, **SCHEMA**, **ROLE** ou **USER**. As permissões também podem ser concedidas para o **SERVER**_class\_type_, mas **SERVER** não é especificado para essas permissões. **DATABASE** não é especificado quando a permissão inclui a palavra **DATABASE** (por exemplo **ALTER ANY DATABASE**). Quando nenhum *class_type* é especificado e o tipo de permissão não é restrito para o servidor ou a classe de banco de dados, a classe é considerada **OBJECT**.  
  
 *securable*  
 O nome do logon, do banco de dados, da tabela, da exibição, do esquema, do procedimento, da função ou do usuário em que as permissões serão concedidas, negadas ou revogadas. O nome do objeto pode ser especificado com as regras de nomenclatura de três partes descritas em [Convenções de sintaxe Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
 TO *principal* [ **,** ...*n* ]  
 Uma ou mais entidades de segurança às quais as permissões estão sendo concedidas, negadas ou revogadas. Entidade de segurança é o nome de um logon, um usuário de banco de dados ou uma função de banco de dados.  
  
 FROM *principal* [ **,** ...*n* ]  
 Uma ou mais entidades de segurança das quais as permissões serão revogadas.  Entidade de segurança é o nome de um logon, um usuário de banco de dados ou uma função de banco de dados. **FROM** só pode ser usado com uma instrução **REVOKE**. **TO** pode ser usado com **GRANT**, **DENY** ou **REVOKE**.  
  
 WITH GRANT OPTION  
 Indica que o usuário autorizado também poderá conceder a permissão especificada a outras entidades.  
  
 CASCADE  
 Indica que a permissão foi negada ou revogada para a entidade de segurança especificada e para todas as outras entidades de segurança às quais a entidade de segurança concedeu a permissão. Necessário quando a entidade de segurança tem a permissão com **GRANT OPTION**.  
  
 GRANT OPTION FOR  
 Indica que a habilidade de conceder a permissão especificada será revogada. Será necessário quando você estiver usando o argumento **CASCADE**.  
  
> [!IMPORTANT]  
>  Se a entidade de segurança tiver a permissão especificada sem a opção **GRANT**, a própria permissão será revogada.  
  
## <a name="permissions"></a>Permissões  
 Para conceder uma permissão, o concessor precisa ter a própria permissão com a **WITH GRANT OPTION** ou ter uma permissão superior que implique a concessão da permissão.  Os proprietários de objetos podem conceder permissões nos objetos de sua propriedade. As entidades de segurança com a permissão **CONTROL** em um protegível podem conceder a permissão nesse protegível.  Os membros das funções de banco de dado fixas **db_owner** e **db_securityadmin** podem conceder qualquer permissão no banco de dados.  
  
## <a name="general-remarks"></a>Comentários gerais  
 Negar ou revogar permissões a uma entidade de segurança não afetará as solicitações com autorização aprovada que estiverem em execução no momento. Para restringir o acesso imediatamente, você precisa cancelar as solicitações ativas ou encerrar as sessões atuais.  
  
> [!NOTE]  
>  A maioria das funções de servidor fixas não estão disponíveis nesta versão. Use as funções de banco de dados definidas pelo usuário. Não é possível adicionar logons à função de servidor fixa **sysadmin**. Conceder a permissão **CONTROL SERVER** aproxima-se da associação à função de servidor fixa **sysadmin**.  
  
 Algumas instruções exigem várias permissões. Por exemplo, para criar uma tabela, são necessárias as permissões **CREATE TABLE** no banco de dados e a permissão **ALTER SCHEMA** para a tabela que conterá a tabela.  
  
 Às vezes, o PDW (Parallel Data Warehouse) executa procedimentos armazenados para distribuir as ações do usuário para os nós de computação. Portanto, a permissão execute para um banco de dados inteiro não pode ser negada. (Por exemplo, `DENY EXECUTE ON DATABASE::<name> TO <user>;` falhará.) Como uma solução alternativa, negue a permissão execute para esquemas de usuário ou objetos específicos (procedimentos).  
  
### <a name="implicit-and-explicit-permissions"></a>Permissões implícitas e explícitas  
 Uma *permissão explícita* é uma permissão **GRANT** ou **DENY** concedida a uma entidade de segurança por uma instrução **GRANT** ou **DENY**.  
  
 Uma *permissão implícita* é uma permissão **GRANT** ou **DENY** que uma entidade de segurança (logon, usuário ou função de banco de dados) herda de outra função de banco de dados.  
  
 Uma permissão implícita também pode ser herdada de uma permissão de cobertura ou pai. Por exemplo, a permissão **UPDATE** em uma tabela pode ser herdada pela presença da permissão **UPDATE** no esquema que contém a tabela ou da permissão **CONTROL** na tabela.  
  
### <a name="ownership-chaining"></a>Encadeamento de propriedade  
 Quando vários objetos de banco de dados acessam uns aos outros sequencialmente, essa sequência é conhecida como *cadeia*. Embora essas cadeias não existam independentemente, quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se desvia de links em uma cadeia, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] avalia as permissões nos objetos do cliente de forma diferente do que faria se estivesse acessando os objetos separadamente. O encadeamento de propriedade tem implicações importantes para o gerenciamento de segurança. Para obter mais informações sobre cadeias de propriedade, veja [Cadeias de Propriedades](https://msdn.microsoft.com/library/ms188676\(v=sql11\).aspx) e [Tutorial: Cadeias de Propriedade e Comutação de Contexto](../../relational-databases/tutorial-ownership-chains-and-context-switching.md).  
  
## <a name="permission-list"></a>Lista de permissões  
  
### <a name="server-level-permissions"></a>Permissões no nível do servidor  
 As permissões no nível do servidor podem ser concedidas, negadas e revogadas dos logons.  
  
 **Permissões que se aplicam a servidores**  
  
-   CONTROL SERVER  
  
-   ADMINISTER BULK OPERATIONS  
  
-   ALTER ANY CONNECTION  
  
-   ALTER ANY DATABASE  
  
-   CREATE ANY DATABASE  
  
-   ALTER ANY EXTERNAL DATA SOURCE  
  
-   ALTER ANY EXTERNAL FILE FORMAT  
  
-   ALTER ANY LOGIN  
  
-   ALTER SERVER STATE  
  
-   CONNECT SQL  
  
-   VIEW ANY DEFINITION  
  
-   VIEW ANY DATABASE  
  
-   VIEW SERVER STATE  
  
 **Permissões que se aplicam a logons**  
  
-   CONTROL ON LOGIN  
  
-   ALTER ON LOGIN  
  
-   IMPERSONATE ON LOGIN  
  
-   VIEW DEFINITION  
  
### <a name="database-level-permissions"></a>Permissões no nível do banco de dados  
 As permissões no nível do banco de dados podem ser concedidas, revogadas e negadas dos usuários de banco de dados e das funções de banco de dados definidas pelo usuário.  
  
 **Permissões que se aplicam a todas as classes de banco de dados**  
  
-   CONTROL  
  
-   ALTER  
  
-   VIEW DEFINITION  
  
 **Permissões que se aplicam a todas as classes de banco de dados, exceto a usuários**  
  
-   TAKE OWNERSHIP  
  
 **Permissões que se aplicam somente a bancos de dados**  
  
-   ALTER ANY DATABASE  
  
-   ALTER ON DATABASE  
  
-   ALTER ANY DATASPACE  
  
-   ALTER ANY ROLE  
  
-   ALTER ANY SCHEMA  
  
-   ALTER ANY USER  
  
-   BACKUP DATABASE  
  
-   CONNECT ON DATABASE  
  
-   CREATE PROCEDURE  
  
-   CREATE ROLE  
  
-   CREATE SCHEMA  
  
-   CREATE TABLE  
  
-   CREATE VIEW  
  
-   SHOWPLAN  
  
 **Permissões que se aplicam somente a usuários**  
  
-   IMPERSONATE  
  
 **Permissões que se aplicam a bancos de dados, esquemas e objetos**  
  
-   ALTER  
  
-   Delete (excluir)  
  
-   Execute  
  
-   INSERT  
  
-   SELECT  
  
-   UPDATE  
  
-   REFERENCES  
  
 Para obter uma definição de cada tipo de permissão, confira [Permissões (Mecanismo de Banco de Dados)](https://msdn.microsoft.com/library/ms191291.aspx).  
  
### <a name="chart-of-permissions"></a>Gráfico de permissões  
 Todas as permissões são representadas graficamente neste cartaz. Essa é a maneira mais fácil de ver a hierarquia aninhada de permissões. Por exemplo a permissão **ALTER ON LOGIN** pode ser concedida sozinha, mas também estará incluída se um logon receber a permissão a **CONTROL** nesse logon ou se um logon receber a permissão **ALTER ANY LOGIN**.  
  
 ![Cartaz de permissões de segurança do APS](../../t-sql/statements/media/aps-security-perms-poster.png "Cartaz de permissões de segurança do APS")  
  
 Para baixar uma versão completa desse cartaz, confira [Permissões do SQL Server PDW](https://go.microsoft.com/fwlink/?LinkId=244249) na seção de arquivos do site do Yammer do APS (ou solicite-a enviando um email para **apsdoc\@microsoft.com**).  
  
## <a name="default-permissions"></a>Permissões padrão  
 A lista a seguir descreve as permissões padrão:  
  
-   Quando um logon é criado usando a instrução **CREATE LOGIN**, o novo logon recebe a permissão **CONNECT SQL**.  
  
-   Todos os logons são membros da função de servidor **pública** e não podem ser removidos dessa função **pública**.  
  
-   Quando um usuário de banco de dados é criado usando a permissão **CREATE USER**, o usuário de banco de dados recebe a permissão **CONNECT** no banco de dados.  
  
-   As entidades de segurança, incluindo a função **pública**, não têm nenhuma permissão explícita ou implícita por padrão.  
  
-   Quando um logon ou um usuário se torna o proprietário de um banco de dados ou de um objeto, o logon ou o usuário passa a ter todas as permissões no banco de dados ou no objeto. As permissões de propriedade não podem ser alteradas e não são visíveis como as permissões explícitas. As instruções **GRANT**, **DENY** e **REVOKE** não têm efeito sobre os proprietários.  
  
-   O logon **sa** tem todas as permissões no dispositivo. Semelhante às permissões de propriedade, as permissões de **sa** não podem ser alteradas e não são visíveis como as permissões explícitas. As instruções **GRANT**, **DENY** e **REVOKE** não têm efeito sobre o logon **sa**. O logon **sa** não pode ser renomeado.  
  
-   A instrução **USE** não requer permissões. Todas as entidades de segurança podem executar a instrução **USE** em qualquer banco de dados.  
  
##  <a name="Examples"></a> Exemplos: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-granting-a-server-level-permission-to-a-login"></a>A. Concedendo uma permissão no nível do servidor para um logon  
 As duas instruções a seguir concedem uma permissão no nível do servidor para um logon.  
  
```  
GRANT CONTROL SERVER TO [Ted];  
```  
  
```  
GRANT ALTER ANY DATABASE TO Mary;  
```  
  
### <a name="b-granting-a-server-level-permission-to-a-login"></a>B. Concedendo uma permissão no nível do servidor para um logon  
 O exemplo a seguir concede uma permissão no nível do servidor em um logon a uma entidade de segurança do servidor (outro logon).  
  
```  
GRANT  VIEW DEFINITION ON LOGIN::Ted TO Mary;  
```  
  
### <a name="c-granting-a-database-level-permission-to-a-user"></a>C. Concedendo uma permissão no nível do banco de dados para um usuário  
 O exemplo a seguir concede uma permissão no nível do banco de dados em um usuário a uma entidade de segurança do banco de dados (outro usuário).  
  
```  
GRANT VIEW DEFINITION ON USER::[Ted] TO Mary;  
```  
  
### <a name="d-granting-denying-and-revoking-a-schema-permission"></a>D. Concedendo, negando e revogando uma permissão de esquema  
 A seguinte instrução **GRANT** concede a Yuen a capacidade de selecionar dados de qualquer tabela ou exibição no esquema dbo.  
  
```  
GRANT SELECT ON SCHEMA::dbo TO [Yuen];  
```  
  
 A seguinte instrução **DENY** impede que Yuen selecione dados de qualquer tabela ou exibição no esquema dbo. Yuen não poderá ler os dados mesmo que tenha recebido a permissão de alguma outra maneira, como por associação de função.  
  
```  
DENY SELECT ON SCHEMA::dbo TO [Yuen];  
```  
  
 A seguinte instrução **REVOKE** remove a permissão **DENY**. Agora, as permissões explícitas do Yuen são neutras. Yuen poderá selecionar dados de qualquer tabela por meio de outras permissões implícitas, como uma associação de função.  
  
```  
REVOKE SELECT ON SCHEMA::dbo TO [Yuen];  
```  
  
### <a name="e-demonstrating-the-optional-object-clause"></a>E. Demonstrando a cláusula opcional OBJECT::  
 Como OBJECT é a classe padrão para uma instrução de permissão, as duas instruções a seguir são iguais. A cláusula **OBJECT::** é opcional.  
  
```  
GRANT UPDATE ON OBJECT::dbo.StatusTable TO [Ted];  
```  
  
```  
GRANT UPDATE ON dbo.StatusTable TO [Ted];  
```  
  
  

