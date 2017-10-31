---
title: DENY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DENY
- DENY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- schema-level securables [SQL Server]
- security [SQL Server], denying access
- DENY statement
- permissions [SQL Server], denying
- server-level securables [SQL Server]
- inherited security settings [SQL Server]
- denying permissions [SQL Server], DENY statement
- principal security [SQL Server]
- database-level securables [SQL Server]
- denying permissions [SQL Server]
ms.assetid: c32d1e01-9ee9-4665-a516-fcfece58078e
caps.latest.revision: 48
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 08f2d3c555dceef71e331b6df8727afb5780b86b
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="deny-transact-sql"></a>DENY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Nega uma permissão a uma entidade de segurança. Impede a entidade de segurança de herdar a permissão através das suas associações de grupo ou de função. NEGA tem precedência sobre todas as permissões, exceto que DENY não se aplicam a proprietários de objetos ou os membros da função de servidor fixa sysadmin.
  **Observação de segurança** função de servidor fixa de membros do sysadmin e proprietários de objeto não podem ser negados permissões. "
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
-- Simplified syntax for DENY  
DENY   { ALL [ PRIVILEGES ] } 
     | <permission>  [ ( column [ ,...n ] ) ] [ ,...n ]  
    [ ON [ <class> :: ] securable ] 
    TO principal [ ,...n ]   
    [ CASCADE] [ AS principal ]  
[;]

<permission> ::=  
{ see the tables below }  
  
<class> ::=  
{ see the tables below }  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DENY   
    <permission> [ ,...n ]  
    [ ON [ <class_> :: ] securable ]   
    TO principal [ ,...n ]  
    [ CASCADE ]  
[;]  
  
<permission> ::=  
{ see the tables below }  
  
<class> ::=  
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
 Esta opção não nega todas as permissões possíveis. Negar ALL é equivalente a negar as permissões a seguir.  
  
-   Se o protegível for um banco de dados, ALL será equivalente a BACKUP DATABASE, BACKUP LOG, CREATE DATABASE, CREATE DEFAULT, CREATE FUNCTION, CREATE PROCEDURE, CREATE RULE, CREATE TABLE e CREATE VIEW.  
  
-   Se o protegível for uma função escalar, ALL será equivalente a EXECUTE e REFERENCES.  
  
-   Se o protegível for uma função com valor de tabela, ALL será equivalente a DELETE, INSERT, REFERENCES, SELECT e UPDATE.  
  
-   Se o protegível for um procedimento armazenado, ALL será equivalente a EXECUTE.  
  
-   Se o protegível for uma tabela, ALL será equivalente a DELETE, INSERT, REFERENCES, SELECT e UPDATE.  
  
-   Se o protegível for uma exibição, ALL será equivalente a DELETE, INSERT, REFERENCES, SELECT e UPDATE.  
  
> [!NOTE]  
>  A sintaxe DENY ALL é preterida. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Negue as permissões específicas em vez disso.  
  
 PRIVILEGES  
 Incluído para conformidade com ISO. Não altera o comportamento de ALL.  
  
 *permissão*  
 É o nome de uma permissão. Os mapeamentos válidos de permissões para protegíveis são descritos nos subtópicos listados a seguir.  
  
 *coluna*  
 Especifica o nome de uma coluna em uma tabela na qual as permissões estão sendo negadas. Os parênteses () são necessários.  
  
 *classe*  
 Especifica a classe do protegível em que a permissão está sendo negada. O qualificador de escopo **::** é necessária.  
  
 *protegível*  
 Especifica o protegível no qual a permissão está sendo negada.  
  
 PARA *principal*  
 É o nome de uma entidade. Os principais para os quais as permissões em um protegível podem ser negadas variam, dependendo do protegível. Consulte os tópicos específicos sobre protegíveis listados a seguir para obter as combinações válidas.  
  
 CASCADE  
 Indica que a permissão está sendo negada para o principal especificado e todos os outros principais aos quais o principal concedeu a permissão. Necessário quando o principal tem a permissão com GRANT OPTION.  
  
 AS *principal*  
  Use a cláusula principal para indicar que a entidade de segurança registrada como denier da permissão deve ser uma entidade de segurança diferente da pessoa que executa a instrução. Por exemplo, suponha que o usuário Mary é principal_id 12 e usuário Raul é 15 principal. Mary executa `DENY SELECT ON OBJECT::X TO Steven WITH GRANT OPTION AS Raul;` agora a tabela database_permissions indicará que grantor_prinicpal_id da instrução deny foi 15 (Raul), embora na verdade, a instrução foi executada pelo usuário 13 (Mary).
  
