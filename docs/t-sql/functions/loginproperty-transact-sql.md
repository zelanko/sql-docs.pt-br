---
title: LOGINPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- BadPasswordCount_TSQL
- BadPasswordTime_TSQL
- IsLockedIsMustChange
- PasswordLastSetTime
- LOGINPROPERTY_TSQL
- LockoutTime
- BadPasswordCount
- PasswordHash
- HistoryLengthIsExpired
- LockoutTime_TSQL
- PasswordHash_TSQL
- HistoryLengthIsExpired_TSQL
- PasswordLastSetTime_TSQL
- BadPasswordTime
- IsLockedIsMustChange_TSQL
- LOGINPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- default database
- LOGINPROPERTY function
ms.assetid: b34df777-79b0-49a5-88db-b99998479a5d
caps.latest.revision: 42
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 31cbf502614fb348f35474237009f444ed294384
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="loginproperty-transact-sql"></a>LOGINPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre configurações de política de logon.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
LOGINPROPERTY ( 'login_name' , 'property_name' )  
```  
  
## <a name="arguments"></a>Argumentos  
 *login_name*  
 É o nome de um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o qual o status da propriedade de logon será retornado.  
  
 *PropertyName*  
 É uma expressão que contém as informações de propriedade a serem retornadas para o logon. *PropertyName* pode ser um dos valores a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|**BadPasswordCount**|Retorna o número de tentativas consecutivas de fazer logon com uma senha incorreta.|  
|**BadPasswordTime**|Retorna a hora da última tentativa de fazer logon com uma senha incorreta.|  
|**DaysUntilExpiration**|Retorna o número de dias para que a senha expire.|  
|**DefaultDatabase**|Retorna o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon padrão banco de dados como armazenado em metadados ou **mestre** se nenhum banco de dados especificado. Retorna NULL para não -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provisionou os usuários (por exemplo, usuários autenticados do Windows).|  
|**DefaultLanguage**|Retorna a linguagem padrão de logon como armazenado em metadados. Retorna NULL para não -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usuários provisionados, por exemplo, o Windows a usuários autenticados.|  
|**HistoryLength**|Retorna o número de senhas rastreadas para o logon usando o mecanismo de imposição de política de senha. 0, se a política de senha não for imposta. Ao retomar a imposição da política de senha, ela é reiniciada em 1.|  
|**IsExpired**|Indica se o logon expirou.|  
|**IsLocked**|Indica se o logon está bloqueado.|  
|**IsMustChange**|Indica se o logon deve alterar sua senha na próxima conexão.|  
|**LockoutTime**|Retorna a data em que o logon no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi bloqueado porque excedeu o número permitido de tentativas de logon com falha.|  
|**PasswordHash**|Retorna o hash da senha.|  
|**PasswordLastSetTime**|Retorna a data em que a senha atual foi definida.|  
|**PasswordHashAlgorithm**|Retorna o algoritmo usado para o hash da senha.|  
  
## <a name="returns"></a>Retorna  
 O tipo de dado depende do valor solicitado.  
  
 **IsLocked**, **IsExpired**, e **IsMustChange** são do tipo **int**.  
  
-   1 se o logon estiver no estado especificado.  
  
-   0 se o logon não estiver no estado especificado.  
  
 **BadPasswordCount** e **HistoryLength** são do tipo **int**.  
  
 **BadPasswordTime**, **LockoutTime**, **PasswordLastSetTime** são do tipo **datetime**.  
  
 **PasswordHash** é do tipo **varbinary**.  
  
 NULL se o logon não for um logon válido do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **DaysUntilExpiration** é do tipo **int**.  
  
-   0 se o logon estiver expirado ou se for expira no dia da consulta.  
  
-   -1 se a política de segurança local no Windows nunca expirar a senha.  
  
-   NULL, se CHECK_POLICY ou CHECK_EXPIRATION forem OFF para um logon ou se o sistema operacional não oferecer suporte à política de senha.  
  
 **PasswordHashAlgorithm** é do tipo int.  
  
-   0, se for um hash SQL7.0  
  
-   1 se um hash SHA-1  
  
-   2, se for um hash SHA-2  
  
-   NULL se o logon não for um logon válido do SQL Server  
  
## <a name="remarks"></a>Comentários  
 Essa função interna retorna informações sobre as configurações de política de senha de um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os nomes das propriedades não diferenciam maiusculas de minúsculas, para nomes de propriedade, como **BadPasswordCount** e **badpasswordcount** são equivalentes. Os valores a **PasswordHash, PasswordHashAlgorithm**, e **PasswordLastSetTime** propriedades estão disponíveis em todas as configurações com suporte de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas as outras propriedades são somente disponível quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em execução no [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] e CHECK_POLICY e CHECK_EXPIRATION estão habilitados. Para obter mais informações, consulte [Password Policy](../../relational-databases/security/password-policy.md).  
  
## <a name="permissions"></a>Permissões  
 Requer permissão VIEW para o logon. Ao solicitar o hash de senha, também requer a permissão CONTROL SERVER.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-checking-whether-a-login-must-change-its-password"></a>A. Verificando se um logon deve alterar sua senha  
 A exemplo a seguir verifica se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] login `John3` deve alterar sua senha na próxima vez que ele se conecta a uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
SELECT LOGINPROPERTY('John3', 'IsMustChange');  
GO  
```  
  
### <a name="b-checking-whether-a-login-is-locked-out"></a>B. Verificando se um logon está bloqueado  
 O exemplo a seguir verifica se o logon `John3` do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está bloqueado.  
  
```  
SELECT LOGINPROPERTY('John3', 'IsLocked');  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)  
  
  

