---
title: SUSER_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: e9bad34cf3d195e4038d794fac913bdb3d16bc91
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "73843558"
---
# <a name="suser_id-transact-sql"></a>SUSER_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Retorna o número de identificação de logon do usuário.  
  
> [!NOTE]  
>  Começando com [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], SUSER_ID retorna o valor listado como **principal_id** na exibição do catálogo **sys.server_principals**.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SUSER_ID ( [ 'login' ] )   
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *login* **'**  
 É o nome de logon do usuário. o *logon* é **nchar**. Se o *logon* for especificado como **char**, o *logon* será convertido implicitamente em **nchar**. o *logon* pode ser qualquer logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou usuário ou grupo do Windows que tenha permissão para conectar-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se o *logon* não for especificado, o número de identificação de logon do usuário atual será retornado. Se o parâmetro contiver a palavra NULL, retornará NULL.  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
## <a name="remarks"></a>Comentários  
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
 [Funções do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)  
  
  
