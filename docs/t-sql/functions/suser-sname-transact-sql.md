---
title: Suser_sname (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SUSER_SNAME_TSQL
- SUSER_SNAME
dev_langs:
- TSQL
helpviewer_keywords:
- security identification names [SQL Server]
- logins [SQL Server], users
- SIDs [SQL Server]
- SUSER_SNAME function
- users [SQL Server], logins
- logins [SQL Server], names
- IDs [SQL Server], logins
- identification numbers [SQL Server], logins
- names [SQL Server], logins
ms.assetid: 11ec7d86-d429-4004-a436-da25df9f8761
caps.latest.revision: 24
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 35e3429d49940cd863cd04fc336226268ddf61c9
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="susersname-transact-sql"></a>SUSER_SNAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna o nome de logon associado a um número de identificação de segurança (SID).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
SUSER_SNAME ( [ server_user_sid ] )   
```  
  
## <a name="arguments"></a>Argumentos  
 *server_user_sid*  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 É o número opcional de identificação de segurança do logon. *server_user_sid* é **varbinary(85)**. *server_user_sid* pode ser o número de identificação de segurança de qualquer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon ou [!INCLUDE[msCoName](../../includes/msconame-md.md)] usuário ou grupo. Se *server_user_sid* não é especificado, serão retornadas informações sobre o usuário atual. Se o parâmetro contiver a palavra NULL, retornará NULL.  
  
## <a name="return-types"></a>Tipos de retorno  
 **nvarchar (128)**  
  
## <a name="remarks"></a>Comentários  
 SUSER_SNAME pode ser usado como uma restrição DEFAULT em ALTER TABLE ou CREATE TABLE. SUSER_SNAME pode ser usado em uma lista de seleção, em uma cláusula WHERE e em qualquer lugar em que uma expressão for permitida. SUSER_SNAME sempre deve ser seguido de parênteses, ainda que nenhum parâmetro seja especificado.  
  
 Quando chamado sem um argumento, SUSER_SNAME retorna o nome do contexto de segurança atual. Quando chamado sem um argumento em um lote que alternou o contexto usando EXECUTE AS, SUSER_SNAME retorna o nome do contexto representado. Quando chamado de um contexto representado, ORIGINAL_LOGIN retorna o nome do contexto original.  
  
## <a name="includesssdsfullincludessssdsfull-mdmd-remarks"></a>[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] Comentários  
 SUSER_NAME sempre retorna o nome de logon para o contexto de segurança atual.  
  
 A instrução SUSER_SNAME não oferece suporte à execução usando um contexto de segurança representado por meio de EXECUTE AS.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-susersname"></a>A. Usando SUSER_SNAME  
 O exemplo a seguir retorna o nome de logon para o contexto de segurança atual.  
  
```  
SELECT SUSER_SNAME();  
GO  
```  
  
### <a name="b-using-susersname-with-a-windows-user-security-id"></a>B. Usando SUSER_SNAME com um identificador de segurança de usuário do Windows  
 O exemplo seguinte retorna o nome de logon associado a um número de identificação de segurança do Windows.  
  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
SELECT SUSER_SNAME(0x010500000000000515000000a065cf7e784b9b5fe77c87705a2e0000);  
GO  
```  
  
### <a name="c-using-susersname-as-a-default-constraint"></a>C. Usando SUSER_SNAME como uma restrição DEFAULT  
 O exemplo a seguir usa `SUSER_SNAME` como uma restrição `DEFAULT` em uma instrução `CREATE TABLE`.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE sname_example  
(  
login_sname sysname DEFAULT SUSER_SNAME(),  
employee_id uniqueidentifier DEFAULT NEWID(),  
login_date  datetime DEFAULT GETDATE()  
);   
GO  
INSERT sname_example DEFAULT VALUES;  
GO  
```  
  
### <a name="d-calling-susersname-in-combination-with-execute-as"></a>D. Chamando SUSER_SNAME em combinação com EXECUTE AS  
 Este exemplo mostra o comportamento de SUSER_SNAME quando chamado de um contexto representado.  
  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
SELECT SUSER_SNAME();  
GO  
EXECUTE AS LOGIN = 'WanidaBenShoof';  
SELECT SUSER_SNAME();  
REVERT;  
GO  
SELECT SUSER_SNAME();  
GO  
  
```  
  
 Aqui está o resultado.  
  
 `sa`  
  
 `WanidaBenShoof`  
  
 `sa`  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-susersname"></a>E. Usando SUSER_SNAME  
 O exemplo seguinte retorna o nome de logon do número de identificação de segurança com um valor de `0x01`.  
  
```  
SELECT SUSER_SNAME(0x01);  
GO  
```  
  
### <a name="f-returning-the-current-login"></a>F. Retornando o logon atual  
 O exemplo a seguir retorna o nome de logon do logon atual.  
  
```  
SELECT SUSER_SNAME() AS CurrentLogin;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [SUSER_SID &#40; Transact-SQL &#41;](../../t-sql/functions/suser-sid-transact-sql.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [EXECUTE AS &#40; Transact-SQL &#41;](../../t-sql/statements/execute-as-transact-sql.md)  
  
  


