---
description: sp_removedistpublisherdbreplication (Transact-SQL)
title: sp_removedistpublisherdbreplication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_removedistpublisherdbreplication_TSQL
- sp_removedistpublisherdbreplication
helpviewer_keywords:
- sp_removedistpublisherdbreplication
ms.assetid: 9bfe002a-25b5-4226-bcfb-feb2060d6b4a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d8ecdfd856555885eb14af34451e1a939c00b233
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88469200"
---
# <a name="sp_removedistpublisherdbreplication-transact-sql"></a>sp_removedistpublisherdbreplication (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Remove metadados de publicação pertencentes a uma publicação específica no Distribuidor. Esse procedimento armazenado é executado no Distribuidor, no banco de dados de distribuição.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_removedistpublisherdbreplication [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'` É o nome do servidor do Publicador. o *Publicador* é **sysname**, sem padrão.  
  
`[ @publisher_db = ] 'publisher_db'` É o nome do banco de dados de publicação. *publisher_db* é **sysname** sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_removedistpublisherdbreplication** é usado pela replicação transacional e de instantâneo.  
  
 **sp_removedistpublisherdbreplication** é usado quando um banco de dados publicado deve ser recriado sem remover também o banco de dados de distribuição. O seguintes metadados são removidos:  
  
-   Todos os metadados de publicação.  
  
-   Metadados de todos os artigos que pertencem à publicação.  
  
-   Metadados de todas as assinaturas de publicação.  
  
-   Metadados de todos os trabalhos de agente de replicação que pertencem à publicação.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** no distribuidor ou membros da função de banco de dados fixa **db_owner** no banco de dados de distribuição podem executar **sp_removedistpublisherdbreplication**.  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
