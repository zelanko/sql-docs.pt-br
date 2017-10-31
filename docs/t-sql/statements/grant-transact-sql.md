---
title: GRANT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bb9bf548f042a4a6f41322fb789a2cd7e5b6bec9
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="grant-transact-sql"></a>GRANT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Concede permissões em um protegível a uma entidade.  O conceito geral é para GRANT \<alguma permissão > ON \<algum objeto > TO \<algum usuário, logon ou grupo >. Para obter uma discussão geral sobre permissões, consulte [permissões &#40; mecanismo de banco de dados &#41;](../../relational-databases/security/permissions-database-engine.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 Esta opção está preterida e é mantida apenas para compatibilidade com versões anteriores. Ela não concede todas as permissões possíveis. A concessão de ALL é equivalente a conceder as seguintes permissões.  
  
-   Se o protegível for um banco de dados, ALL será equivalente a BACKUP DATABASE, BACKUP LOG, CREATE DATABASE, CREATE DEFAULT, CREATE FUNCTION, CREATE PROCEDURE, CREATE RULE, CREATE TABLE e CREATE VIEW.  
  
-   Se o protegível for uma função escalar, ALL será equivalente a EXECUTE e REFERENCES.  
  
-   Se o protegível for uma função com valor de tabela, ALL será equivalente a DELETE, INSERT, REFERENCES, SELECT e UPDATE.  
  
-   Se o protegível for um procedimento armazenado, ALL será equivalente a EXECUTE.  
  
-   Se o protegível for uma tabela, ALL será equivalente a DELETE, INSERT, REFERENCES, SELECT e UPDATE.  
  
-   Se o protegível for uma exibição, ALL será equivalente a DELETE, INSERT, REFERENCES, SELECT e UPDATE.  
  
PRIVILEGES  
 Incluído para conformidade com ISO. Não altera o comportamento de ALL.  
  
*permissão*  
 É o nome de uma permissão. Os mapeamentos válidos de permissões para protegíveis são descritos nos subtópicos listados a seguir.  
  
*coluna*  
 Especifica o nome de uma coluna em uma tabela na qual estão sendo concedidas permissões. Os parênteses () são necessários.  
  
*classe*  
 Especifica a classe do protegível na qual a permissão está sendo concedida. O qualificador de escopo **::** é necessária.  
  
*protegível*  
 Especifica o protegível no qual a permissão está sendo concedida.  
  
PARA *principal*  
 É o nome de uma entidade. As entidades para as quais permissões em um protegível podem ser concedidas variam, dependendo do protegível. Consulte os subtópicos listados a seguir para obter combinações válidas.  
  
GRANT OPTION  
 Indica que o usuário autorizado também poderá conceder a permissão especificada a outras entidades.  
  
AS *principal*  
 Use a cláusula principal para indicar que a entidade de segurança registrada como o concessor da permissão deve ser uma entidade de segurança diferente da pessoa que executa a instrução. Por exemplo, suponha que o usuário Mary é principal_id 12 e usuário Raul é 15 principal. Mary executa `GRANT SELECT ON OBJECT::X TO Steven WITH GRANT OPTION AS Raul;` agora a tabela database_permissions indicará que o grantor_prinicpal_id foi 15 (Raul), embora na verdade, a instrução foi executada pelo usuário 13 (Mary).

Usando a cláusula geralmente não é recomendado, a menos que você precisa definir explicitamente a cadeia de permissão. Para obter mais informações, consulte o **resumo do algoritmo de verificação de permissão** seção [permissões (mecanismo de banco de dados)](../../relational-databases/security/permissions-database-engine.md).

O uso de como esta instrução não implica a capacidade de representar outro usuário. 
  
## <a name="remarks"></a>Comentários  
 A sintaxe completa da instrução GRANT é complexa. O diagrama de sintaxe acima foi simplificado para chamar atenção para sua estrutura. A sintaxe completa para conceder permissões em protegíveis específicos é descrita nos tópicos listados a seguir.  
  
 A instrução REVOKE pode ser usada para remover permissões concedidas, e a instrução DENY pode ser usada para evitar que uma entidade ganhe uma permissão específica por meio de um GRANT.  
  
 A concessão de uma permissão remove DENY ou REVOKE daquela permissão no protegível especificado. Se a mesma permissão for negada a um escopo mais alto que contém o protegível, o DENY terá precedência. Mas a revogação da permissão concedida em um escopo mais alto não tem precedência.  
  
 Permissões em nível de banco de dados são concedidas dentro do escopo do banco de dados especificado. Se um usuário precisar de permissões em objetos em outro banco de dados, crie a conta de usuário no outro banco de dados ou conceda acesso à conta de usuário no outro banco de dados, bem como no banco de dados atual.  
  
> [!CAUTION]  
>  Um DENY em nível de tabela não tem precedência sobre um GRANT em nível de coluna. Essa inconsistência na hierarquia de permissões foi preservada para manter a compatibilidade com versões anteriores. Ela será removida em uma versão futura.  
  
 O procedimento armazenado do sistema sp_helprotect relata as permissões em um protegível no nível de banco de dados.  
  
## <a name="with-grant-option"></a>WITH GRANT OPTION  
 O **GRANT** ... **COM a opção GRANT** Especifica que a entidade de segurança que recebe a permissão recebe a capacidade de conceder a permissão especificada para outras contas de segurança. Quando a entidade que recebe a permissão é uma função ou um grupo do Windows, o **AS** cláusula deve ser usada quando a permissão de objeto deve ser concedida a usuários que não são membros do grupo ou função. Porque somente um usuário, em vez de um grupo ou função, pode executar uma **GRANT** instrução, um membro específico de grupo ou função deve usar o **AS** cláusula para invocar a associação de função ou grupo explicitamente ao conceder a permissão. A exemplo a seguir mostra como o **WITH GRANT OPTION** é usado quando concedido a uma função ou grupo do Windows.  
  
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
 Para obter um cartaz gráfico dimensionado de todas as permissões do [!INCLUDE[ssDE](../../includes/ssde-md.md)] em formato pdf, veja [http://go.microsoft.com/fwlink/?LinkId=229142](http://go.microsoft.com/fwlink/?LinkId=229142).  
  
## <a name="permissions"></a>Permissões  
 O concessor (ou a entidade de segurança especificada com a opção AS) deve ter a própria permissão com GRANT OPTION ou uma permissão superior que tenha a permissão que está sendo concedida implícita. Se a opção AS for usada, requisitos adicionais se aplicarão. Consulte o tópico específico sobre protegíveis para obter detalhes.  
  
 Os proprietários de objetos podem conceder permissões nos objetos de sua propriedade. Principais com a permissão CONTROL em um item protegível podem conceder permissão nesse item.  
  
 Os usuários autorizados da permissão CONTROL SERVER, como os membros da função de servidor fixa sysadmin, podem conceder qualquer permissão em qualquer protegível do servidor. Os usuários autorizados da permissão CONTROL em um banco de dados, como os membros da função de banco de dados fixa db_owner, podem conceder qualquer permissão para qualquer item de segurança do banco de dados. Os usuários autorizados da permissão CONTROL em um esquema podem conceder qualquer permissão em qualquer objeto dentro do esquema.  
  
## <a name="examples"></a>Exemplos  
 A tabela a seguir lista os protegíveis e os tópicos que descrevem a sintaxe específica de protegíveis.  
  
|||  
|-|-|  
|Função de aplicativo|[CONCEDER permissões de entidade de banco de dados &#40; Transact-SQL &#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md)|  
|Assembly|[CONCEDER permissões de Assembly &#40; Transact-SQL &#41;](../../t-sql/statements/grant-assembly-permissions-transact-sql.md)|  
|Chave assimétrica|[CONCEDER permissões de chave assimétrica &#40; Transact-SQL &#41;](../../t-sql/statements/grant-asymmetric-key-permissions-transact-sql.md)|  
|Grupo de disponibilidade|[Permissões de grupo de disponibilidade GRANT &#40; Transact-SQL &#41;](../../t-sql/statements/grant-availability-group-permissions-transact-sql.md)|  
|Certificado|[Permissões de certificado GRANT &#40; Transact-SQL &#41;](../../t-sql/statements/grant-certificate-permissions-transact-sql.md)|  
|Contrato|[Permissões do GRANT Service Broker &#40; Transact-SQL &#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|Banco de Dados|[Permissões de banco de dados GRANT &#40; Transact-SQL &#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md)|
|Credencial com escopo de banco de dados|[Escopo do banco de dados GRANT credencial (Transact-SQL)](../../t-sql/statements/grant-database-scoped-credential-transact-sql.md)|  
|Ponto de extremidade|[CONCEDER permissões de ponto de extremidade &#40; Transact-SQL &#41;](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md)|  
|Catálogo de texto completo|[Permissões de texto completo GRANT &#40; Transact-SQL &#41;](../../t-sql/statements/grant-full-text-permissions-transact-sql.md)|  
|Lista de palavras irrelevantes de texto completo|[Permissões de texto completo GRANT &#40; Transact-SQL &#41;](../../t-sql/statements/grant-full-text-permissions-transact-sql.md)|  
|Função|[Permissões de objeto GRANT &#40; Transact-SQL &#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|Logon|[CONCEDER permissões de entidade do servidor &#40; Transact-SQL &#41;](../../t-sql/statements/grant-server-principal-permissions-transact-sql.md)|  
|Tipo de mensagem|[Permissões do GRANT Service Broker &#40; Transact-SQL &#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|Objeto|[Permissões de objeto GRANT &#40; Transact-SQL &#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|Fila|[Permissões de objeto GRANT &#40; Transact-SQL &#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|Associação de serviço remoto|[Permissões do GRANT Service Broker &#40; Transact-SQL &#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|Função|[CONCEDER permissões de entidade de banco de dados &#40; Transact-SQL &#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md)|  
|Rota|[Permissões do GRANT Service Broker &#40; Transact-SQL &#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|esquema|[Permissões de esquema GRANT &#40; Transact-SQL &#41;](../../t-sql/statements/grant-schema-permissions-transact-sql.md)|  
|Lista de propriedades de pesquisa|[Permissões de lista de propriedades de pesquisa GRANT &#40; Transact-SQL &#41;](../../t-sql/statements/grant-search-property-list-permissions-transact-sql.md)|  
|Servidor|[Permissões de servidor GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-server-permissions-transact-sql.md)|  
|Serviço|[Permissões do GRANT Service Broker &#40; Transact-SQL &#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|Procedimento armazenado|[Permissões de objeto GRANT &#40; Transact-SQL &#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|Chave simétrica|[CONCEDER permissões de chave simétrica &#40; Transact-SQL &#41;](../../t-sql/statements/grant-symmetric-key-permissions-transact-sql.md)|  
|Sinônimo|[Permissões de objeto GRANT &#40; Transact-SQL &#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|Objetos do sistema|[Permissões de objeto do sistema GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-system-object-permissions-transact-sql.md)|  
|Table|[Permissões de objeto GRANT &#40; Transact-SQL &#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|Tipo|[Tipo de concessão de permissões &#40; Transact-SQL &#41;](../../t-sql/statements/grant-type-permissions-transact-sql.md)|  
|Usuário|[CONCEDER permissões de entidade de banco de dados &#40; Transact-SQL &#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md)|  
|Exibição|[Permissões de objeto GRANT &#40; Transact-SQL &#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|Coleção de esquema XML|[CONCEDER permissões de coleção de esquemas XML &#40; Transact-SQL &#41;](../../t-sql/statements/grant-xml-schema-collection-permissions-transact-sql.md)|  
  
## <a name="see-also"></a>Consulte também  
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_adduser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [sp_changedbowner &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [sp_dropuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [sp_helprotect &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)   
 [sp_helpuser &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)  
  
  

