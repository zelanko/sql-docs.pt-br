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
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SUSER_ID_TSQL
- SUSER_ID
dev_langs:
- TSQL
helpviewer_keywords:
- users [SQL Server], IDs
- logins [SQL Server], IDs
- SUSER_ID function
- IDs [SQL Server], logins
- identification numbers [SQL Server], logins
- user IDs [SQL Server]
ms.assetid: 348911ab-b0b6-4867-aee7-e6f42e053a4a
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c66da357e43d1a43b3b97c7047d223751ecbe2ba
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/21/2018
---
# <a name="suserid-transact-sql"></a>SUSER_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Retorna o número de identificação de logon do usuário.  

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]
  
> [!NOTE]  
>  Começando com [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], SUSER_ID retorna o valor listado como **principal_id** na exibição do catálogo **sys.server_principals**.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SUSER_ID ( [ 'login' ] )   
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *login* **'**  
 É o nome de logon do usuário. o *logon* é **nchar**. Se o *logon* for especificado como **char**, o *logon* será convertido implicitamente em **nchar**. o *logon* pode ser qualquer logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou usuário ou grupo do Windows que tenha permissão para conectar-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se o *logon* não for especificado, o número de identificação de logon do usuário atual será retornado. Se o parâmetro contiver a palavra NULL, retornará NULL.  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
## <a name="remarks"></a>Remarks  
 SUSER_ID só retorna um número de identificação para logons que foram explicitamente provisionados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa ID é usada no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para acompanhar propriedade e permissões. Ela não é equivalente ao SID do logon que é retornado por SUSER_SID. Se o *logon* for um logon do SQL Server, a SID será mapeada para um GUID. Se o *logon* for um logon ou um grupo do Windows, a SID será mapeada para um identificador de segurança do Windows.  
  
 SUSER_SID retorna um SUID apenas para um logon que tenha uma entrada na tabela do sistema **syslogins**.  
  
 As funções de sistema podem ser usadas na lista de seleção, na cláusula WHERE e em qualquer local em que uma expressão seja permitida, e devem sempre ser seguidas por parênteses, mesmo se nenhum parâmetro for especificado.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna o número de identificação de logon para o logon `sa`.  
  
```  
SELECT SUSER_ID('sa');  
```  
  
## <a name="see-also"></a>Consulte Também  
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [SUSER_SID &#40;Transact-SQL&#41;](../../t-sql/functions/suser-sid-transact-sql.md)   
 [Funções do Sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  
