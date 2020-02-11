---
title: sp_browsesnapshotfolder (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_browsesnapshotfolder
- sp_browsesnapshotfolder_TSQL
helpviewer_keywords:
- sp_browsesnapshotfolder
ms.assetid: 0872edf2-4038-4bc1-a68d-05ebfad434d2
author: stevestein
ms.author: sstein
ms.openlocfilehash: dcc7c4031253f83df49b45feae17449814af3fc3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68768977"
---
# <a name="sp_browsesnapshotfolder-transact-sql"></a>sp_browsesnapshotfolder (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Retorna o caminho completo do último instantâneo gerado para uma publicação. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_browsesnapshotfolder [@publication= ] 'publication'  
    { [ , [ @subscriber = ] 'subscriber' ]  
 [ , [ @subscriber_db = ] 'subscriber_db' ] }  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação que contém o artigo. a *publicação* é **sysname**, sem padrão.  
  
`[ @subscriber = ] 'subscriber'`É o nome do Assinante. o *assinante* é **sysname**, com um padrão de NULL.  
  
`[ @subscriber_db = ] 'subscriber_db'`É o nome do banco de dados de assinatura. *subscriber_db* é **sysname**, com um padrão de NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**snapshot_folder**|**nvarchar(512)**|Caminho completo para o diretório de instantâneo.|  
  
## <a name="remarks"></a>Comentários  
 **sp_browsesnapshotfolder** é usado na replicação de instantâneo e na replicação transacional.  
  
 Se os campos *assinante* e *subscriber_db* forem nulos, o procedimento armazenado retornará a pasta de instantâneo do instantâneo mais recente que ele pode encontrar para a publicação. Se os campos *assinante* e *subscriber_db* forem especificados, o procedimento armazenado retornará a pasta de instantâneo para a assinatura especificada. Se um instantâneo não tiver sido gerado para a publicação, um conjunto de resultados vazio será retornado.  
  
 Se a publicação for definida para gerar arquivos de instantâneo no diretório de trabalho do Publicador e na pasta de instantâneo do Publicador, o conjunto de resultados conterá duas linhas. A primeira linha contém a pasta de instantâneo da publicação e a segunda linha contém o diretório de trabalho do publicador. **sp_browsesnapshotfolder** é útil para determinar o diretório onde os arquivos de instantâneo são gerados.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_browsesnapshotfolder**.  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
