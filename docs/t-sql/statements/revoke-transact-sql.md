---
title: REVOKE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 41
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: aa08be63c0d792ed1e0422860b55a0c8f2abdc8b
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="revoke-transact-sql"></a>REVOKE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Remove uma permissão concedida ou negada anteriormente.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
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
  
 *permissão*  
 É o nome de uma permissão. Os mapeamentos válidos de permissões para protegíveis são descritos nos tópicos listados em [sintaxe específica a protegível](#securable) mais adiante neste tópico.  
  
 *coluna*  
 Especifica o nome de uma coluna em uma tabela na qual estão sendo revogadas permissões. Os parênteses são necessários.  
  
 *classe*  
 Especifica a classe do protegível na qual a permissão está sendo revogada. O qualificador de escopo **::** é necessária.  
  
 *protegível*  
 Especifica o protegível no qual a permissão está sendo revogada.  
  
 PARA | DE *principal*  
 É o nome de uma entidade. As entidades das quais permissões em um protegível podem ser revogadas variam, dependendo do protegível. Para obter mais informações sobre as combinações válidas, consulte os tópicos listados em [sintaxe específica a protegível](#securable) mais adiante neste tópico.  
  
 CASCADE  
 Indica que a permissão que está sendo revogada também será revogada de outras entidades para as quais ela foi concedida por essa entidade. Ao usar o argumento CASCADE, você também deve incluir o argumento GRANT OPTION FOR.  
  
> [!CAUTION]  
>  A revogação em cascata de uma permissão WITH GRANT OPTION concedida revogará as opções GRANT e DENY dessa permissão.  
  
 AS *principal*  
 Use a cláusula principal para indicar que você está revogando uma permissão que foi concedida por uma entidade que não seja você. Por exemplo, suponha que o usuário Mary é principal_id 12 e usuário Raul é 15 principal. Mary e Raul concedem a que um usuário nomeado Steven a mesma permissão. A tabela database_permissions indicará as permissões duas vezes, mas tenha um valor de grantor_prinicpal_id diferente. Mary pode revogar a permissão usando o `AS RAUL` cláusula para remover a concessão de Raul da permissão.
 
O uso de como esta instrução não implica a capacidade de representar outro usuário.  
  
## <a name="remarks"></a>Comentários  
 A sintaxe completa da instrução REVOKE é complexa. O diagrama de sintaxe acima foi simplificado para chamar atenção para sua estrutura. A sintaxe completa para revogação de permissões em protegíveis específicos é descrita nos tópicos listados em [sintaxe específica a protegível](#securable) mais adiante neste tópico.  
  
 A instrução REVOKE pode ser usada para remover permissões concedidas, e a instrução DENY pode ser usada para evitar que uma entidade ganhe uma permissão específica por meio de um GRANT.  
  
 A concessão de uma permissão remove DENY ou REVOKE daquela permissão no protegível especificado. Se a mesma permissão for negada a um escopo mais alto que contém o protegível, o DENY terá precedência. No entanto a revogação da permissão concedida em um escopo mais alto não tem precedência.  
  
> [!CAUTION]  
>  Um DENY em nível de tabela não tem precedência sobre um GRANT em nível de coluna. Essa inconsistência na hierarquia de permissões foi preservada para compatibilidade com versões anteriores. Ela será removida em uma versão futura.  
  
 O procedimento armazenado do sistema sp_helprotect relata permissões em um protegível no nível de banco de dados  
  
 A instrução REVOKE falhará se CASCADE não estiver especificado ao revogar uma permissão de uma entidade que recebeu aquela permissão com GRANT OPTION especificada.  
  
## <a name="permissions"></a>Permissões  
 As entidades com a permissão CONTROL em um protegível podem revogar a permissão naquele protegível. Os proprietários de objetos podem revogar permissões nos objetos de sua propriedade.  
  
 Os usuários autorizados da permissão CONTROL SERVER, como os membros da função de servidor fixa sysadmin, podem revogar qualquer permissão em qualquer protegível do servidor. Os usuários autorizados da permissão CONTROL em um banco de dados, como os membros da função de banco de dados fixa db_owner, podem revogar qualquer permissão para qualquer item de segurança do banco de dados. Os usuários autorizados da permissão CONTROL em um esquema podem revogar qualquer permissão em qualquer objeto dentro do esquema.  
  
##  <a name="securable"></a>Sintaxe específica de protegíveis  
 A tabela a seguir lista os protegíveis e os tópicos que descrevem a sintaxe específica de protegíveis.  
  
|Protegível|Tópico|  
|---------------|-----------|  
|Função de aplicativo|[REVOGAR permissões de Principal de banco de dados &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-database-principal-permissions-transact-sql.md)|  
|Assembly|[REVOGAR permissões de Assembly &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-assembly-permissions-transact-sql.md)|  
|Chave assimétrica|[Permissões de chave assimétrica REVOKE &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-asymmetric-key-permissions-transact-sql.md)|  
|Grupo de disponibilidade|[Permissões de grupo de disponibilidade REVOKE &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-availability-group-permissions-transact-sql.md)|  
|Certificado|[Permissões de certificado REVOKE &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-certificate-permissions-transact-sql.md)|  
|Contrato|[REVOGAR permissões do Service Broker &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-service-broker-permissions-transact-sql.md)|  
|Banco de Dados|[REVOGAR permissões de banco de dados &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-database-permissions-transact-sql.md)|  
|Ponto de extremidade|[REVOGAR permissões de ponto de extremidade &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-endpoint-permissions-transact-sql.md)|  
|Credencial com escopo de banco de dados|[Credencial (Transact-SQL) no escopo do banco de dados REVOKE](../../t-sql/statements/revoke-database-scoped-credential-transact-sql.md)|  
|Catálogo de texto completo|[REVOGAR permissões de texto completo &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-full-text-permissions-transact-sql.md)|  
|Lista de palavras irrelevantes de texto completo|[REVOGAR permissões de texto completo &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-full-text-permissions-transact-sql.md)|  
|Função|[REVOGAR permissões de objeto &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)|  
|Logon|[REVOGAR permissões de entidade do servidor &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-server-principal-permissions-transact-sql.md)|  
|Tipo de mensagem|[REVOGAR permissões do Service Broker &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-service-broker-permissions-transact-sql.md)|  
|Objeto|[REVOGAR permissões de objeto &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)|  
|Fila|[REVOGAR permissões de objeto &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)|  
|Associação de serviço remoto|[REVOGAR permissões do Service Broker &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-service-broker-permissions-transact-sql.md)|  
|Função|[REVOGAR permissões de Principal de banco de dados &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-database-principal-permissions-transact-sql.md)|  
|Rota|[REVOGAR permissões do Service Broker &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-service-broker-permissions-transact-sql.md)|  
|esquema|[Permissões de esquema REVOKE &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-schema-permissions-transact-sql.md)|  
|Lista de propriedades de pesquisa|[REVOGAR permissões Search Property List &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-search-property-list-permissions-transact-sql.md)|  
|Servidor|[REVOGAR permissões de servidor &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-server-permissions-transact-sql.md)|  
|Serviço|[REVOGAR permissões do Service Broker &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-service-broker-permissions-transact-sql.md)|  
|Procedimento armazenado|[REVOGAR permissões de objeto &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)|  
|Chave simétrica|[Permissões de chave simétrica REVOKE &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-symmetric-key-permissions-transact-sql.md)|  
|Sinônimo|[REVOGAR permissões de objeto &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)|  
|Objetos do sistema|[REVOGAR permissões de objeto do sistema &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-system-object-permissions-transact-sql.md)|  
|Table|[REVOGAR permissões de objeto &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)|  
|Tipo|[Permissões do tipo REVOKE &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-type-permissions-transact-sql.md)|  
|Usuário|[REVOGAR permissões de Principal de banco de dados &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-database-principal-permissions-transact-sql.md)|  
|Exibição|[REVOGAR permissões de objeto &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)|  
|Coleção de esquema XML|[REVOGAR permissões de coleção de esquemas XML &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-xml-schema-collection-permissions-transact-sql.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Hierarquia de permissões &#40;Mecanismo de banco de dados&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)   
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_adduser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [sp_changedbowner &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [sp_dropuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [sp_helprotect &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)   
 [sp_helpuser &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)  
  
  

