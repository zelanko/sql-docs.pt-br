---
title: SUSER_ID (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SUSER_ID_TSQL
- SUSER_ID
dev_langs: TSQL
helpviewer_keywords:
- users [SQL Server], IDs
- logins [SQL Server], IDs
- SUSER_ID function
- IDs [SQL Server], logins
- identification numbers [SQL Server], logins
- user IDs [SQL Server]
ms.assetid: 348911ab-b0b6-4867-aee7-e6f42e053a4a
caps.latest.revision: "22"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e4b00485c741857f1e3438c3e50995886900fe29
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="suserid-transact-sql"></a>SUSER_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o número de identificação de logon do usuário.  
  
> [!NOTE]  
>  Começando com [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], SUSER_ID retorna o valor listado como **principal_id** no **sys. server_principals** exibição do catálogo.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SUSER_ID ( [ 'login' ] )   
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *login* **'**  
 É o nome de logon do usuário. *logon* é **nchar**. Se *login* é especificado como **char**, *login* é convertido implicitamente em **nchar**. *logon* pode ser qualquer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon ou usuário do Windows ou grupo que tem permissão para se conectar a uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se *login* não é especificado, o número de identificação de logon para o usuário atual será retornado. Se o parâmetro contiver a palavra NULL, retornará NULL.  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
## <a name="remarks"></a>Comentários  
 SUSER_ID só retorna um número de identificação para logons que foram explicitamente provisionados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa ID é usada no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para acompanhar propriedade e permissões. Ela não é equivalente ao SID do logon que é retornado por SUSER_SID. Se *login* é um logon do SQL Server, o SID será mapeado para um GUID. Se *login* é um logon do Windows ou grupo do Windows, o SID será mapeado para um identificador de segurança do Windows.  
  
 SUSER_SID retorna apenas um SUID para um logon que tenha uma entrada no **syslogins** tabela do sistema.  
  
 As funções de sistema podem ser usadas na lista de seleção, na cláusula WHERE e em qualquer local em que uma expressão seja permitida, e devem sempre ser seguidas por parênteses, mesmo se nenhum parâmetro for especificado.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna o número de identificação de logon para o logon `sa`.  
  
```  
SELECT SUSER_ID('sa');  
```  
  
## <a name="see-also"></a>Consulte também  
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [SUSER_SID &#40; Transact-SQL &#41;](../../t-sql/functions/suser-sid-transact-sql.md)   
 [Funções do sistema &#40; Transact-SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  
