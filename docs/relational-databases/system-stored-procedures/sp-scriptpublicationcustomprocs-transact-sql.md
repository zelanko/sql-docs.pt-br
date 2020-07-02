---
title: sp_scriptpublicationcustomprocs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_scriptpublicationcustomprocs
- sp_scriptpublicationcustomprocs_TSQL
helpviewer_keywords:
- sp_scriptpublicationcustomprocs
ms.assetid: b06102d5-4284-4834-b126-bc0baea49be5
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 19a7b793a1bd7a72941a8f07baba44c584e5d8f2
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85645381"
---
# <a name="sp_scriptpublicationcustomprocs-transact-sql"></a>sp_scriptpublicationcustomprocs (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Gera scripts dos procedimentos personalizados INSERT, UPDATE e DELETE para todos os artigos de tabela em uma publicação na qual a opção de esquema de procedimento personalizado está habilitada. **sp_scriptpublicationcustomprocs** é particularmente útil para configurar assinaturas para as quais o instantâneo é aplicado manualmente.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_scriptpublicationcustomprocs [ @publication = ] 'publication_name'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication_name'`É o nome da publicação. *publication_name* é **sysname** sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Retorna um conjunto de resultados que consiste em uma única coluna **nvarchar (4000)** . O conjunto de resultados forma a instrução completa CREATE PROCEDURE necessária para criar o procedimento armazenado personalizado.  
  
## <a name="remarks"></a>Comentários  
 Não são gerados scripts de procedimentos personalizados para artigos sem a opção de geração automática de esquema de procedimento personalizado (0x2).  
  
 Os procedimentos a seguir são usados pelo **sp_scriptpublicationcustomprocs** para criar procedimentos ao Assinante e não devem ser executados diretamente:  
  
 **sp_script_reconciliation_delproc**  
  
 **sp_script_reconciliation_insproc**  
  
 **sp_script_reconciliation_vdelproc**  
  
 **sp_script_reconciliation_xdelproc**  
  
 **sp_scriptdelproc**  
  
 **sp_scriptinsproc**  
  
 **sp_scriptmappedupdproc**  
  
 **sp_scriptupdproc**  
  
 **sp_scriptvdelproc**  
  
 **sp_scriptvupdproc**  
  
 **sp_scriptxdelproc**  
  
 **sp_scriptxupdproc**  
  
## <a name="permissions"></a>Permissões  
 A permissão execute é concedida a **Public**; uma verificação de segurança de procedimento é executada dentro desse procedimento armazenado para restringir o acesso a membros da função de servidor fixa **sysadmin** e **db_owner** função de banco de dados fixa no banco de dados atual.  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
