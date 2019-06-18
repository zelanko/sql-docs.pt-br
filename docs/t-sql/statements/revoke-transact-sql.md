---
title: REVOKE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- REVOKE_TSQL
- REVOKE
dev_langs:
- TSQL
helpviewer_keywords:
- schema-level securables [SQL Server]
- REVOKE statement, Transact-SQL syntax
- removing permissions
- server-level securables [SQL Server]
- deleting permissions
- revoking permissions [SQL Server]
- REVOKE statement
- denying permissions [SQL Server], removing
- database-level securables [SQL Server]
- granting permissions [SQL Server], removing
- permissions [SQL Server], revoking
- dropping permissions
ms.assetid: 9d31d3e7-0883-45cd-bf0e-f0361bbb0956
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2993baa2608c4d5852bd691dcc45667de736edc8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62638704"
---
# <a name="revoke-transact-sql"></a>REVOKE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Remove uma permissão concedida ou negada anteriormente.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
-- Simplified syntax for REVOKE  
REVOKE [ GRANT OPTION FOR ]  
      {   
        [ ALL [ PRIVILEGES ] ]  
        |  
                permission [ ( column [ ,...n ] ) ] [ ,...n ]  
      }  
      [ ON [ class :: ] securable ]   
      { TO | FROM } principal [ ,...n ]   
      [ CASCADE] [ AS principal ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
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
 GRANT OPTION FOR  
 Indica que a habilidade de conceder a permissão especificada será revogada. Isso é necessário quando você está usando o argumento CASCADE.  
  
> [!IMPORTANT]  
>  Se a entidade de segurança tiver a permissão especificada sem a opção GRANT, a própria permissão será revogada.  
  
 ALL  
**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Esta opção não revoga todas as permissões possíveis. A revogação ALL é equivalente a revogar as seguintes permissões.  
  
-   Se o protegível for um banco de dados, ALL será equivalente a BACKUP DATABASE, BACKUP LOG, CREATE DATABASE, CREATE DEFAULT, CREATE FUNCTION, CREATE PROCEDURE, CREATE RULE, CREATE TABLE e CREATE VIEW.  
  
-   Se o protegível for uma função escalar, ALL será equivalente a EXECUTE e REFERENCES.  
  
-   Se o protegível for uma função com valor de tabela, ALL será equivalente a DELETE, INSERT, REFERENCES, SELECT e UPDATE.  
  
-   Se o protegível for um procedimento armazenado, ALL será equivalente a EXECUTE.  
  
-   Se o protegível for uma tabela, ALL será equivalente a DELETE, INSERT, REFERENCES, SELECT e UPDATE.  
  
-   Se o protegível for uma exibição, ALL será equivalente a DELETE, INSERT, REFERENCES, SELECT e UPDATE.  
  
> [!NOTE]  
>  A sintaxe de REVOKE ALL é preterida. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Em vez disso, revogue permissões específicas.  
  
 PRIVILEGES  
 Incluído para conformidade com ISO. Não altera o comportamento de ALL.  
  
 *permission*  
 É o nome de uma permissão. Os mapeamentos válidos de permissões para protegíveis são descritos nos tópicos listados em [Sintaxe específica a protegível](#securable) mais adiante neste tópico.  
  
 *column*  
 Especifica o nome de uma coluna em uma tabela na qual estão sendo revogadas permissões. Os parênteses são necessários.  
  
 *class*  
 Especifica a classe do protegível na qual a permissão está sendo revogada. O qualificador de escopo **::** é obrigatório.  
  
 *securable*  
 Especifica o protegível no qual a permissão está sendo revogada.  
  
 TO | FROM *principal*  
 É o nome de uma entidade. As entidades das quais permissões em um protegível podem ser revogadas variam, dependendo do protegível. Para obter mais informações sobre combinações válidas, veja os tópicos listados em [Sintaxe específica a protegível](#securable) mais adiante neste tópico.  
  
 CASCADE  
 Indica que a permissão que está sendo revogada também será revogada de outras entidades para as quais ela foi concedida por essa entidade. Ao usar o argumento CASCADE, você também deve incluir o argumento GRANT OPTION FOR.  
  
> [!CAUTION]  
>  A revogação em cascata de uma permissão WITH GRANT OPTION concedida revogará as opções GRANT e DENY dessa permissão.  
  
 AS *principal*  
 Use a cláusula de entidade de segurança AS para indicar que você está revogando uma permissão que foi concedida por uma entidade de segurança que não você. Por exemplo, suponha que o usuário Maria seja a principal_id 12 e o usuário Ricardo seja a entidade de segurança 15. Tanto Maria quanto Ricardo concedem a um usuário chamado Estevão a mesma permissão. A tabela database_permissions indicará as permissões duas vezes, mas elas terão, cada uma, um valor de grantor_prinicpal_id diferente. Maria pode revogar a permissão usando o `AS RAUL` cláusula para remover a concessão de Ricardo da permissão.
 
O uso de AS nessa instrução não implica a capacidade de representar outro usuário.  
  
## <a name="remarks"></a>Remarks  
 A sintaxe completa da instrução REVOKE é complexa. O diagrama de sintaxe acima foi simplificado para chamar atenção para sua estrutura. A sintaxe completa para revogação de permissões em protegíveis específicos é descrita nos tópicos listados em [Sintaxe específica a protegível](#securable) mais adiante neste tópico.  
  
 A instrução REVOKE pode ser usada para remover permissões concedidas, e a instrução DENY pode ser usada para evitar que uma entidade ganhe uma permissão específica por meio de um GRANT.  
  
 A concessão de uma permissão remove DENY ou REVOKE daquela permissão no protegível especificado. Se a mesma permissão for negada a um escopo mais alto que contém o protegível, o DENY terá precedência. No entanto a revogação da permissão concedida em um escopo mais alto não tem precedência.  
  
> [!CAUTION]  
>  Um DENY em nível de tabela não tem precedência sobre um GRANT em nível de coluna. Essa inconsistência na hierarquia de permissões foi preservada para compatibilidade com versões anteriores. Ela será removida em uma versão futura.  
  
 O procedimento armazenado do sistema sp_helprotect relata permissões em um protegível no nível de banco de dados  
  
 A instrução REVOKE falhará se CASCADE não estiver especificado ao revogar uma permissão de uma entidade que recebeu aquela permissão com GRANT OPTION especificada.  
  
## <a name="permissions"></a>Permissões  
 As entidades com a permissão CONTROL em um protegível podem revogar a permissão naquele protegível. Os proprietários de objetos podem revogar permissões nos objetos de sua propriedade.  
  
 Os usuários autorizados da permissão CONTROL SERVER, como os membros da função de servidor fixa sysadmin, podem revogar qualquer permissão em qualquer protegível do servidor. Os usuários autorizados da permissão CONTROL em um banco de dados, como os membros da função de banco de dados fixa db_owner, podem revogar qualquer permissão para qualquer item de segurança do banco de dados. Os usuários autorizados da permissão CONTROL em um esquema podem revogar qualquer permissão em qualquer objeto dentro do esquema.  
  
##  <a name="securable"></a> Sintaxe específica de protegível  
 A tabela a seguir lista os protegíveis e os tópicos que descrevem a sintaxe específica a protegíveis.  
  
|Protegível|Tópico|  
|---------------|-----------|  
|Função de aplicativo|[Permissões REVOKE da entidade de segurança do banco de dados &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-database-principal-permissions-transact-sql.md)|  
|Assembly|[Permissões REVOKE de assembly &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-assembly-permissions-transact-sql.md)|  
|Chave assimétrica|[Permissões REVOKE de chave assimétrica &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-asymmetric-key-permissions-transact-sql.md)|  
|Grupo de disponibilidade|[Permissões REVOKE do grupo de disponibilidade &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-availability-group-permissions-transact-sql.md)|  
|Certificado|[Permissões REVOKE de certificado &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-certificate-permissions-transact-sql.md)|  
|Contrato|[Permissões REVOKE do Service Broker &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-service-broker-permissions-transact-sql.md)|  
|banco de dados|[Permissões REVOKE do banco de dados &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-database-permissions-transact-sql.md)|  
|Ponto de extremidade|[Permissões REVOKE do ponto de extremidade &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-endpoint-permissions-transact-sql.md)|  
|Credencial no escopo do banco de dados|[Credencial REVOKE no escopo do banco de dados (Transact-SQL)](../../t-sql/statements/revoke-database-scoped-credential-transact-sql.md)|  
|Catálogo de texto completo|[Permissões REVOKE de texto completo &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-full-text-permissions-transact-sql.md)|  
|Lista de palavras irrelevantes de texto completo|[Permissões REVOKE de texto completo &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-full-text-permissions-transact-sql.md)|  
|Função|[Permissões de Objeto REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)|  
|Logon|[Permissões REVOKE de entidade de segurança do servidor &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-server-principal-permissions-transact-sql.md)|  
|Tipo de mensagem|[Permissões REVOKE do Service Broker &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-service-broker-permissions-transact-sql.md)|  
|Object|[Permissões de Objeto REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)|  
|Fila|[Permissões de Objeto REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)|  
|Associação de serviço remoto|[Permissões REVOKE do Service Broker &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-service-broker-permissions-transact-sql.md)|  
|Role|[Permissões REVOKE da entidade de segurança do banco de dados &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-database-principal-permissions-transact-sql.md)|  
|Rota|[Permissões REVOKE do Service Broker &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-service-broker-permissions-transact-sql.md)|  
|esquema|[Permissões REVOKE de esquema &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-schema-permissions-transact-sql.md)|  
|Lista de propriedades de pesquisa|[Permissões REVOKE de lista de propriedades de pesquisa &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-search-property-list-permissions-transact-sql.md)|  
|Servidor|[Permissões de servidor REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-server-permissions-transact-sql.md)|  
|Serviço|[Permissões REVOKE do Service Broker &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-service-broker-permissions-transact-sql.md)|  
|Procedimento armazenado|[Permissões de Objeto REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)|  
|Chave simétrica|[Permissões REVOKE de chave simétrica &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-symmetric-key-permissions-transact-sql.md)|  
|Sinônimo|[Permissões de Objeto REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)|  
|Objetos do sistema|[Permissões REVOKE do objeto do sistema &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-system-object-permissions-transact-sql.md)|  
|Table|[Permissões de Objeto REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)|  
|Tipo|[Permissões REVOKE de tipo &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-type-permissions-transact-sql.md)|  
|Usuário|[Permissões REVOKE da entidade de segurança do banco de dados &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-database-principal-permissions-transact-sql.md)|  
|Exibição|[Permissões de Objeto REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)|  
|Coleção de esquema XML|[Permissões REVOKE de coleção de esquemas XML &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-xml-schema-collection-permissions-transact-sql.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Hierarquia de permissões &#40;Mecanismo de banco de dados&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)   
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_adduser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [sp_changedbowner &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [sp_dropuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [sp_helprotect &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)   
 [sp_helpuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)  
  
  
