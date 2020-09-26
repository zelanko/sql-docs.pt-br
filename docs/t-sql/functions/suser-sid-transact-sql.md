---
description: SUSER_SID (Transact-SQL)
title: SUSER_SID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SUSER_SID
- SUSER_SID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- logins [SQL Server], users
- SIDs [SQL Server]
- security identifiers [SQL Server]
- users [SQL Server], logins
- 15401 (Database Engine error)
- IDs [SQL Server], logins
- identification numbers [SQL Server], logins
- SUSER_SID function
ms.assetid: 57b42a74-94e1-4326-85f1-701b9de53c7d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: c3a08123af9155789fa2d14e2deac807061bf162
ms.sourcegitcommit: 197a6ffb643f93592edf9e90b04810a18be61133
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2020
ms.locfileid: "91380051"
---
# <a name="suser_sid-transact-sql"></a>SUSER_SID (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna o SID (número de identificação de segurança) para o nome de logon especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
SUSER_SID ( [ 'login' ] [ , Param2 ] )   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 **'** *login* **'**  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior
  
 É o nome de logon do usuário. *login* é **sysname**. *login*, que é opcional, pode ser um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou um usuário ou grupo do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Se *login* não for especificado, serão retornadas informações sobre o contexto de segurança atual. Se o parâmetro contiver a palavra NULL, retornará NULL.  
  
 *Param2*  
**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior
  
 Especifica se o nome de logon é validado. *Param2* é do tipo **int** e é opcional. Quando *Param2* for 0, o nome de logon não será validado. Quando*Param2* não estiver especificado como 0, será verificado se o nome de logon do Windows é exatamente igual ao nome de logon armazenado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="return-types"></a>Tipos de retorno  
 **varbinary(85)**  
  
## <a name="remarks"></a>Comentários  
 SUSER_SID pode ser usado como uma restrição DEFAULT em ALTER TABLE ou CREATE TABLE. SUSER_ID pode ser usado em uma lista de seleção, em uma cláusula WHERE ou em qualquer local em que uma expressão seja permitida. SUSER_SID deve sempre ser seguido de parênteses, mesmo que nenhum parâmetro seja especificado.  
  
 Quando chamado sem um argumento, SUSER_SID retorna o SID do contexto de segurança atual. Quando chamado sem um argumento em um lote que alternou o contexto usando EXECUTE AS, SUSER_SID retorna o SID do contexto representado. Quando chamado de um contexto representado, SUSER_SID(ORIGINAL_LOGIN()) retorna o SID contexto original.  
  
 No caso de a ordenação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e a ordenação do Windows serem diferentes, SUSER_SID poderá falhar quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o Windows armazenarem o logon em um formato diferente. Por exemplo, se o computador do Windows TestComputer tiver o logon User e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] armazenar o logon como TESTCOMPUTER\User, a pesquisa do logon TestComputer\User poderá não resolver o nome de logon corretamente. Para ignorar essa validação do nome de logon, use *Param2*. Ordenações diferentes são geralmente uma causa do erro 15401 do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
 `Windows NT user or group '%s' not found. Check the name again.`  
  
## <a name="sssdsfull-remarks"></a>[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] Comentários  
 SUSER_SID sempre retorna o SID de logon para o contexto de segurança atual. Use [sys.database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md) para obter o SID de um logon diferente.
  
 A instrução SUSER_SID não oferece suporte à execução usando um contexto de segurança representado por meio de EXECUTE AS.  

## <a name="examples"></a>Exemplos  
  
### <a name="a-using-suser_sid"></a>a. Usando SUSER_SID  
 O exemplo a seguir retorna o SID (número de identificação de segurança) para o contexto de segurança atual.  
  
```sql
SELECT SUSER_SID();  
```  
  
### <a name="b-using-suser_sid-with-a-specific-login"></a>B. Usando SUSER_SID com um logon específico  
 O exemplo a seguir retorna o número de identificação de segurança para o logon [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `sa`.  
  
**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior
  
```sql
SELECT SUSER_SID('sa');  
GO  
```  
  
### <a name="c-using-suser_sid-with-a-windows-user-name"></a>C. Usando SUSER_SID com um nome de usuário do Windows  
 O exemplo a seguir retorna o número de identificação de segurança para o usuário do Windows `London\Workstation1`.  
  
**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior
  
```sql
SELECT SUSER_SID('London\Workstation1');  
GO  
```  
  
### <a name="d-using-suser_sid-as-a-default-constraint"></a>D. Usando SUSER_SID como uma restrição DEFAULT  
 O exemplo a seguir usa `SUSER_SID` como uma restrição `DEFAULT` em uma instrução `CREATE TABLE`.  
  
```sql
USE AdventureWorks2012;  
GO  
CREATE TABLE sid_example  
(  
login_sid   VARBINARY(85) DEFAULT SUSER_SID(),  
login_name  VARCHAR(30) DEFAULT SYSTEM_USER,  
login_dept  VARCHAR(10) DEFAULT 'SALES',  
login_date  DATETIME DEFAULT GETDATE()  
);   
GO  
INSERT sid_example DEFAULT VALUES;  
GO  
```  
  
### <a name="e-comparing-the-windows-login-name-to-the-login-name-stored-in-sql-server"></a>E. Comparando o nome de logon do Windows ao nome de logon armazenado no SQL Server  
 O exemplo a seguir mostra como usar *Param2* para obter o SID do Windows e usa esse SID como uma entrada para a função `SUSER_SNAME`. O exemplo fornece o logon no formato em que está armazenado no Windows (`TestComputer\User`) e o retorna no formato em que está armazenado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (`TESTCOMPUTER\User`).  
  
**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior
  
```sql
SELECT SUSER_SNAME(SUSER_SID('TestComputer\User', 0));  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ORIGINAL_LOGIN &#40;Transact-SQL&#41;](../../t-sql/functions/original-login-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [binary e varbinary &#40;Transact-SQL&#41;](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)   
 [Funções do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)  
  
  