O uso de como esta instrução não implica a capacidade de representar outro usuário.  
  
## <a name="remarks"></a>Comentários  
 A sintaxe completa da instrução DENY é complexa. O diagrama de sintaxe acima foi simplificado para chamar atenção para sua estrutura. A sintaxe completa para negar permissões em protegíveis específicos é descrita nos tópicos listados a seguir.  
  
 DENY falhará se CASCADE não for especificado ao negar uma permissão a uma entidade de segurança à qual ela foi concedida com GRANT OPTION especificado.  
  
 O procedimento armazenado do sistema sp_helprotect relata as permissões em um protegível no nível de banco de dados.  
  
> [!CAUTION]  
>  Um DENY em nível de tabela não tem precedência sobre um GRANT em nível de coluna. Essa inconsistência na hierarquia de permissões foi preservada para manter a compatibilidade com versões anteriores. Ela será removida em uma versão futura.  
  
> [!CAUTION]  
>  Negar a permissão CONTROL em um banco de dados implicitamente nega a permissão CONNECT no banco de dados. Um principal ao qual é negada a permissão CONTROL em um banco de dados não poderá se conectar a esse banco de dados.  
  
> [!CAUTION]  
>  Negar a permissão CONTROL SERVER implicitamente nega a permissão CONNECT SQL no servidor. Um principal ao qual é negada a permissão CONTROL SERVER em um servidor não poderá se conectar a esse servidor.  
  
## <a name="permissions"></a>Permissões  
 O chamador (ou o principal especificado com a opção AS) deve ter a permissão CONTROL no protegível ou uma permissão superior que indica a permissão CONTROL no protegível. Se usar a cláusula AS, o principal especificado deverá ser proprietário do protegível no qual uma permissão está sendo negada.  
  
 Os usuários autorizados da permissão CONTROL SERVER, como os membros da função de servidor fixa sysadmin, podem negar qualquer permissão em qualquer protegível do servidor. Os usuários autorizados da permissão CONTROL no banco de dados, como os membros da função de banco de dados fixa db_owner, podem negar qualquer permissão em qualquer protegível no banco de dados. Os usuários autorizados da permissão CONTROL em um esquema podem negar qualquer permissão no esquema. Se a cláusula AS for usada, o principal especificado deverá ser proprietário do protegível no qual as permissões estão sendo negadas.  
  
## <a name="examples"></a>Exemplos  
 A tabela a seguir lista os protegíveis e os tópicos que descrevem a sintaxe específica de protegíveis.  
  
