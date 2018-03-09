---
title: sp_validname (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_validname
- sp_validname_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_validname
ms.assetid: d51c53c2-1332-407f-b725-4983f2e710eb
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 00dc003905fb90ae819bc49eba68aeee2f1cdbb1
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="spvalidname-transact-sql"></a>sp_validname (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Verifica nomes de identificadores válidos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Todos os dados de zero e não binários, incluindo dados de Unicode que podem ser armazenados usando o **nchar**, **nvarchar**, ou **ntext** tipos de dados, são aceitos como caracteres válidos para nomes de identificador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_validname [@name =] 'name'   
     [, [@raise_error =] raise_error]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@name=** ] **'***nome***'**  
 É o nome do [identificadores](../../relational-databases/databases/database-identifiers.md) para o qual verificar a validade. *nome* é **sysname**, sem padrão. *nome* não pode ser NULL, não pode ser uma cadeia de caracteres vazia e não pode conter um caractere zero binário.  
  
 [  **@raise_error=** ] *gerar_erro*  
 Especifica se um erro deve ser gerado. *gerar_erro* é **bit**, com um padrão de 1. Isso significa que aparecerão erros. 0 faz com que nenhuma mensagem de erro apareça.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="see-also"></a>Consulte também  
 [Mecanismo de banco de dados armazenados procedimentos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [NCHAR &#40; Transact-SQL &#41;](../../t-sql/functions/nchar-transact-sql.md)   
 [nchar e nvarchar &#40; Transact-SQL &#41;](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)   
 [ntext, texto e imagem &#40; Transact-SQL &#41;](../../t-sql/data-types/ntext-text-and-image-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
