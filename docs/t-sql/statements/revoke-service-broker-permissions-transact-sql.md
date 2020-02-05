---
title: Permissões REVOKE do Service Broker (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- routes [Service Broker], permissions
- Service Broker, permissions
- remote service bindings [Service Broker], permissions
- permissions [Service Broker]
- message types [Service Broker], permissions
- contracts [Service Broker], permissions
- services [Service Broker], permissions
- REVOKE statement, Service Broker
ms.assetid: 70f1d938-97e2-48a4-9bc0-8be9f2f2c36d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 4ed6e67bbf6f3fcda872650c2d3394d6311802b3
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "67914221"
---
# <a name="revoke-service-broker-permissions-transact-sql"></a>Permissões REVOKE do Service Broker (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Revoga as permissões em contratos, tipos de mensagem, ligações de serviços remotos, rotas ou serviços do [!INCLUDE[ssSB](../../includes/sssb-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
REVOKE [ GRANT OPTION FOR ] permission [ ,...n ] ON  
    {   
       [ CONTRACT :: contract_name ]   
       | [ MESSAGE TYPE :: message_type_name ]    
       | [ REMOTE SERVICE BINDING :: remote_binding_name ]    
       | [ ROUTE :: route_name ]   
       | [ SERVICE :: service_name ]      
        }  
    { TO | FROM } database_principal [ ,...n ]  
    [ CASCADE ]  
    [ AS revoking_principal ]  
```  
  
## <a name="arguments"></a>Argumentos  
 GRANT OPTION FOR  
 Indica que o direito de conceder a permissão especificada diretamente a outros principais será revogado. A permissão em si não será revogada.  
  
> [!IMPORTANT]  
>  Se a entidade de segurança tiver a permissão especificada sem a opção GRANT, a própria permissão será revogada.  
  
 *permission*  
 Especifica uma permissão que pode ser revogada em um protegível do [!INCLUDE[ssSB](../../includes/sssb-md.md)]. Para obter uma lista dessas permissões, consulte a seção Comentários mais adiante neste tópico.  
  
 CONTRACT **::** _contract_name_  
 Especifica o contrato no qual a permissão está sendo revogada. O qualificador de escopo **::** é obrigatório.  
  
 MESSAGE TYPE **::** _message_type_name_  
 Especifica o tipo de mensagem no qual a permissão está sendo revogada. O qualificador de escopo **::** é obrigatório.  
  
 REMOTE SERVICE BINDING **::** _remote_binding_name_  
 Especifica a associação de serviço remoto na qual a permissão está sendo revogada. O qualificador de escopo **::** é obrigatório.  
  
 ROUTE **::** _route_name_  
 Especifica o roteamento no qual a permissão está sendo revogada. O qualificador de escopo **::** é obrigatório.  
  
 SERVICE **::** _message_type_name_  
 Especifica o serviço no qual a permissão está sendo revogada. O qualificador de escopo **::** é obrigatório.  
  
 *database_principal*  
 Especifica a entidade a partir da qual a permissão está sendo revogada. *database_principal* pode ser um dos seguintes:  
  
-   Usuário de banco de dados  
  
-   Função de banco de dados  
  
-   Função de aplicativo  
  
-   Usuário de banco de dados mapeado para um logon do Windows  
  
-   Usuário de banco de dados mapeado para um grupo do Windows  
  
-   Usuário de banco de dados mapeado para um certificado  
  
-   Usuário de banco de dados mapeado para uma chave assimétrica  
  
-   Usuário do banco de dados não mapeado para um principal de servidor.  
  
 CASCADE  
 Indica que a permissão que está sendo revogada também é revogada de outros principais aos quais ela foi concedida ou negada por esse principal.  
  
> [!CAUTION]  
>  A revogação em cascata de uma permissão WITH GRANT OPTION concedida revogará as opções GRANT e DENY dessa permissão.  
  
 AS *revoking_principal*  
 Especifica uma entidade de segurança da qual a entidade de segurança que está executando essa consulta deriva seu direito de revogar a permissão. *revoking_principal* pode ser um dos seguintes:  
  
-   Usuário de banco de dados  
  
-   Função de banco de dados  
  
-   Função de aplicativo  
  
-   Usuário de banco de dados mapeado para um logon do Windows  
  
-   Usuário de banco de dados mapeado para um grupo do Windows  
  
-   Usuário de banco de dados mapeado para um certificado  
  
-   Usuário de banco de dados mapeado para uma chave assimétrica  
  
-   Usuário do banco de dados não mapeado para um principal de servidor.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="service-broker-contracts"></a>Contratos do Agente de Serviços  
 Um contrato do [!INCLUDE[ssSB](../../includes/sssb-md.md)] é um protegível no nível do banco de dados contido pelo banco de dados que é seu pai na hierarquia de permissões. As permissões mais específicas e limitadas que podem ser revogadas em um contrato do [!INCLUDE[ssSB](../../includes/sssb-md.md)] são listadas na tabela a seguir, junto com as permissões mais gerais que as incluem implicitamente.  
  
|Permissão do contrato do Agente de Serviços|Indicado pela permissão do contrato do Agente de Serviços|Implícito na permissão de banco de dados|  
|----------------------------------------|---------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY CONTRACT|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="service-broker-message-types"></a>Tipos de mensagem do Agente de Serviços  
 Um tipo de mensagem do [!INCLUDE[ssSB](../../includes/sssb-md.md)] é um protegível em nível de banco de dados contido no banco de dados pai da hierarquia de permissões. As permissões mais específicas e limitadas que podem ser revogadas em um tipo de mensagem do [!INCLUDE[ssSB](../../includes/sssb-md.md)] são listadas na tabela a seguir, junto com as permissões mais gerais que as incluem implicitamente.  
  
|Permissão do tipo de mensagem do Agente de Serviços|Indicado pela permissão do tipo de mensagem do Agente de Serviços|Implícito na permissão de banco de dados|  
|--------------------------------------------|-------------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY MESSAGE TYPE|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="service-broker-remote-service-bindings"></a>Associações de serviço remoto do Agente de Serviços  
 Uma associação de serviço remoto do [!INCLUDE[ssSB](../../includes/sssb-md.md)] é um protegível em nível de banco de dados contido no banco de dados pai da hierarquia de permissões. As permissões mais específicas e limitadas que podem ser revogadas em uma associação de serviço remoto do [!INCLUDE[ssSB](../../includes/sssb-md.md)] são listadas na tabela a seguir, junto com as permissões mais gerais que as incluem implicitamente.  
  
|Permissão da associação de serviço remoto do Agente de Serviços|Indicado pela permissão da associação de serviço remoto do Agente de Serviços|Implícito na permissão de banco de dados|  
|------------------------------------------------------|-----------------------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY REMOTE SERVICE BINDING|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="service-broker-routes"></a>Rotas do Agente de Serviços  
 Uma rota do [!INCLUDE[ssSB](../../includes/sssb-md.md)] é um protegível em nível de banco de dados contido no banco de dados pai da hierarquia de permissões. As permissões mais específicas e limitadas que podem ser revogadas em uma rota do [!INCLUDE[ssSB](../../includes/sssb-md.md)] são listadas na tabela a seguir, junto com as permissões mais gerais que as contêm implicitamente.  
  
|Permissão da rota do Agente de Serviços|Indicado pela permissão da rota do Agente de Serviços|Implícito na permissão de banco de dados|  
|-------------------------------------|------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ROUTE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
### <a name="service-broker-services"></a>Serviços do Agente de Serviços  
 Um serviço do [!INCLUDE[ssSB](../../includes/sssb-md.md)] é um protegível em nível de banco de dados contido no banco de dados pai da hierarquia de permissões. As permissões mais específicas e limitadas que podem ser revogadas em um serviço do [!INCLUDE[ssSB](../../includes/sssb-md.md)] são listadas na tabela a seguir, junto com as permissões mais gerais que as incluem implicitamente.  
  
|Permissão do serviço do Agente de Serviços|Indicado pela permissão do serviço do Agente de Serviços|Implícito na permissão de banco de dados|  
|---------------------------------------|--------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|SEND|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY SERVICE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão de CONTROL no contrato, tipo de mensagem, associação de serviço remoto, rota ou serviço do [!INCLUDE[ssSB](../../includes/sssb-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [Permissões GRANT do Service Broker &#40;Transact-SQL&#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)   
 [Permissões DENY do Service Broker &#40;Transact-SQL&#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