|||  
|-|-|  
|Função de aplicativo|[Negar permissões de Principal de banco de dados &#40; Transact-SQL &#41;](../../t-sql/statements/deny-database-principal-permissions-transact-sql.md)|  
|Assembly|[Negar permissões de Assembly &#40; Transact-SQL &#41;](../../t-sql/statements/deny-assembly-permissions-transact-sql.md)|  
|Chave assimétrica|[Negar permissões de chave assimétrica &#40; Transact-SQL &#41;](../../t-sql/statements/deny-asymmetric-key-permissions-transact-sql.md)|  
|Grupo de disponibilidade|[Negar permissões de grupo de disponibilidade &#40; Transact-SQL &#41;](../../t-sql/statements/deny-availability-group-permissions-transact-sql.md)|  
|Certificado|[Negar permissões de certificado &#40; Transact-SQL &#41;](../../t-sql/statements/deny-certificate-permissions-transact-sql.md)|  
|Contrato|[Negar permissões do Service Broker &#40; Transact-SQL &#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)|  
|Banco de Dados|[Negar permissões de banco de dados &#40; Transact-SQL &#41;](../../t-sql/statements/deny-database-permissions-transact-sql.md)|  
|Credencial com escopo de banco de dados|[DENY (Transact-SQL) de credencial no escopo do banco de dados](../../t-sql/statements/deny-database-scoped-credential-transact-sql.md)|  
|Ponto de extremidade|[Negar permissões de ponto de extremidade &#40; Transact-SQL &#41;](../../t-sql/statements/deny-endpoint-permissions-transact-sql.md)|  
|Catálogo de texto completo|[Negar permissões de texto completo &#40; Transact-SQL &#41;](../../t-sql/statements/deny-full-text-permissions-transact-sql.md)|  
|Lista de palavras irrelevantes de texto completo|[Negar permissões de texto completo &#40; Transact-SQL &#41;](../../t-sql/statements/deny-full-text-permissions-transact-sql.md)|  
|Função|[Negar permissões de objeto &#40; Transact-SQL &#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|Logon|[Negar permissões de entidade do servidor &#40; Transact-SQL &#41;](../../t-sql/statements/deny-server-principal-permissions-transact-sql.md)|  
|Tipo de mensagem|[Negar permissões do Service Broker &#40; Transact-SQL &#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)|  
|Objeto|[Negar permissões de objeto &#40; Transact-SQL &#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|Fila|[Negar permissões de objeto &#40; Transact-SQL &#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|Associação de serviço remoto|[Negar permissões do Service Broker &#40; Transact-SQL &#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)|  
|Função|[Negar permissões de Principal de banco de dados &#40; Transact-SQL &#41;](../../t-sql/statements/deny-database-principal-permissions-transact-sql.md)|  
|Rota|[Negar permissões do Service Broker &#40; Transact-SQL &#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)|  
|esquema|[Negar permissões de esquema &#40; Transact-SQL &#41;](../../t-sql/statements/deny-schema-permissions-transact-sql.md)|  
|Lista de propriedades de pesquisa|[Negar permissões Search Property List &#40; Transact-SQL &#41;](../../t-sql/statements/deny-search-property-list-permissions-transact-sql.md)|  
|Servidor|[Negar permissões de servidor &#40; Transact-SQL &#41;](../../t-sql/statements/deny-server-permissions-transact-sql.md)|  
|Serviço|[Negar permissões do Service Broker &#40; Transact-SQL &#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)|  
|Procedimento armazenado|[Negar permissões de objeto &#40; Transact-SQL &#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|Chave simétrica|[Negar permissões de chave simétrica &#40; Transact-SQL &#41;](../../t-sql/statements/deny-symmetric-key-permissions-transact-sql.md)|  
|Sinônimo|[Negar permissões de objeto &#40; Transact-SQL &#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|Objetos do sistema|[Negar permissões de objeto do sistema &#40; Transact-SQL &#41;](../../t-sql/statements/deny-system-object-permissions-transact-sql.md)|  
|Table|[Negar permissões de objeto &#40; Transact-SQL &#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|Tipo|[Negar permissões do tipo &#40; Transact-SQL &#41;](../../t-sql/statements/deny-type-permissions-transact-sql.md)|  
|Usuário|[Negar permissões de Principal de banco de dados &#40; Transact-SQL &#41;](../../t-sql/statements/deny-database-principal-permissions-transact-sql.md)|  
|Exibição|[Negar permissões de objeto &#40; Transact-SQL &#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|Coleção de esquema XML|[Negar permissões de coleção de esquemas XML &#40; Transact-SQL &#41;](../../t-sql/statements/deny-xml-schema-collection-permissions-transact-sql.md)|  
  
## <a name="see-also"></a>Consulte também  
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_adduser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [sp_changedbowner &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [sp_dropuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [sp_helprotect &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)   
 [sp_helpuser &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)  
  
  

