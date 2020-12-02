---
description: SUSER_NAME (Transact-SQL)
title: SUSER_NAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1044f594889c8d7a6698c0ffc5a09692ed734a47
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91379762"
---
# <a name="suser_name-transact-sql"></a>SUSER_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

Retorna o nome de identificação de logon do usuário.  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
SUSER_NAME ( [ server_user_id ] )   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
_server\_user\_id_  
É o número de identificação de logon do usuário. _server\_user\_id_, que é opcional, é **int**. _server\_user\_id_ pode ser o número de identificação de logon de qualquer logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou usuário ou grupo do Windows [!INCLUDE[msCoName](../../includes/msconame-md.md)] que tenha permissão para se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Quando _server\_user\_id_ não for especificado, o nome de identificação de logon do usuário atual será retornado. Se o parâmetro contiver a palavra NULL, ele retornará NULL.  
  
## <a name="return-types"></a>Tipos de retorno  
**nvarchar(128)**  
  
## <a name="remarks"></a>Comentários  
No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versão 7.0, o SID (número de identificação de segurança) substituiu o SUID (número de identificação de usuário do servidor).  
  
SUSER_NAME retorna um nome de logon apenas para um logon que tenha uma entrada na tabela do sistema **syslogins**.  
  
SUSER_NAME pode ser usado em uma lista de seleção, em uma cláusula WHERE e em qualquer lugar em que uma expressão for permitida. Use parênteses após SUSER_NAME, mesmo se nenhum parâmetro for especificado.  

> [!NOTE]
> Embora a função SUSER_NAME tenha suporte no Banco de Dados SQL do Azure, usar *Executar como* com SUSER_NAME não tem suporte no Banco de Dados SQL do Azure. 
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir retorna o nome de identificação de logon do usuário com um número de identificação de logon de `1`.  
  
```sql
SELECT SUSER_NAME(1);  
```  
  
## <a name="see-also"></a>Consulte Também  
[SUSER_ID &#40;Transact-SQL&#41;](../../t-sql/functions/suser-id-transact-sql.md)   
[Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
