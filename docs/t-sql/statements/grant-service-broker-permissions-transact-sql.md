---
title: "Permissões do serviço de concessão Broker (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 06/10/2016
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
- granting permissions [SQL Server], Service Broker
- routes [Service Broker], permissions
- Service Broker, permissions
- GRANT statement, Service Broker
- remote service bindings [Service Broker], permissions
- message types [Service Broker], permissions
- contracts [Service Broker], permissions
ms.assetid: c5579976-97c4-4123-be0c-d0b98a9e38fb
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 185950b1872ca5f11663f3d5051d1a2303cce090
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="grant-service-broker-permissions-transact-sql"></a>Permissões GRANT do Agente de Serviços (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Concede permissões em um contrato, tipos de mensagem, associações remotas, rotas ou serviços no Service Broker.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
GRANT permission  [ ,...n ] ON  
    {    
              [ CONTRACT :: contract_name ]   
       | [ MESSAGE TYPE :: message_type_name ]    
       | [ REMOTE SERVICE BINDING :: remote_binding_name ]    
       | [ ROUTE :: route_name ]   
       | [ SERVICE :: service_name ]      
    }  
    TO database_principal [ ,...n ]   
    [ WITH GRANT OPTION ]  
        [ AS granting_principal ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *permissão*  
 Especifica uma permissão que pode ser concedida em um Service Broker protegível.  Listada abaixo.  
  
 CONTRATO **::***contract_name*  
 Especifica o contrato no qual a permissão está sendo concedida. O qualificador de escopo "::" é necessária.  
  
 TIPO de mensagem **::***message_type_name*  
 Especifica o tipo de mensagem no qual a permissão está sendo concedida. O qualificador de escopo "::" é obrigatório.  
  
 A associação de serviço remoto **::***remote_binding_name*  
 Especifica a associação de serviço remoto na qual a permissão está sendo concedida. O qualificador de escopo "::" é obrigatório.  
  
 ROTA **::***route_name*  
 Especifica a rota na qual a permissão está sendo concedida. O qualificador de escopo "::" é obrigatório.  
  
 SERVIÇO **::***service_name*  
 Especifica o serviço no qual a permissão está sendo concedida. O qualificador de escopo "::" é obrigatório.  
  
 *database_principal*  
 Especifica a entidade de segurança para o qual a permissão está sendo concedida. Um dos seguintes:  
  
-   usuário de banco de dados  
  
-   função de banco de dados  
  
-   função de aplicativo  
  
-   usuário de banco de dados mapeado para um logon do Windows  
  
-   usuário de banco de dados mapeado para um grupo do Windows  
  
-   usuário de banco de dados mapeado para um certificado  
  
-   usuário de banco de dados mapeado para uma chave assimétrica  
  
-   usuário de banco de dados não mapeado para uma entidade do servidor.  
  
 GRANT OPTION  
 Indica que o principal também terá a capacidade de conceder a permissão especificada a outros principais.  
  
 *granting_principal*  
 Especifica uma entidade de segurança da qual a entidade de segurança que executa esta consulta deriva seu direito de conceder a permissão. Um dos seguintes:  
  
-   usuário de banco de dados  
  
-   função de banco de dados  
  
-   função de aplicativo  
  
-   usuário de banco de dados mapeado para um logon do Windows  
  
-   usuário de banco de dados mapeado para um grupo do Windows  
  
-   usuário de banco de dados mapeado para um certificado  
  
-   usuário de banco de dados mapeado para uma chave assimétrica  
  
-   usuário de banco de dados não mapeado para uma entidade do servidor.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="service-broker-contracts"></a>Contratos do Agente de Serviços  
 Um contrato do Agente de Serviços é um item protegível do nível do banco de dados contido pelo banco de dados que é seu pai na hierarquia de permissões. As permissões mais específicas e limitadas que podem ser concedidas em um contrato do Agente de Serviços são listadas a seguir, junto com as permissões mais gerais que as contêm implicitamente.  
  
|Permissão do contrato do Agente de Serviços|Indicado pela permissão do contrato do Agente de Serviços|Implícito na permissão de banco de dados|  
|----------------------------------------|---------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY CONTRACT|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="service-broker-message-types"></a>Tipos de mensagem do Agente de Serviços  
 Um tipo de mensagem do Agente de Serviços é um item protegível do nível do banco de dados contido pelo banco de dados que é seu pai na hierarquia de permissões. As permissões mais específicas e limitadas que podem ser concedidas em um tipo de mensagem do Agente de Serviços são listadas a seguir, junto com as permissões mais gerais que as contêm implicitamente.  
  
|Permissão do tipo de mensagem do Agente de Serviços|Indicado pela permissão do tipo de mensagem do Agente de Serviços|Implícito na permissão de banco de dados|  
|--------------------------------------------|-------------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY MESSAGE TYPE|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="service-broker-remote-service-bindings"></a>Associações de serviço remoto do Agente de Serviços  
 Uma associação de serviço remoto do Agente de Serviços é um item protegível do nível do banco de dados contido pelo banco de dados que é seu pai na hierarquia de permissões. As permissões mais específicas e limitadas que podem ser concedidas em uma associação de serviço remoto do Agente de Serviços são listadas a seguir, junto com as permissões mais gerais que as contêm implicitamente.  
  
|Permissão da associação de serviço remoto do Agente de Serviços|Indicado pela permissão da associação de serviço remoto do Agente de Serviços|Implícito na permissão de banco de dados|  
|------------------------------------------------------|-----------------------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY REMOTE SERVICE BINDING|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="service-broker-routes"></a>Rotas do Agente de Serviços  
 Uma rota do Agente de Serviços é um item protegível do nível do banco de dados contido pelo banco de dados que é seu pai na hierarquia de permissões. As permissões mais específicas e limitadas que podem ser concedidas em uma rota do Agente de Serviços são listadas a seguir, junto com as permissões mais gerais que as contêm implicitamente.  
  
|Permissão da rota do Agente de Serviços|Indicado pela permissão da rota do Agente de Serviços|Implícito na permissão de banco de dados|  
|-------------------------------------|------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ROUTE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
### <a name="service-broker-services"></a>Serviços do Agente de Serviços  
 Um serviço do Agente de Serviços é um item protegível do nível do banco de dados contido pelo banco de dados que é seu pai na hierarquia de permissões. As permissões mais específicas e limitadas que podem ser concedidas em um serviço do Agente de Serviços são listadas a seguir, junto com as permissões mais gerais que as contêm implicitamente.  
  
|Permissão do serviço do Agente de Serviços|Indicado pela permissão do serviço do Agente de Serviços|Implícito na permissão de banco de dados|  
|---------------------------------------|--------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|SEND|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY SERVICE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissões  
 O concessor (ou a entidade de segurança especificada com a opção AS) deve ter a própria permissão com GRANT OPTION ou uma permissão superior que tenha a permissão que está sendo concedida implícita.  
  
 Se a opção AS for usada, esses requisitos adicionais se aplicarão.  
  
|AS *granting_principal*|Permissão adicional necessária|  
|------------------------------|------------------------------------|  
|Usuário de banco de dados|Permissão IMPERSONATE no usuário, associação a **db_securityadmin** função fixa de banco de dados, associação ao **db_owner** fixo de função de banco de dados ou associação no **sysadmin** função de servidor fixa.|  
|Usuário de banco de dados mapeado para um logon do Windows|Permissão IMPERSONATE no usuário, associação a **db_securityadmin** função fixa de banco de dados, associação ao **db_owner** fixo de função de banco de dados ou associação no **sysadmin** função de servidor fixa.|  
|Usuário de banco de dados mapeado para um grupo do Windows|Associação no grupo do Windows, associação a **db_securityadmin** função fixa de banco de dados, associação ao **db_owner** fixo de função de banco de dados ou associação no **sysadmin**função de servidor fixa.|  
|Usuário de banco de dados mapeado para um certificado|Associação a **db_securityadmin** função fixa de banco de dados, associação ao **db_owner** fixo de função de banco de dados ou associação no **sysadmin** função de servidor fixa.|  
|Usuário de banco de dados mapeado para uma chave assimétrica|Associação a **db_securityadmin** função fixa de banco de dados, associação ao **db_owner** fixo de função de banco de dados ou associação no **sysadmin** função de servidor fixa.|  
|Usuário de banco de dados não mapeado para nenhuma entidade de segurança de servidor|Permissão IMPERSONATE no usuário, associação a **db_securityadmin** função fixa de banco de dados, associação ao **db_owner** fixo de função de banco de dados ou associação no **sysadmin** função de servidor fixa.|  
|Função de banco de dados|A permissão ALTER na função, associação no **db_securityadmin** função fixa de banco de dados, associação ao **db_owner** fixo de função de banco de dados, ou a associação a **sysadmin**função de servidor fixa.|  
|Função de aplicativo|A permissão ALTER na função, associação no **db_securityadmin** função fixa de banco de dados, associação ao **db_owner** fixo de função de banco de dados, ou a associação a **sysadmin**função de servidor fixa.|  
  
 Os proprietários de objetos podem conceder permissões nos objetos de sua propriedade. Principais com a permissão CONTROL em um item protegível podem conceder permissão nesse item.  
  
 Os usuários autorizados da permissão CONTROL SERVER, como os membros do **sysadmin** função de servidor fixa, podem conceder qualquer permissão em qualquer protegível do servidor. Os usuários autorizados da permissão CONTROL em um banco de dados, como os membros do **db_owner** função de banco de dados fixa, podem conceder qualquer permissão em qualquer protegível no banco de dados. Os usuários autorizados da permissão CONTROL em um esquema podem conceder qualquer permissão em qualquer objeto dentro do esquema.  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  

