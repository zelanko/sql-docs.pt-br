---
description: sp_validname (Transact-SQL)
title: sp_validname (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_validname
- sp_validname_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_validname
ms.assetid: d51c53c2-1332-407f-b725-4983f2e710eb
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e73d8f6345be199c44278cb15aa43c6ada7f91c0
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97466787"
---
# <a name="sp_validname-transact-sql"></a>sp_validname (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Verifica nomes de identificadores válidos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Todos os dados não binários e não nulos, incluindo dados Unicode que podem ser armazenados usando os tipos de dados **nchar**, **nvarchar** ou **ntext** , são aceitos como caracteres válidos para nomes de identificadores.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_validname [@name =] 'name'   
     [, [@raise_error =] raise_error]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @name = ] 'name'` É o nome dos [identificadores](../../relational-databases/databases/database-identifiers.md) para os quais verificar a validade. o *nome* é **sysname**, sem padrão. o *nome* não pode ser nulo, não pode ser uma cadeia de caracteres vazia e não pode conter um caractere binário zero.  
  
`[ @raise_error = ] raise_error` Especifica se um erro deve ser gerado. *raise_error* é **bit**, com um padrão de 1. Isso significa que aparecerão erros. 0 faz com que nenhuma mensagem de erro apareça.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="see-also"></a>Consulte Também  
 [Mecanismo de Banco de Dados procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [NCHAR &#40;Transact-SQL&#41;](../../t-sql/functions/nchar-transact-sql.md)   
 [nchar e nvarchar &#40;&#41;de Transact-SQL ](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)   
 [ntext, Text e Image &#40;Transact-SQL&#41;](../../t-sql/data-types/ntext-text-and-image-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
