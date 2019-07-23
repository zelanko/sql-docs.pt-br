---
title: Permissões DENY do Service Broker (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/09/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- denying permissions [Service Broker]
- routes [Service Broker], permissions
- Service Broker, permissions
- DENY statement, Service Broker
- remote service bindings [Service Broker], permissions
- permissions [Service Broker]
- message types [Service Broker], permissions
- denying permissions [SQL Server], Service Broker
- contracts [Service Broker], permissions
- services [Service Broker], permissions
ms.assetid: 7c6de71b-865c-41db-9413-ad9b3562e579
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 346044530087c40c468abe9d304231ce06220845
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67984426"
---
# <a name="deny-service-broker-permissions-transact-sql"></a>Permissões DENY do Service Broker (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Nega as permissões em contratos, tipos de mensagem, ligações de serviço remoto, rotas ou serviços do [!INCLUDE[ssSB](../../includes/sssb-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
DENY permission  [ ,...n ] ON  
    {    
       [ CONTRACT :: contract_name ]   
       | [ MESSAGE TYPE :: message_type_name ]    
       | [ REMOTE SERVICE BINDING :: remote_binding_name ]    
       | [ ROUTE :: route_name ]   
       | [ SERVICE :: service_name ]      
        }  
    TO database_principal [ ,...n ]   
    [ CASCADE ]  
        [ AS denying_principal ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *permission*  
 Especifica uma permissão que pode ser negada em um protegível do [!INCLUDE[ssSB](../../includes/sssb-md.md)]. Para obter uma lista de permissões, consulte a seção Comentários mais adiante neste tópico.  
  
 CONTRACT **::** _contract_name_  
 Especifica o contrato no qual a permissão está sendo negada. O qualificador de escopo **::** é obrigatório.  
  
 MESSAGE TYPE **::** _message_type_name_  
 Especifica o tipo de mensagem no qual a permissão está sendo negada. O qualificador de escopo **::** é obrigatório.  
  
 REMOTE SERVICE BINDING **::** _remote_binding_name_  
 Especifica a associação de serviço remoto na qual a permissão está sendo negada. O qualificador de escopo **::** é obrigatório.  
  
 ROUTE **::** _route_name_  
 Especifica o roteamento no qual a permissão está sendo negada. O qualificador de escopo **::** é obrigatório.  
  
 SERVICE **::** _message_type_name_  
 Especifica o serviço no qual a permissão está sendo negada. O qualificador de escopo **::** é obrigatório.  
  
 *database_principal*  
 Especifica a entidade à qual a permissão está sendo negada. Um dos seguintes:  
  
-   Usuário de banco de dados  
-   Função de banco de dados  
-   Função de aplicativo  
-   Usuário de banco de dados mapeado para um logon do Windows  
-   Usuário de banco de dados mapeado para um grupo do Windows  
-   Usuário de banco de dados mapeado para um certificado  
-   Usuário de banco de dados mapeado para uma chave assimétrica  
-   Usuário do banco de dados não mapeado para um principal de servidor.  
  
CASCADE  
 Indica que a permissão que está sendo negada também é negada a outros principais aos quais ela foi concedida por esse principal.  
  
*denying_principal*  
 Especifica uma entidade de segurança da qual a entidade de segurança que executa essa consulta deriva seu direito de negar a permissão. Um dos seguintes:  
  
-   Usuário de banco de dados  
-   Função de banco de dados  
-   Função de aplicativo  
-   Usuário de banco de dados mapeado para um logon do Windows  
-   Usuário de banco de dados mapeado para um grupo do Windows  
-   Usuário de banco de dados mapeado para um certificado  
-   Usuário de banco de dados mapeado para uma chave assimétrica  
-   Usuário do banco de dados não mapeado para um principal de servidor.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="service-broker-contracts"></a>Contratos do Agente de Serviços  
 Um contrato do [!INCLUDE[ssSB](../../includes/sssb-md.md)] é um protegível em nível de banco de dados contido no banco de dados pai da hierarquia de permissões. As permissões mais específicas e limitadas que podem ser negadas em um contrato do [!INCLUDE[ssSB](../../includes/sssb-md.md)] são listadas na tabela a seguir, junto com as permissões mais gerais que as incluem implicitamente.  
  
|Permissão do contrato do Agente de Serviços|Indicado pela permissão do contrato do Agente de Serviços|Implícito na permissão de banco de dados|  
|----------------------------------------|---------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY CONTRACT|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="service-broker-message-types"></a>Tipos de mensagem do Agente de Serviços  
 Um tipo de mensagem do [!INCLUDE[ssSB](../../includes/sssb-md.md)] é um protegível em nível de banco de dados contido no banco de dados pai da hierarquia de permissões. As permissões mais específicas e limitadas que podem ser negadas em um tipo de mensagem do [!INCLUDE[ssSB](../../includes/sssb-md.md)] são listadas na tabela a seguir, junto com as permissões mais gerais que as incluem implicitamente.  
  
|Permissão do tipo de mensagem do Agente de Serviços|Indicado pela permissão do tipo de mensagem do Agente de Serviços|Implícito na permissão de banco de dados|  
|--------------------------------------------|-------------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY MESSAGE TYPE|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="service-broker-remote-service-bindings"></a>Associações de serviço remoto do Agente de Serviços  
 Uma associação de serviço remoto do [!INCLUDE[ssSB](../../includes/sssb-md.md)] é um protegível em nível de banco de dados contido no banco de dados pai da hierarquia de permissões. As permissões mais específicas e limitadas que podem ser negadas em uma associação de serviço remoto do [!INCLUDE[ssSB](../../includes/sssb-md.md)] são listadas na tabela a seguir, junto com as permissões mais gerais que as incluem implicitamente.  
  
|Permissão da associação de serviço remoto do Agente de Serviços|Indicado pela permissão da associação de serviço remoto do Agente de Serviços|Implícito na permissão de banco de dados|  
|------------------------------------------------------|-----------------------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY REMOTE SERVICE BINDING|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="service-broker-routes"></a>Rotas do Agente de Serviços  
 Uma rota do [!INCLUDE[ssSB](../../includes/sssb-md.md)] é um protegível em nível de banco de dados contido no banco de dados pai da hierarquia de permissões. As permissões mais específicas e limitadas que podem ser negadas em uma rota do [!INCLUDE[ssSB](../../includes/sssb-md.md)] são listadas na tabela a seguir, junto com as permissões mais gerais que as contêm implicitamente.  
  
|Permissão da rota do Agente de Serviços|Indicado pela permissão da rota do Agente de Serviços|Implícito na permissão de banco de dados|  
|-------------------------------------|------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ROUTE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
### <a name="service-broker-services"></a>Serviços do Agente de Serviços  
 Um serviço do [!INCLUDE[ssSB](../../includes/sssb-md.md)] é um protegível em nível de banco de dados contido no banco de dados pai da hierarquia de permissões. As permissões mais específicas e limitadas que podem ser negadas em um serviço do [!INCLUDE[ssSB](../../includes/sssb-md.md)] são listadas na tabela a seguir, junto com as permissões mais gerais que as contêm implicitamente.  
  
|Permissão do serviço do Agente de Serviços|Indicado pela permissão do serviço do Agente de Serviços|Implícito na permissão de banco de dados|  
|---------------------------------------|--------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|SEND|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY SERVICE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissões  
 Exige a permissão CONTROL no contrato, tipo de mensagem, associação de serviço remoto, rota ou serviço do [!INCLUDE[ssSB](../../includes/sssb-md.md)]. Se a cláusula AS for usada, o principal especificado deverá ser proprietário do protegível no qual as permissões estão sendo negadas.  
  
## <a name="see-also"></a>Consulte Também  
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Permissões REVOKE do Service Broker &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-service-broker-permissions-transact-sql.md)   
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-database-engine.md)  
  
  
