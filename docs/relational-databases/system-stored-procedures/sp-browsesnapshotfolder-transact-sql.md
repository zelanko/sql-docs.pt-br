---
title: sp_browsesnapshotfolder (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_browsesnapshotfolder
- sp_browsesnapshotfolder_TSQL
helpviewer_keywords:
- sp_browsesnapshotfolder
ms.assetid: 0872edf2-4038-4bc1-a68d-05ebfad434d2
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4b31f3bb0e865452fd6f557a4832b04a21c11624
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spbrowsesnapshotfolder-transact-sql"></a>sp_browsesnapshotfolder (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o caminho completo do último instantâneo gerado para uma publicação. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_browsesnapshotfolder [@publication= ] 'publication'  
    { [ , [ @subscriber = ] 'subscriber' ]  
 [ , [ @subscriber_db = ] 'subscriber_db' ] }  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=**] **'***publicação***'**  
 É o nome da publicação que contém o artigo. *publicação* é **sysname**, sem padrão.  
  
 [  **@subscriber=**] **'***assinante***'**  
 É o nome do Assinante. *assinante* é **sysname**, com um padrão NULL.  
  
 [  **@subscriber_db=**] **'***subscriber_db***'**  
 É o nome do banco de dados de assinatura. *subscriber_db* é **sysname**, com um padrão NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**snapshot_folder**|**nvarchar(512)**|Caminho completo para o diretório de instantâneo.|  
  
## <a name="remarks"></a>Comentários  
 **sp_browsesnapshotfolder** é usado em replicação de instantâneo e replicação transacional.  
  
 Se o *assinante* e *subscriber_db* campos forem NULL, o procedimento armazenado retorna a pasta de instantâneo do instantâneo mais recente, ele pode encontrar para a publicação. Se o *assinante* e *subscriber_db* campos forem especificados, o procedimento armazenado retorna a pasta de instantâneo para a assinatura especificada. Se um instantâneo não tiver sido gerado para a publicação, um conjunto de resultados vazio será retornado.  
  
 Se a publicação for definida para gerar arquivos de instantâneo no diretório de trabalho do Publicador e na pasta de instantâneo do Publicador, o conjunto de resultados conterá duas linhas. A primeira linha contém a pasta de instantâneo da publicação e a segunda linha contém o diretório de trabalho do publicador. **sp_browsesnapshotfolder** é útil para determinar o diretório onde os arquivos de instantâneo são gerados.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_browsesnapshotfolder**.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
