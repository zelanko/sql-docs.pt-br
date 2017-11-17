---
title: SUSER_NAME (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SUSER_NAME
- SUSER_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- security identification names [SQL Server]
- logins [SQL Server], users
- identification names for logins [SQL Server]
- users [SQL Server], logins
- SUSER_NAME function
- logins [SQL Server], names
- names [SQL Server], logins
ms.assetid: ae598d9f-9baa-49b8-b1c1-042854206de4
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a8d4eae9424d5c5cb2dbb2e7851d4e660fa0ba72
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="susername-transact-sql"></a>SUSER_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

  Retorna o nome de identificação de logon do usuário.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SUSER_NAME ( [ server_user_id ] )   
```  
  
## <a name="arguments"></a>Argumentos  
 *server_user_id*  
 É o número de identificação de logon do usuário. *server_user_id*, que é opcional, é **int**. *server_user_id* pode ser o número de identificação de logon de qualquer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon ou [!INCLUDE[msCoName](../../includes/msconame-md.md)] usuário ou grupo que tem permissão para se conectar a uma instância do Windows [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se *server_user_id* não é especificado, o nome de identificação de logon para o usuário atual será retornado. Se o parâmetro contiver a palavra NULL, retornará NULL.  
  
## <a name="return-types"></a>Tipos de retorno  
 **nvarchar (128)**  
  
## <a name="remarks"></a>Comentários  
 Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versão 7.0, o número de identificação de segurança (SID) substituiu o número de identificação de usuário do servidor (SUID).  
  
 SUSER_NAME retorna um nome de logon somente para um logon que tenha uma entrada no **syslogins** tabela do sistema.  
  
 SUSER_NAME pode ser usado em uma lista de seleção, cláusula WHERE e em qualquer local em que uma expressão seja permitida, e deve sempre ser seguido de parênteses, mesmo que nenhum parâmetro seja especificado.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna o nome de identificação de logon do usuário com um número de identificação de logon de `1`.  
  
```  
SELECT SUSER_NAME(1);  
```  
  
## <a name="see-also"></a>Consulte também  
 [SUSER_ID &#40; Transact-SQL &#41;](../../t-sql/functions/suser-id-transact-sql.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  

