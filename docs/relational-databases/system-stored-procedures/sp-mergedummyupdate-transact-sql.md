---
title: sp_mergedummyupdate (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_mergedummyupdate_TSQL
- sp_mergedummyupdate
helpviewer_keywords:
- sp_mergedummyupdate
ms.assetid: b834f7f6-9588-4d59-a3e2-83d8e8e722e1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 30e999d4f0d88eee21cf65c2d4e73f767485d6df
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47805594"
---
# <a name="spmergedummyupdate-transact-sql"></a>sp_mergedummyupdate (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Faz uma atualização fictícia na linha determinada de forma que ela é enviada novamente durante a próxima mesclagem. Esse procedimento armazenado pode ser executado no Publicador, no banco de dados de publicação, ou no Assinante, no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_mergedummyupdate [ @source_object =] 'source_object', [ @rowguid =] 'rowguid'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@source_object=**] **'***source_object***'**  
 É o nome do objeto de origem. *source_object*está **nvarchar(386)**, sem padrão.  
  
 [  **@rowguid=**] **'***rowguid***'**  
 É o identificador da linha. *ROWGUID* está **uniqueidentifier**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_mergedummyupdate** é usado em replicação de mesclagem.  
  
 **sp_mergedummyupdate** será útil se você gravar sua própria alternativa para o Visualizador de conflitos de replicação (Wzcnflct.exe).  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **db_owner** pode executar a função de banco de dados fixa **sp_mergedummyupdate**.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
