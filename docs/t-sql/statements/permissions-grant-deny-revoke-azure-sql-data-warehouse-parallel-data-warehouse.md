---
title: "Dados do SQL Azure REVOKE negar CONCEDER as permissões e o Parallel Data Warehouses | Microsoft Docs"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5a3b7424-408e-4cb0-8957-667ebf4596fc
caps.latest.revision: 9
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3c4beb3881b983c0af3add7671dc4c7155649497
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="permissions-grant-deny-revoke-azure-sql-data-warehouse-parallel-data-warehouse"></a>Permissões: GRANT, DENY, REVOKE (Azure SQL Data Warehouse, Parallel Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Use [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] **GRANT** e **DENY** instruções para conceder ou negar uma permissão (como **atualização**) em um protegível (como um banco de dados, tabela, exibição etc.) para uma entidade de segurança (um logon, um usuário de banco de dados ou uma função de banco de dados). Use **REVOGAR** para remover a concessão ou negar uma permissão.  
  
 Permissões de nível de servidor são aplicadas a logons. Permissões de nível de banco de dados são aplicadas a usuários de banco de dados e funções de banco de dados.  
  
 Para ver quais permissões foram concedidas e negadas, consulte as exibições server_permissions e database_permissions. Permissões que não são explicitamente concedidas ou negadas a uma entidade de segurança podem ser herdadas por ter associação em uma função que tenha permissões. As permissões das funções fixas de banco de dados não podem ser alteradas e não aparecem nas exibições server_permissions e database_permissions.  
  
-   **GRANT** concede explicitamente uma ou mais permissões.  
  
-   **Negar** nega explicitamente a entidade de segurança de ter uma ou mais permissões.  
  
-   **REVOGAR** remove existente **GRANT** ou **DENY** permissões.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "ícone de link do tópico") [convenções de sintaxe do Transact-SQL &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 \<permissão > [ **,**... *n* ]  
 Uma ou mais permissões para conceder, negar ou revogar.  
  
 ON [ \<class_type >::] *protegível* o **ON** cláusula descreve o parâmetro protegível na qual deseja conceder, negar ou revogar permissões.  
  
 \<class_type > o tipo de classe do protegível. Isso pode ser **LOGIN**, **banco de dados**, **objeto**, **esquema**, **função**, ou **usuário** . Também podem ser concedidas permissões para o **servidor***class_type*, mas **SERVER** não for especificado para essas permissões. **Banco de dados** não for especificado quando a permissão inclui a palavra **banco de dados** (por exemplo **ALTER ANY DATABASE**). Quando nenhum *class_type* é especificado e o tipo de permissão não é restrito para o servidor ou a classe de banco de dados, a classe é considerada como **objeto**.  
  
 *protegível*  
 O nome de logon, banco de dados, tabela, exibição, esquema, procedimento, função ou usuário no qual deseja conceder, negar ou revogar permissões. O nome do objeto pode ser especificado com as regras de nomenclatura de três partes que são descritas na [convenções de sintaxe do Transact-SQL &#40; Transact-SQL &#41; ](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
 PARA *principal* [ **,**... *n* ]  
 Uma ou mais entidades que estão sendo concedidas, negadas ou revogadas permissões. Entidade é o nome de logon, usuário de banco de dados ou função de banco de dados.  
  
 DE *principal* [ **,**... *n* ]  
 Uma ou mais entidades revogar as permissões.  Entidade é o nome de logon, usuário de banco de dados ou função de banco de dados. **DE** só pode ser usado com um **REVOGAR** instrução. **PARA** pode ser usado com **GRANT**, **DENY**, ou **REVOGAR**.  
  
 WITH GRANT OPTION  
 Indica que o usuário autorizado também poderá conceder a permissão especificada a outras entidades.  
  
 CASCADE  
 Indica que a permissão for negada ou revogada para a entidade especificada e todos os outros principais aos quais o principal concedeu a permissão. Necessário quando a entidade de segurança tem a permissão com **GRANT OPTION**.  
  
 GRANT OPTION FOR  
 Indica que a habilidade de conceder a permissão especificada será revogada. Isso é necessário quando você estiver usando o **CASCADE** argumento.  
  
> [!IMPORTANT]  
>  Se o principal tiver a permissão especificada sem o **GRANT** opção, a própria permissão será revogada.  
  
## <a name="permissions"></a>Permissões  
 Para conceder uma permissão, o concessor deve ter a permissão em si com o **WITH GRANT OPTION**, ou deve ter uma permissão superior que implique na concessão da permissão.  Os proprietários de objetos podem conceder permissões nos objetos de sua propriedade. Entidades com **controle** permissão em um protegível pode conceder a permissão naquele protegível.  Membros de **db_owner** e **db_securityadmin** funções de banco de dados fixa podem conceder qualquer permissão no banco de dados.  
  
## <a name="general-remarks"></a>Comentários gerais  
 Negar ou revogar permissões para uma entidade de segurança não afetará a solicitações que passaram a autorização e estão em execução no momento. Para restringir o acesso imediatamente, você deve cancelar solicitações ativas ou eliminar as sessões atuais.  
  
> [!NOTE]  
>  Funções de servidor fixas mais não estão disponíveis nesta versão. Use as funções de banco de dados definido pelo usuário. Não não possível adicionar logons a **sysadmin** função de servidor fixa. Concedendo a **CONTROL SERVER** permissão aproxima a associação a **sysadmin** função de servidor fixa.  
  
 Algumas instruções exigem várias permissões. Por exemplo criar uma tabela requer o **CREATE TABLE** permissões no banco de dados e o **ALTER SCHEMA** permissão para a tabela que conterá a tabela.  
  
 Às vezes, o PDW executa procedimentos armazenados para distribuir as ações do usuário para os nós de computação. Portanto, não pode ser negada a permissão execute para um banco de dados inteiro. (Por exemplo `DENY EXECUTE ON DATABASE::<name> TO <user>;` falhará.) Como uma solução alternativa, nega a permissão execute para esquemas de usuário ou objetos específicos (procedimentos).  
  
### <a name="implicit-and-explicit-permissions"></a>Permissões implícitas e explícitas  
 Um *permissão explícita* é um **GRANT** ou **DENY** permissão concedida a uma entidade de segurança por um **GRANT** ou **DENY**instrução.  
  
 Um *permissão implícita* é um **GRANT** ou **DENY** permissão uma entidade de segurança (logon, usuário ou função de banco de dados) foi herdado de outra função de banco de dados.  
  
 Uma permissão implícita também pode ser herdada de uma cobertura ou a permissão pai. Por exemplo, **atualização** permissão em uma tabela pode ser herdada por ter **atualização** permissão no esquema que contém a tabela, ou **controle** permissão na tabela.  
  
### <a name="ownership-chaining"></a>Encadeamento de propriedade  
 Quando vários objetos de banco de dados acessam uns aos outros sequencialmente, a sequência é conhecida como uma *cadeia*. Embora essas cadeias não existam independentemente, quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se desvia de links em uma cadeia, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] avalia as permissões nos objetos do cliente de forma diferente do que faria se estivesse acessando os objetos separadamente. Encadeamento de propriedade tem implicações importantes para gerenciar a segurança. Para obter mais informações sobre cadeias de propriedade, consulte [cadeias de propriedade](http://msdn.microsoft.com/en-us/library/ms188676\(v=sql11\).aspx) e [Tutorial: cadeias de propriedade e alternância de contexto](http://msdn.microsoft.com/en-us/library/bb153640\(v=sql11\).aspx).  
  
## <a name="permission-list"></a>Lista de permissão  
  
### <a name="server-level-permissions"></a>Permissões de nível de servidor  
 Permissões de nível de servidor podem ser concedida, negadas e revogadas de logons.  
  
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
  
-   LOGON DE CONTROLE  
  
-   ALTER LOGON  
  
-   IMPERSONATE NO LOGON  
  
-   VIEW DEFINITION  
  
### <a name="database-level-permissions"></a>Permissões de nível de banco de dados  
 Permissões de nível de banco de dados podem ser concedidas, revogadas e negadas de usuários de banco de dados e funções de banco de dados definido pelo usuário.  
  
 **Permissões que se aplicam a todas as classes de banco de dados**  
  
-   CONTROL  
  
-   ALTER  
  
-   VIEW DEFINITION  
  
 **Permissões que se aplicam a todas as classes de banco de dados, exceto os usuários**  
  
-   TAKE OWNERSHIP  
  
 **Permissões que se aplicam somente aos bancos de dados**  
  
-   ALTER ANY DATABASE  
  
-   ALTER NO BANCO DE DADOS  
  
-   ALTER ANY DATASPACE  
  
-   ALTER ANY ROLE  
  
-   ALTER ANY SCHEMA  
  
-   ALTER ANY USER  
  
-   BACKUP DATABASE  
  
-   CONECTAR-SE NO BANCO DE DADOS  
  
-   CREATE PROCEDURE  
  
-   CREATE ROLE  
  
-   CREATE SCHEMA  
  
-   CREATE TABLE  
  
-   CREATE VIEW  
  
-   SHOWPLAN  
  
 **Permissões que se aplicam somente aos usuários**  
  
-   IMPERSONATE  
  
 **Permissões que se aplicam a bancos de dados, esquemas e objetos**  
  
-   ALTER  
  
-   DELETE  
  
-   EXECUTE  
  
-   INSERT  
  
-   SELECT  
  
-   UPDATE  
  
-   REFRENCES  
  
 Para obter uma definição de cada tipo de permissão, consulte [permissões (mecanismo de banco de dados)](http://msdn.microsoft.com/library/ms191291.aspx).  
  
### <a name="chart-of-permissions"></a>Gráfico de permissões  
 Todas as permissões são representadas graficamente desse cartaz. Essa é a maneira mais fácil para ver a hierarquia aninhada de permissões. Por exemplo o **ALTER ON LOGIN** permissão pode ser concedida por si só, mas também está incluído, se um logon for concedido a **controle** permissão necessária naquele logon, ou se um logon é concedido a **ALTER ANY LOGON** permissão.  
  
 ![Cartaz de permissões de segurança APS](../../t-sql/statements/media/aps-security-perms-poster.png "cartaz de permissões de segurança APS")  
  
 Para baixar uma versão completa desse cartaz, consulte [permissões do SQL Server PDW](http://go.microsoft.com/fwlink/?LinkId=244249)na seção de arquivos do site do Yammer APS (ou solicitação por email de  **apsdoc@microsoft.com** .  
  
## <a name="default-permissions"></a>Permissões padrão  
 A lista a seguir descreve as permissões padrão:  
  
-   Quando um logon é criado usando o **CREATE LOGIN** instrução o novo logon recebe o **CONNECT SQL** permissão.  
  
-   Todos os logons são membros do **pública** função de servidor e não pode ser removido de **público**.  
  
-   Quando um usuário de banco de dados é criado usando o **CREATE USER** permissão, o usuário de banco de dados recebe o **conectar** no banco de dados.  
  
-   Todas as entidades, incluindo o **pública** função, não têm nenhuma permissão explícita ou implícita por padrão.  
  
-   Quando um logon ou usuário se torna o proprietário de um banco de dados ou objeto, o logon ou usuário sempre tem todas as permissões no banco de dados ou objeto. As permissões de propriedade não podem ser alteradas e não são visíveis como permissões explícitas. O **GRANT**, **DENY**, e **REVOGAR** instruções não têm efeito sobre os proprietários.  
  
-   O **sa** logon tem todas as permissões no dispositivo. Semelhante às permissões de propriedade, o **sa** permissões não pode ser alteradas e não são visíveis como permissões explícitas. O **GRANT**, **DENY**, e **REVOGAR** instruções não têm nenhum efeito **sa** logon. O **sa** logon não pode ser renomeado.  
  
-   O **USE** instrução não requer permissões. Todas as entidades de segurança podem executar o **USE** instrução em qualquer banco de dados.  
  
##  <a name="Examples"></a>Exemplos: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-granting-a-server-level-permission-to-a-login"></a>A. Concedendo uma permissão de nível de servidor para um logon  
 As duas instruções a seguir conceder uma permissão de nível de servidor para um logon.  
  
```  
GRANT CONTROL SERVER TO [Ted];  
```  
  
```  
GRANT ALTER ANY DATABASE TO Mary;  
```  
  
### <a name="b-granting-a-server-level-permission-to-a-login"></a>B. Concedendo uma permissão de nível de servidor para um logon  
 O exemplo a seguir concede uma permissão de nível de servidor em um logon para um servidor principal (outro logon).  
  
```  
GRANT  VIEW DEFINITION ON LOGIN::Ted TO Mary;  
```  
  
### <a name="c-granting-a-database-level-permission-to-a-user"></a>C. Concedendo uma permissão de nível de banco de dados para um usuário  
 O exemplo a seguir concede uma permissão de nível de banco de dados em um usuário para um banco de dados principal (outro usuário).  
  
```  
GRANT VIEW DEFINITION ON USER::[Ted] TO Mary;  
```  
  
### <a name="d-granting-denying-and-revoking-a-schema-permission"></a>D. Conceder, negar e revogar uma permissão de esquema  
 O seguinte **GRANT** instrução concede Yuen a capacidade de selecionar dados de qualquer tabela ou exibição no esquema dbo.  
  
```  
GRANT SELECT ON SCHEMA::dbo TO [Yuen];  
```  
  
 O seguinte **DENY** instrução impede que Yuen selecionar dados de qualquer tabela ou exibição no esquema dbo. Yuen não é possível ler os dados mesmo se ele tem permissão de alguma outra maneira, como através de uma associação de função.  
  
```  
DENY SELECT ON SCHEMA::dbo TO [Yuen];  
```  
  
 O seguinte **REVOGAR** instrução remove o **DENY** permissão. Agora, as permissões explícitas do Yuen são neutras. Yuen poderá selecionar dados de qualquer tabela por meio de outras permissões implícitas, como um membro da função.  
  
```  
REVOKE SELECT ON SCHEMA::dbo TO [Yuen];  
```  
  
### <a name="e-demonstrating-the-optional-object-clause"></a>E. Demonstrando o objeto opcional:: cláusula  
 Porque o objeto é a classe padrão para uma instrução de permissão, as duas instruções a seguir são os mesmos. O **objeto::** cláusula é opcional.  
  
```  
GRANT UPDATE ON OBJECT::dbo.StatusTable TO [Ted];  
```  
  
```  
GRANT UPDATE ON dbo.StatusTable TO [Ted];  
```  
  
  


