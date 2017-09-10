---
title: "Negar permissões do Service Broker (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 06/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ed0ab0e375ecddbf9086647adce744a8ef4cb53d
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="deny-service-broker-permissions-transact-sql"></a>Permissões DENY do Service Broker (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Nega as permissões em contratos, tipos de mensagem, ligações de serviço remoto, rotas ou serviços do [!INCLUDE[ssSB](../../includes/sssb-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 *permissão*  
 Especifica uma permissão que pode ser negada em um protegível do [!INCLUDE[ssSB](../../includes/sssb-md.md)]. Para obter uma lista de permissões, consulte a seção Comentários mais adiante neste tópico.  
  
 CONTRATO **::***contract_name*  
 Especifica o contrato no qual a permissão está sendo negada. O qualificador de escopo **::** é necessária.  
  
 TIPO de mensagem **::***message_type_name*  
 Especifica o tipo de mensagem no qual a permissão está sendo negada. O qualificador de escopo **::** é necessária.  
  
 A associação de serviço remoto **::***remote_binding_name*  
 Especifica a associação de serviço remoto na qual a permissão está sendo negada. O qualificador de escopo **::** é necessária.  
  
 ROTA **::***route_name*  
 Especifica o roteamento no qual a permissão está sendo negada. O qualificador de escopo **::** é necessária.  
  
 SERVIÇO **::***message_type_name*  
 Especifica o serviço no qual a permissão está sendo negada. O qualificador de escopo **::** é necessária.  
  
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
  
## <a name="remarks"></a>Comentários  
  
## <a name="service-broker-contracts"></a>Contratos do Agente de Serviços  
 Um contrato do [!INCLUDE[ssSB](../../includes/sssb-md.md)] é um protegível em nível de banco de dados contido no banco de dados pai da hierarquia de permissões. Mais permissões específicas e limitadas que podem ser negadas em um [!INCLUDE[ssSB](../../includes/sssb-md.md)] contrato são listados na tabela a seguir, junto com as permissões mais gerais que as incluem implicitamente.  
  
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
 Uma rota do [!INCLUDE[ssSB](../../includes/sssb-md.md)] é um protegível em nível de banco de dados contido no banco de dados pai da hierarquia de permissões. Mais permissões específicas e limitadas que podem ser negadas em um [!INCLUDE[ssSB](../../includes/sssb-md.md)] rota são listados na tabela a seguir, junto com as permissões mais gerais que as incluem implicitamente.  
  
|Permissão da rota do Agente de Serviços|Indicado pela permissão da rota do Agente de Serviços|Implícito na permissão de banco de dados|  
|-------------------------------------|------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ROUTE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
### <a name="service-broker-services"></a>Serviços do Agente de Serviços  
 Um serviço do [!INCLUDE[ssSB](../../includes/sssb-md.md)] é um protegível em nível de banco de dados contido no banco de dados pai da hierarquia de permissões. Mais permissões específicas e limitadas que podem ser negadas em um [!INCLUDE[ssSB](../../includes/sssb-md.md)] serviço são listados na tabela a seguir, junto com as permissões mais gerais que as incluem implicitamente.  
  
|Permissão do serviço do Agente de Serviços|Indicado pela permissão do serviço do Agente de Serviços|Implícito na permissão de banco de dados|  
|---------------------------------------|--------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|SEND|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY SERVICE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissões  
 Exige permissão CONTROL para o [!INCLUDE[ssSB](../../includes/sssb-md.md)] contrato, tipo de mensagem, associação de serviço remoto, rota ou serviço. Se a cláusula AS for usada, o principal especificado deverá ser proprietário do protegível no qual as permissões estão sendo negadas.  
  
## <a name="see-also"></a>Consulte também  
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [REVOGAR permissões do Service Broker &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-service-broker-permissions-transact-sql.md)   
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [Permissões &#40; mecanismo de banco de dados &#41;](../../relational-databases/security/permissions-database-engine.md)  
  
  

