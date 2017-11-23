---
title: "REVOGAR permissões de ponto de extremidade (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- endpoints [SQL Server], permissions
- REVOKE statement, endpoints
- permissions [SQL Server], endpoints
ms.assetid: 826f513e-9ad0-46b9-87ad-7525713638c8
caps.latest.revision: "24"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a02fa4d0d19e52599b8b148410e099f989afe4f3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="revoke-endpoint-permissions-transact-sql"></a>Permissões de ponto de extremidade REVOKE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Revoga permissões concedidas ou negadas em um ponto de extremidade.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
REVOKE [ GRANT OPTION FOR ] permission [ ,...n ]   
    ON ENDPOINT :: endpoint_name  
    { FROM | TO } <server_principal> [ ,...n ]  
    [ CASCADE ]  
    [ AS SQL_Server_login ]   
  
<server_principal> ::=   
        SQL_Server_login  
    | SQL_Server_login_from_Windows_login   
    | SQL_Server_login_from_certificate   
    | SQL_Server_login_from_AsymKey  
```  
  
## <a name="arguments"></a>Argumentos  
 *permissão*  
 Especifica uma permissão que pode ser concedida em um ponto de extremidade. Para obter uma lista de permissões, consulte a seção Comentários mais adiante neste tópico.  
  
 NO ponto de EXTREMIDADE **::***endpoint_name*  
 Especifica o ponto de extremidade no qual a permissão está sendo concedida. O qualificador de escopo (**::**) é necessária.  
  
 {DO | PARA} \<server_principal > especifica o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon a partir do qual a permissão está sendo revogada.  
  
 *SQL_Server_login*  
 Especifica o nome de um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *SQL_Server_login_from_Windows_login*  
 Especifica o nome de um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criado a partir de um logon do Windows.  
  
 *SQL_Server_login_from_certificate*  
 Especifica o nome de um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mapeado para um certificado.  
  
 *SQL_Server_login_from_AsymKey*  
 Especifica o nome de um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mapeado para uma chave assimétrica.  
  
 GRANT OPTION  
 Indica que o direito de conceder a permissão especificada a outros principais será revogado. A permissão em si não será revogada.  
  
> [!IMPORTANT]  
>  Se a entidade de segurança tiver a permissão especificada sem a opção GRANT, a própria permissão será revogada.  
  
 CASCADE  
 Indica que a permissão que está sendo revogada também é revogada de outros principais aos quais ela foi concedida ou negada por esse principal.  
  
> [!CAUTION]  
>  A revogação em cascata de uma permissão WITH GRANT OPTION concedida revogará as opções GRANT e DENY dessa permissão.  
  
 AS *SQL_Server_login*  
 Especifica o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a partir do qual o principal que executa esta consulta deriva seu direito de revogar a permissão.  
  
## <a name="remarks"></a>Comentários  
 As permissões no escopo do servidor podem ser revogadas somente quando o banco de dados atual é **mestre**.  
  
 Informações sobre pontos de extremidade são visíveis no [Endpoints](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md) exibição do catálogo. Informações sobre permissões de servidor são visíveis no [server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) exibição de catálogo e obter informações sobre as entidades de servidor é visível no [sys. server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) exibição do catálogo.  
  
 Um ponto de extremidade é um protegível em nível de servidor. As permissões mais específicas e limitadas que podem ser revogadas em um ponto de extremidade são listadas na tabela a seguir, junto com as permissões mais gerais que as incluem implicitamente.  
  
|Permissão de ponto de extremidade|Indicado pela permissão de ponto de extremidade|Implícito na permissão de servidor|  
|-------------------------|------------------------------------|----------------------------------|  
|ALTER|CONTROL|ALTER ANY ENDPOINT|  
|CONNECT|CONTROL|CONTROL SERVER|  
|CONTROL|CONTROL|CONTROL SERVER|  
|TAKE OWNERSHIP|CONTROL|CONTROL SERVER|  
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|  
  
## <a name="permissions"></a>Permissões  
 Requer permissão CONTROL no ponto de extremidade ou a permissão ALTER ANY ENDPOINT no servidor.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-revoking-view-definition-permission-on-an-endpoint"></a>A. Revogando a permissão VIEW DEFINITION em um ponto de extremidade  
 O exemplo a seguir revoga a permissão `VIEW DEFINITION` no ponto de extremidade `Mirror7` do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon `ZArifin`.  
  
```  
USE master;  
REVOKE VIEW DEFINITION ON ENDPOINT::Mirror7 FROM ZArifin;  
GO  
```  
  
### <a name="b-revoking-take-ownership-permission-with-the-cascade-option"></a>B. Revogando a permissão TAKE OWNERSHIP com a opção CASCADE  
 O exemplo a seguir revoga `TAKE OWNERSHIP` permissão no ponto de extremidade `Shipping83` do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usuário `PKomosinski` e de todas as entidades às quais `PKomosinski` concedidas `TAKE OWNERSHIP` em `Shipping83`.  
  
```  
USE master;  
REVOKE TAKE OWNERSHIP ON ENDPOINT::Shipping83 FROM PKomosinski   
    CASCADE;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Permissões GRANT do ponto de extremidade &#40;Transact-SQL&#41;](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md)   
 [Negar permissões de ponto de extremidade &#40; Transact-SQL &#41;](../../t-sql/statements/deny-endpoint-permissions-transact-sql.md)   
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)   
 [Exibições do catálogo de pontos de extremidade &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)   
 [sys. Endpoints &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md)   
 [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  

