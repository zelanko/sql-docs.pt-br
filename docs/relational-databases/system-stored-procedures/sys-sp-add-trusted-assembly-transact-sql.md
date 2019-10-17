---
title: sys. sp_add_trusted_assembly (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_trusted_assembly_TSQL
- sp_add_trusted_assembly
- sys.sp_add_trusted_assembly_TSQL
- sys.sp_add_trusted_assembly
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_add_trusted_assembly
ms.assetid: ''
author: VanMSFT
ms.author: vanto
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bb34a814780a46c12c65948bd0b552effaacda4d
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452880"
---
# <a name="syssp_add_trusted_assembly-transact-sql"></a>sys. sp_add_trusted_assembly (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdbmi-xxxx-xxx-md.md)]

Adiciona um assembly à lista de assemblies confiáveis para o servidor.

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  


## <a name="syntax"></a>Sintaxe
```  
sp_add_trusted_assembly 
    [ @hash = ] 'value'
    [ , [ @description = ] 'description' ]
```  

## <a name="remarks"></a>Remarks  

Este procedimento adiciona um assembly a [Sys. trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md).

## <a name="arguments"></a>Argumentos

[@hash =] '*valor*'  
O valor de hash SHA2_512 do assembly a ser adicionado à lista de assemblies confiáveis para o servidor. Os assemblies confiáveis podem ser carregados quando a [segurança estrita do CLR](../../database-engine/configure-windows/clr-strict-security.md) estiver habilitada, mesmo se o assembly não estiver assinado ou se o banco de dados não estiver marcado como confiável.

[@description =] '*Descrição*'  
Descrição opcional definida pelo usuário do assembly. A Microsoft recomenda usar o nome canônico que codifica o nome simples, o número de versão, a cultura, a chave pública e a arquitetura do assembly para confiar. Esse valor identifica exclusivamente o assembly no lado Common Language Runtime (CLR) e é o mesmo que o valor clr_name em sys. assemblies. 

## <a name="permissions"></a>Permissões

Requer associação na função de servidor fixa `sysadmin` ou na permissão `CONTROL SERVER`.

## <a name="examples"></a>Exemplos  

O exemplo a seguir adiciona um assembly chamado `pointudt` à lista de assemblies confiáveis para o servidor. Esses valores estão disponíveis em [Sys. assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md).     

```  
EXEC sp_add_trusted_assembly 0x8893AD6D78D14EE43DF482E2EAD44123E3A0B684A8873C3F7BF3B5E8D8F09503F3E62370CE742BBC96FE3394477214B84C7C1B0F7A04DCC788FA99C2C09DFCCC, 
N'pointudt, version=0.0.0.0, culture=neutral, publickeytoken=null, processorarchitecture=msil';
```  

## <a name="see-also"></a>Consulte Também  
  [sys. sp_drop_trusted_assembly](sys-sp-drop-trusted-assembly-transact-sql.md)  
  [sys. trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md)  
  [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
  [Segurança estrita do CLR](../../database-engine/configure-windows/clr-strict-security.md)  
  [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)  
  [sys.dm_clr_loaded_assemblies](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)  

