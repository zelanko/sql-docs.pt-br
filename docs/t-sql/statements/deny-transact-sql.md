---
title: DENY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d14ee4d8bef4e9b7ada7ee558ca2524538775148
ms.sourcegitcommit: 0343cdf903ca968c6722d09f017df4a2a4c7fd6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2019
ms.locfileid: "67166378"
---
# <a name="deny-transact-sql"></a>DENY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Nega uma permissão a uma entidade de segurança. Impede a entidade de segurança de herdar a permissão através das suas associações de grupo ou de função. DENY tem precedência sobre todas as permissões, exceto que DENY não se aplica a proprietários do objeto nem a membros da função de servidor fixa sysadmin.
  **Observação de segurança** Membros da função de servidor fixa sysadmin e proprietários do objeto não podem ter permissões negadas.
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
  
 *permission*  
 É o nome de uma permissão. Os mapeamentos válidos de permissões para protegíveis são descritos nos subtópicos listados a seguir.  
  
 *column*  
 Especifica o nome de uma coluna em uma tabela na qual as permissões estão sendo negadas. Os parênteses () são necessários.  
  
 *class*  
 Especifica a classe do protegível em que a permissão está sendo negada. O qualificador de escopo **::** é obrigatório.  
  
 *securable*  
 Especifica o protegível no qual a permissão está sendo negada.  
  
 TO *principal*  
 É o nome de uma entidade. Os principais para os quais as permissões em um protegível podem ser negadas variam, dependendo do protegível. Consulte os tópicos específicos sobre protegíveis listados a seguir para obter as combinações válidas.  
  
 CASCADE  
 Indica que a permissão está sendo negada para o principal especificado e todos os outros principais aos quais o principal concedeu a permissão. Necessário quando o principal tem a permissão com GRANT OPTION.  
  
 AS *principal*  
 Especifica o principal do qual o principal que executa esta consulta deriva seu direito de negar a permissão.
Use a cláusula de entidade de segurança AS para indicar que a entidade de segurança registrada como o negador da permissão deve ser uma entidade de segurança diferente da pessoa que executa a instrução. Por exemplo, suponha que o usuário Maria seja a principal_id 12 e o usuário Ricardo seja a entidade de segurança 15. Melissa executa `DENY SELECT ON OBJECT::X TO Steven WITH GRANT OPTION AS Raul;`. Agora a tabela sys.database_permissions indicará que a grantor_principal_id da instrução de negação era 15 (Ricardo), embora na verdade, a instrução tenha sido executada pelo usuário 13 (Melissa).
  
O uso de AS nessa instrução não implica a capacidade de representar outro usuário.  
  
## <a name="remarks"></a>Remarks  
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
 A tabela a seguir lista os protegíveis e os tópicos que descrevem a sintaxe específica a protegíveis.  
  
|||  
|-|-|  
|Função de aplicativo|[Permissões DENY da entidade de segurança do banco de dados &#40;Transact-SQL&#41;](../../t-sql/statements/deny-database-principal-permissions-transact-sql.md)|  
|Assembly|[Permissões DENY de assembly &#40;Transact-SQL&#41;](../../t-sql/statements/deny-assembly-permissions-transact-sql.md)|  
|Chave assimétrica|[Permissões DENY de chave assimétrica &#40;Transact-SQL&#41;](../../t-sql/statements/deny-asymmetric-key-permissions-transact-sql.md)|  
|Grupo de disponibilidade|[Permissões DENY de grupo de disponibilidade &#40;Transact-SQL&#41;](../../t-sql/statements/deny-availability-group-permissions-transact-sql.md)|  
|Certificado|[Permissões DENY de certificado &#40;Transact-SQL&#41;](../../t-sql/statements/deny-certificate-permissions-transact-sql.md)|  
|Contrato|[Permissões DENY do Service Broker &#40;Transact-SQL&#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)|  
|banco de dados|[Permissões DENY de banco de dados &#40;Transact-SQL&#41;](../../t-sql/statements/deny-database-permissions-transact-sql.md)|  
|Credencial no escopo do banco de dados|[Credencial no escopo do banco de dados DENY (Transact-SQL)](../../t-sql/statements/deny-database-scoped-credential-transact-sql.md)|  
|Ponto de extremidade|[Permissões DENY de ponto de extremidade &#40;Transact-SQL&#41;](../../t-sql/statements/deny-endpoint-permissions-transact-sql.md)|  
|Catálogo de texto completo|[Permissões DENY de texto completo &#40;Transact-SQL&#41;](../../t-sql/statements/deny-full-text-permissions-transact-sql.md)|  
|Lista de palavras irrelevantes de texto completo|[Permissões DENY de texto completo &#40;Transact-SQL&#41;](../../t-sql/statements/deny-full-text-permissions-transact-sql.md)|  
|Função|[Permissões de objeto DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|Logon|[Permissões DENY de entidade de segurança do servidor &#40;Transact-SQL&#41;](../../t-sql/statements/deny-server-principal-permissions-transact-sql.md)|  
|Tipo de mensagem|[Permissões DENY do Service Broker &#40;Transact-SQL&#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)|  
|Object|[Permissões de objeto DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|Fila|[Permissões de objeto DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|Associação de serviço remoto|[Permissões DENY do Service Broker &#40;Transact-SQL&#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)|  
|Role|[Permissões DENY da entidade de segurança do banco de dados &#40;Transact-SQL&#41;](../../t-sql/statements/deny-database-principal-permissions-transact-sql.md)|  
|Rota|[Permissões DENY do Service Broker &#40;Transact-SQL&#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)|  
|esquema|[Permissões DENY de esquema &#40;Transact-SQL&#41;](../../t-sql/statements/deny-schema-permissions-transact-sql.md)|  
|Lista de propriedades de pesquisa|[Permissões DENY de lista de propriedades de pesquisa &#40;Transact-SQL&#41;](../../t-sql/statements/deny-search-property-list-permissions-transact-sql.md)|  
|Servidor|[Permissões DENY de servidor &#40;Transact-SQL&#41;](../../t-sql/statements/deny-server-permissions-transact-sql.md)|  
|Serviço|[Permissões DENY do Service Broker &#40;Transact-SQL&#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)|  
|Procedimento armazenado|[Permissões de objeto DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|Chave simétrica|[Permissões DENY de chave simétrica &#40;Transact-SQL&#41;](../../t-sql/statements/deny-symmetric-key-permissions-transact-sql.md)|  
|Sinônimo|[Permissões de objeto DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|Objetos do sistema|[Permissões DENY de objeto do sistema &#40;Transact-SQL&#41;](../../t-sql/statements/deny-system-object-permissions-transact-sql.md)|  
|Table|[Permissões de objeto DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|Tipo|[Permissões DENY de tipo &#40;Transact-SQL&#41;](../../t-sql/statements/deny-type-permissions-transact-sql.md)|  
|Usuário|[Permissões DENY da entidade de segurança do banco de dados &#40;Transact-SQL&#41;](../../t-sql/statements/deny-database-principal-permissions-transact-sql.md)|  
|Exibição|[Permissões de objeto DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|Coleção de esquema XML|[Permissões DENY de coleção de esquemas XML &#40;Transact-SQL&#41;](../../t-sql/statements/deny-xml-schema-collection-permissions-transact-sql.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_adduser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [sp_changedbowner &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [sp_dropuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [sp_helprotect &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)   
 [sp_helpuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)  
  
  
