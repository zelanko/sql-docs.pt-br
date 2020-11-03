---
description: sys.trusted_assemblies (Transact-SQL)
title: sys.trusted_assemblies (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- trusted_assemblies_TSQL
- trusted_assemblies
- sys.trusted_assemblies_TSQL
- sys.trusted_assemblies
dev_langs:
- TSQL
helpviewer_keywords:
- sys.trusted_assemblies
ms.assetid: ''
author: VanMSFT
ms.author: vanto
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4cbf5b3310d23f5bc3f488a536447d0dc3e92350
ms.sourcegitcommit: 80701484b8f404316d934ad2a85fd773e26ca30c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93243830"
---
# <a name="systrusted_assemblies-transact-sql"></a>sys.trusted_assemblies (Transact-SQL)  
[!INCLUDE[SQL Server 2017](../../includes/applies-to-version/sqlserver2017.md)]

Contém uma linha para cada assembly confiável para o servidor.

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  


|Nome da coluna |Tipo de dados |Descrição |
|--- |--- |--- |
|hash |varbinary(8000) |SHA2_512 hash do conteúdo do assembly. |
|descrição |nvarchar(4000) |Descrição opcional definida pelo usuário do assembly. A Microsoft recomenda usar o nome canônico que codifica o nome simples, o número de versão, a cultura, a chave pública e a arquitetura do assembly para confiar. Esse valor identifica exclusivamente o assembly no lado Common Language Runtime (CLR) e é o mesmo que o valor de clr_name em sys. assemblies. |
|create_date |datetime2 |Data em que o assembly foi adicionado à lista de assemblies confiáveis. |
|created_by |nvarchar(128) |Nome de logon da entidade de segurança que adicionou o assembly à lista. |
| | | |

### <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
 
## <a name="remarks"></a>Comentários  
Use **[Sys.sp_add_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md)** para adicionar e **[Sys.sp_drop_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-drop-trusted-assembly-transact-sql.md)** para remover assemblies do `sys.trusted_assemblies` .

## <a name="see-also"></a>Consulte Também  
  [sys.sp_add_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md)  
  [sys.sp_drop_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-drop-trusted-assembly-transact-sql.md)  
  [DROP ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)  
  [sys.dm_clr_loaded_assemblies](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)  
