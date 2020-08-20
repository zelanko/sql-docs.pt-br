---
description: sys.sp_drop_trusted_assembly (Transact-SQL)
title: sys. sp_drop_trusted_assembly (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_drop_trusted_assembly_TSQL
- sp_drop_trusted_assembly
- sys.sp_drop_trusted_assembly_TSQL
- sys.sp_drop_trusted_assembly
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_drop_trusted_assembly
ms.assetid: ''
author: VanMSFT
ms.author: vanto
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fd3c1747fee1e23e0f68a7bcf1744f40e80786b8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489020"
---
# <a name="syssp_drop_trusted_assembly-transact-sql"></a>sys.sp_drop_trusted_assembly (Transact-SQL)  
[!INCLUDE[SQL Server 2017](../../includes/applies-to-version/sqlserver2017.md)]

Remove um assembly da lista de assemblies confiáveis no servidor.

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  


## <a name="syntax"></a>Sintaxe
```  
sp_drop_trusted_assembly 
    [ @hash = ] 'value'
```  

## <a name="arguments"></a>Argumentos

[ @hash =] '*valor*'  
O SHA2_512 valor de hash do assembly a ser removido da lista de assemblies confiáveis para o servidor. Os assemblies confiáveis podem ser carregados quando a segurança estrita do CLR estiver habilitada, mesmo se o assembly não estiver assinado ou se o banco de dados não estiver marcado como confiável.

## <a name="remarks"></a>Comentários  

Este procedimento remove um assembly de [Sys. trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md).

## <a name="permissions"></a>Permissões

Requer a associação à `sysadmin` função de servidor fixa ou à `CONTROL SERVER` permissão.

## <a name="examples"></a>Exemplos  

O exemplo a seguir remove um hash de assembly da lista de assemblies confiáveis para o servidor.  

```  
EXEC sp_drop_trusted_assembly 
0x8893AD6D78D14EE43DF482E2EAD44123E3A0B684A8873C3F7BF3B5E8D8F09503F3E62370CE742BBC96FE3394477214B84C7C1B0F7A04DCC788FA99C2C09DFCCC; 
```  

## <a name="see-also"></a>Consulte Também  
  [Sys. sp_add_trusted_assembly](sys-sp-add-trusted-assembly-transact-sql.md) [Sys. trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md) [drop assembly &#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)  
  [sys.dm_clr_loaded_assemblies](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)  

