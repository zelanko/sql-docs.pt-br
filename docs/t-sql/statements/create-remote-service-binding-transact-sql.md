---
title: CREATE REMOTE SERVICE BINDING (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE REMOTE SERVICE BINDING
- SERVICE_BINDING_TSQL
- CREATE REMOTE SERVICE
- REMOTE_TSQL
- CREATE_REMOTE_SERVICE_BINDING_TSQL
- CREATE_REMOTE_SERVICE_TSQL
- BINDING
- SERVICE BINDING
- BINDING_TSQL
- CREATE_REMOTE_TSQL
- REMOTE_SERVICE_TSQL
- CREATE REMOTE
- REMOTE SERVICE
- REMOTE_SERVICE_BINDING_TSQL
- REMOTE
- REMOTE SERVICE BINDING
dev_langs:
- TSQL
helpviewer_keywords:
- binding remote service [Service Broker]
- dialog security [Service Broker]
- end-to-end security [Service Broker]
- security [Service Broker], remote service bindings
- CREATE REMOTE SERVICE BINDING statement
- conversation security [Service Broker]
- remote service bindings [Service Broker], creating
ms.assetid: 4165c404-4d50-4063-9a6e-6e267d309376
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 2fc021cec09a7f62d05f5e435db9d6fc2597fce3
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68117338"
---
# <a name="create-remote-service-binding-transact-sql"></a>CREATE REMOTE SERVICE BINDING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria uma associação que define as credenciais de segurança a serem usadas para iniciar uma conversa com um serviço remoto.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CREATE REMOTE SERVICE BINDING binding_name   
   [ AUTHORIZATION owner_name ]   
   TO SERVICE 'service_name'   
   WITH  USER = user_name [ , ANONYMOUS = { ON | OFF } ]  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *binding_name*  
 É o nome da associação de serviço remoto a ser criada. Os nomes de servidor, banco de dados e esquema não podem ser especificados. O *binding_name* deve ser um **sysname** válido.  
  
 AUTHORIZATION *owner_name*  
 Define o proprietário da associação à função ou ao usuário de banco de dados especificado. Quando o usuário atual é **dbo** ou **sa**, *owner_name* pode ser o nome de qualquer usuário ou função válida. Caso contrário, *owner_name* deverá ser o nome do usuário atual, o nome de um usuário para o qual o usuário atual tenha permissões IMPERSONATE ou o nome de uma função à qual o usuário atual pertença.  
  
 TO SERVICE '*service_name*'  
 Especifica o serviço remoto a ser associado ao usuário identificado na cláusula WITH USER.  
  
 USER = *user_name*  
 Especifica a entidade de banco de dados proprietária do certificado associado ao serviço remoto identificado pela cláusula TO SERVICE. Esse certificado é usado para criptografia e autenticação de mensagens trocadas com o serviço remoto.  
  
 ANONYMOUS  
 Especifica se a autenticação anônima é usada durante a comunicação com o serviço remoto. Se ANONYMOUS = ON, a autenticação anônima será usada e as operações no banco de dados remoto ocorrerão como um membro da função de banco de dados fixa **public**. Se ANONYMOUS = OFF, as operações no banco de dados remoto ocorrerão como um usuário específico nesse banco de dados. Se essa cláusula não for especificada, o padrão será OFF.  
  
## <a name="remarks"></a>Comentários  
 O [!INCLUDE[ssSB](../../includes/sssb-md.md)] usa uma associação de serviço remoto para localizar o certificado a ser usado para uma nova conversa. A chave pública no certificado associado a *user_name* é usada para autenticar as mensagens enviadas ao serviço remoto e para criptografar uma chave da sessão que, em seguida, é usada para criptografar a conversa. O certificado de *owner_name* deve corresponder ao certificado de um usuário no banco de dados que hospeda o serviço remoto.  
  
 A associação de serviço remoto é necessária apenas para serviços iniciadores que se comunicam com serviços de destino fora da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Um banco de dados que hospeda um serviço iniciador deve conter associações de serviço remoto para quaisquer serviços de destino fora da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Um banco de dados que hospeda um serviço de destino deve conter associações de serviço remoto para os serviços iniciadores que se comunicam com o serviço de destino. Quando os serviços iniciador e de destino estão na mesma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], nenhuma associação de serviço remoto é necessária. Entretanto, se uma associação de serviço remoto estiver presente em que o *service_name* especificado para TO SERVICE corresponde ao nome do serviço local, o [!INCLUDE[ssSB](../../includes/sssb-md.md)] usará a associação.  
  
 Quando ANONYMOUS = ON, o serviço iniciador se conecta ao serviço de destino como membro da função de banco de dados fixa **public**. Por padrão, os membros dessa função não têm permissão para conectar-se a um banco de dados. Para enviar uma mensagem com êxito, o banco de dados de destino deve conceder à função **public** a permissão CONNECT para o banco de dados e a permissão SEND para o serviço de destino.  
  
 Quando um usuário possui mais de um certificado, o [!INCLUDE[ssSB](../../includes/sssb-md.md)] seleciona o certificado com a data de validade mais recente dentre os que estão válidos e marcados como AVAILABLE FOR BEGIN_DIALOG.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, as permissões para criar uma associação de serviço remoto correspondem ao usuário nomeado na cláusula USER, membros da função de banco de dados fixa **db_owner**, membros da função de banco de dados fixa **db_ddladmin** e membros da função de servidor fixa **sysadmin**.  
  
 O usuário que executa a instrução CREATE REMOTE SERVICE BINDING deve ter a permissão de representação para a entidade especificada na instrução.  
  
 Uma associação de serviço remoto pode não ser um objeto temporário. Nomes de associação de serviço remoto que começam com **#** são permitidos, mas são objetos permanentes.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-remote-service-binding"></a>a. Criando uma associação de serviço remoto  
 O exemplo a seguir cria uma associação para o serviço `//Adventure-Works.com/services/AccountsPayable`. O [!INCLUDE[ssSB](../../includes/sssb-md.md)] usa o certificado de propriedade da entidade de banco de dados `APUser` para se autenticar no serviço remoto e trocar a chave de criptografia de sessão com o serviço remoto.  
  
```  
CREATE REMOTE SERVICE BINDING APBinding  
    TO SERVICE '//Adventure-Works.com/services/AccountsPayable'  
    WITH USER = APUser ;  
```  
  
### <a name="b-creating-a-remote-service-binding-using-anonymous-authentication"></a>B. Criando uma associação de serviço remoto que usa autenticação anônima  
 O exemplo a seguir cria uma associação para o serviço `//Adventure-Works.com/services/AccountsPayable`. O [!INCLUDE[ssSB](../../includes/sssb-md.md)] usa o certificado de propriedade da entidade de banco de dados `APUser` para trocar a chave de criptografia de sessão com o serviço remoto. O agente não faz autenticação no serviço remoto. No banco de dados que hospeda o serviço remoto, as mensagens são entregues como o usuário **guest**.  
  
```  
CREATE REMOTE SERVICE BINDING APBinding  
    TO SERVICE '//Adventure-Works.com/services/AccountsPayable'  
    WITH USER = APUser, ANONYMOUS=ON ;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER REMOTE SERVICE BINDING &#40;Transact-SQL&#41;](../../t-sql/statements/alter-remote-service-binding-transact-sql.md)   
 [DROP REMOTE SERVICE BINDING &#40;Transact-SQL&#41;](../../t-sql/statements/drop-remote-service-binding-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
