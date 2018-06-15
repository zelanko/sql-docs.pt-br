---
title: GRANT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- GRANT_TSQL
- GRANT
dev_langs:
- TSQL
helpviewer_keywords:
- granting permissions [SQL Server], GRANT statement
- schema-level securables [SQL Server]
- GRANT statement
- cross-database permissions
- GRANT statement, about GRANT statement
- server-level securables [SQL Server]
- database-level securables [SQL Server]
- permissions [SQL Server], granting
ms.assetid: a760c16a-4d2d-43f2-be81-ae9315f38185
caps.latest.revision: 64
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 71e48ac3fdf525ba77c288cf0e33cc879e72a5a9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33074783"
---
# <a name="grant-transact-sql"></a>GRANT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Concede permissões em um protegível a uma entidade.  O conceito geral é usar GRANT para conceder \<some permission> ON \<some object> TO \<some user, login, or group>. Para obter uma discussão geral sobre permissões, consulte [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-database-engine.md).  
  
 ![Ícone de link do artigo](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do artigo") [Convenções de sintaxe do Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
-- Simplified syntax for GRANT  
GRANT { ALL [ PRIVILEGES ] }  
      | permission [ ( column [ ,...n ] ) ] [ ,...n ]  
      [ ON [ class :: ] securable ] TO principal [ ,...n ]   
      [ WITH GRANT OPTION ] [ AS principal ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
GRANT   
    <permission> [ ,...n ]  
    [ ON [ <class_type> :: ] securable ]   
    TO principal [ ,...n ]  
    [ WITH GRANT OPTION ]  
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
 ALL  
 Esta opção está preterida e é mantida apenas para compatibilidade com versões anteriores. Ela não concede todas as permissões possíveis. A concessão ALL é equivalente a conceder as seguintes permissões: 
  
-   Se o protegível for um banco de dados, ALL será equivalente a BACKUP DATABASE, BACKUP LOG, CREATE DATABASE, CREATE DEFAULT, CREATE FUNCTION, CREATE PROCEDURE, CREATE RULE, CREATE TABLE e CREATE VIEW.  
  
-   Se o protegível for uma função escalar, ALL será equivalente a EXECUTE e REFERENCES.  
  
-   Se o protegível for uma função com valor de tabela, ALL será equivalente a DELETE, INSERT, REFERENCES, SELECT e UPDATE.  
  
-   Se o protegível for um procedimento armazenado, ALL será equivalente a EXECUTE.  
  
-   Se o protegível for uma tabela, ALL será equivalente a DELETE, INSERT, REFERENCES, SELECT e UPDATE.  
  
-   Se o protegível for uma exibição, ALL será equivalente a DELETE, INSERT, REFERENCES, SELECT e UPDATE.  
  
PRIVILEGES  
 Incluído para conformidade com ISO. Não altera o comportamento de ALL.  
  
*permission*  
 É o nome de uma permissão. Os mapeamentos válidos de permissões para protegíveis são descritos nos subtópicos listados a seguir.  
  
*column*  
 Especifica o nome de uma coluna em uma tabela na qual estão sendo concedidas permissões. Os parênteses () são necessários.  
  
*class*  
 Especifica a classe do protegível na qual a permissão está sendo concedida. O qualificador de escopo **::** é obrigatório.  
  
*securable*  
 Especifica o protegível no qual a permissão está sendo concedida.  
  
TO *principal*  
 É o nome de uma entidade. As entidades para as quais permissões em um protegível podem ser concedidas variam, dependendo do protegível. Consulte os subtópicos listados a seguir para ver as combinações válidas.  
  
GRANT OPTION  
 Indica que o usuário autorizado também poderá conceder a permissão especificada a outras entidades.  
  
AS *principal*  
 Use a cláusula de entidade de segurança AS para indicar que a entidade de segurança registrada como o concessor da permissão deve ser uma entidade de segurança diferente da pessoa que executa a instrução. Por exemplo, suponha que o usuário Maria seja a principal_id 12 e o usuário Ricardo seja a entidade de segurança 15. Melissa executa `GRANT SELECT ON OBJECT::X TO Steven WITH GRANT OPTION AS Raul;`. Agora a tabela sys.database_permissions indicará que a grantor_principal_id era 15 (Ricardo), embora na verdade, a instrução tenha sido executada pelo usuário 13 (Melissa).

O uso da cláusula AS geralmente não é recomendado, a menos que você precise definir explicitamente a cadeia de permissão. Para obter mais informações, consulte a seção **Resumo do algoritmo de verificação de permissão** de [Permissões (Mecanismo de Banco de Dados)](../../relational-databases/security/permissions-database-engine.md).

O uso de AS nessa instrução não implica a capacidade de representar outro usuário. 
  
## <a name="remarks"></a>Remarks  
 A sintaxe completa da instrução GRANT é complexa. O diagrama de sintaxe acima foi simplificado para chamar atenção para sua estrutura. A sintaxe completa para conceder permissões em protegíveis específicos é descrita nos artigos listados a seguir.  
  
 A instrução REVOKE pode ser usada para remover permissões concedidas, e a instrução DENY pode ser usada para evitar que uma entidade ganhe uma permissão específica por meio de um GRANT.  
  
 A concessão de uma permissão remove DENY ou REVOKE daquela permissão no protegível especificado. Se a mesma permissão for negada a um escopo mais alto que contém o protegível, o DENY terá precedência. Mas a revogação da permissão concedida em um escopo mais alto não tem precedência.  
  
 Permissões em nível de banco de dados são concedidas dentro do escopo do banco de dados especificado. Se um usuário precisar de permissões em objetos em outro banco de dados, crie a conta de usuário no outro banco de dados ou conceda acesso à conta de usuário no outro banco de dados, bem como no banco de dados atual.  
  
> [!CAUTION]  
>  Um DENY em nível de tabela não tem precedência sobre um GRANT em nível de coluna. Essa inconsistência na hierarquia de permissões foi preservada para manter a compatibilidade com versões anteriores. Ela será removida em uma versão futura.  
  
 O procedimento armazenado do sistema sp_helprotect relata as permissões em um protegível no nível de banco de dados.  
  
## <a name="with-grant-option"></a>WITH GRANT OPTION  
 A instrução **GRANT** ... **WITH GRANT OPTION** especifica que a entidade de segurança que recebe a permissão recebe a capacidade de conceder a permissão especificada para outras contas de segurança. Quando a entidade de segurança que recebe a permissão é uma função ou um grupo do Windows, a cláusula **AS** deve ser usada quando a permissão de objeto precisa ser concedida a usuários que não são os membros do grupo ou da função. Como apenas um usuário, em vez de um grupo ou uma função, pode executar uma instrução **GRANT**, um membro específico do grupo ou um função deve usar a cláusula **AS** para invocar a função ou a associação ao grupo explicitamente ao conceder a permissão. O exemplo a seguir mostra como **WITH GRANT OPTION** é usado quando concedido a uma função ou um grupo do Windows.  
  
```  
-- Execute the following as a database owner  
GRANT EXECUTE ON TestProc TO TesterRole WITH GRANT OPTION;  
EXEC sp_addrolemember TesterRole, User1;  
-- Execute the following as User1  
-- The following fails because User1 does not have the permission as the User1  
GRANT EXECUTE ON TestMe TO User2;  
-- The following succeeds because User1 invokes the TesterRole membership  
GRANT EXECUTE ON TestMe TO User2 AS TesterRole;  
```  
  
## <a name="chart-of-sql-server-permissions"></a>Gráfico de permissões do SQL Server  
 Para obter um gráfico com tamanho de um cartaz de todas as permissões do [!INCLUDE[ssDE](../../includes/ssde-md.md)] em formato pdf, consulte [https://aka.ms/sql-permissions-poster](https://aka.ms/sql-permissions-poster).  
  
## <a name="permissions"></a>Permissões  
 O concessor (ou a entidade de segurança especificada com a opção AS) deve ter a própria permissão com GRANT OPTION ou uma permissão superior que tenha a permissão que está sendo concedida implícita. Se a opção AS for usada, requisitos adicionais se aplicarão. Consulte o artigo específico do protegível para ver os detalhes.  
  
 Os proprietários de objetos podem conceder permissões nos objetos de sua propriedade. Principais com a permissão CONTROL em um item protegível podem conceder permissão nesse item.  
  
 Os usuários autorizados da permissão CONTROL SERVER, como os membros da função de servidor fixa sysadmin, podem conceder qualquer permissão em qualquer protegível do servidor. Os usuários autorizados da permissão CONTROL em um banco de dados, como os membros da função de banco de dados fixa db_owner, podem conceder qualquer permissão para qualquer item de segurança do banco de dados. Os usuários autorizados da permissão CONTROL em um esquema podem conceder qualquer permissão em qualquer objeto dentro do esquema.  
  
## <a name="examples"></a>Exemplos  
 A tabela a seguir lista os protegíveis e os artigos que descrevem a sintaxe específica do protegível.  
  
|||  
|-|-|  
|Função de aplicativo|[Permissões GRANT de entidade de segurança do banco de dados &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md)|  
|Assembly|[Permissões GRANT de assembly &#40;Transact-SQL&#41;](../../t-sql/statements/grant-assembly-permissions-transact-sql.md)|  
|Chave assimétrica|[Permissões GRANT de chave assimétrica &#40;Transact-SQL&#41;](../../t-sql/statements/grant-asymmetric-key-permissions-transact-sql.md)|  
|Grupo de disponibilidade|[Permissões GRANT de grupo de disponibilidade &#40;Transact-SQL&#41;](../../t-sql/statements/grant-availability-group-permissions-transact-sql.md)|  
|Certificado|[Permissões GRANT de certificado &#40;Transact-SQL&#41;](../../t-sql/statements/grant-certificate-permissions-transact-sql.md)|  
|Contrato|[Permissões GRANT do Service Broker &#40;Transact-SQL&#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|banco de dados|[Permissões GRANT de banco de dados &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md)|
|Credencial no escopo do banco de dados|[Credencial GRANT no escopo do banco de dados (Transact-SQL)](../../t-sql/statements/grant-database-scoped-credential-transact-sql.md)|  
|Ponto de extremidade|[Permissões GRANT de ponto de extremidade &#40;Transact-SQL&#41;](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md)|  
|Catálogo de texto completo|[Permissões GRANT de texto completo &#40;Transact-SQL&#41;](../../t-sql/statements/grant-full-text-permissions-transact-sql.md)|  
|Lista de palavras irrelevantes de texto completo|[Permissões GRANT de texto completo &#40;Transact-SQL&#41;](../../t-sql/statements/grant-full-text-permissions-transact-sql.md)|  
|Função|[Permissões de objeto GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|Logon|[Permissões GRANT de entidade de segurança do servidor &#40;Transact-SQL&#41;](../../t-sql/statements/grant-server-principal-permissions-transact-sql.md)|  
|Tipo de mensagem|[Permissões GRANT do Service Broker &#40;Transact-SQL&#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|Object|[Permissões de objeto GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|Fila|[Permissões de objeto GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|Associação de serviço remoto|[Permissões GRANT do Service Broker &#40;Transact-SQL&#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|Role|[Permissões GRANT de entidade de segurança do banco de dados &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md)|  
|Rota|[Permissões GRANT do Service Broker &#40;Transact-SQL&#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|esquema|[Permissões GRANT de esquema &#40;Transact-SQL&#41;](../../t-sql/statements/grant-schema-permissions-transact-sql.md)|  
|Lista de propriedades de pesquisa|[Permissões GRANT de lista de propriedades de pesquisa &#40;Transact-SQL&#41;](../../t-sql/statements/grant-search-property-list-permissions-transact-sql.md)|  
|Servidor|[Permissões de servidor GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-server-permissions-transact-sql.md)|  
|Serviço|[Permissões GRANT do Service Broker &#40;Transact-SQL&#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|Procedimento armazenado|[Permissões de objeto GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|Chave simétrica|[Permissões GRANT de chave simétrica &#40;Transact-SQL&#41;](../../t-sql/statements/grant-symmetric-key-permissions-transact-sql.md)|  
|Sinônimo|[Permissões de objeto GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|Objetos do sistema|[Permissões de objeto do sistema GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-system-object-permissions-transact-sql.md)|  
|Table|[Permissões de objeto GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|Tipo|[Permissões GRANT de tipo &#40;Transact-SQL&#41;](../../t-sql/statements/grant-type-permissions-transact-sql.md)|  
|Usuário|[Permissões GRANT de entidade de segurança do banco de dados &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md)|  
|Exibição|[Permissões de objeto GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|Coleção de esquema XML|[Permissões GRANT de coleção de esquemas XML &#40;Transact-SQL&#41;](../../t-sql/statements/grant-xml-schema-collection-permissions-transact-sql.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_adduser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [sp_changedbowner &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [sp_dropuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [sp_helprotect &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)   
 [sp_helpuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)  
  
  
