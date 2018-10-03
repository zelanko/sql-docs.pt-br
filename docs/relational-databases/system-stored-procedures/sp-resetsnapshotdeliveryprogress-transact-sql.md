---
title: sp_resetsnapshotdeliveryprogress (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_resetsnapshotdeliveryprogress
- sp_resetsnapshotdeliveryprogress_TSQL
helpviewer_keywords:
- sp_resetsnapshotdeliveryprogress
ms.assetid: 5df7d86b-d343-4d9b-88b1-74429ed092e6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9685aa789f0539e9a5720a78ec2180987aac9d4a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47685634"
---
# <a name="spresetsnapshotdeliveryprogress-transact-sql"></a>sp_resetsnapshotdeliveryprogress (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Redefine o processo de entrega de instantâneo para uma assinatura pull, para que a entrega do instantâneo possa ser reiniciada. Executado no Assinante, no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_resetsnapshotdeliveryprogress [ [ @verbose_level = ] verbose_level ]  
    [ , [ @drop_table = ] 'drop_table' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@verbose_level**=] *verbose_level*  
 Especifica a quantidade de informações a ser retornada. *verbose_level*está **int**, com um padrão de **1**. Um valor de **1** significa que um erro é retornado se os bloqueios necessários não podem ser obtidos na **MSsnapshotdeliveryprogress** tabela, e **0** significa que nenhum erro será retornado.  
  
 [ **@drop_table**=] **'***drop_table***'**  
 Especifica se deve descartar ou truncar as tabela que contém informações sobre o progresso do instantâneo. *drop_table* é **nvarchar (5)**, com um padrão de **FALSE**. false significa que a tabela é truncada, e true significa que a tabela é removida.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_resetsnapshotdeliveryprogress** remove todas as linhas as **MSsnapshotdeliveryprogress** tabela. Isso remove efetivamente todos os metadados deixados para trás no banco de dados de assinatura por qualquer progresso anterior feito nos processos de entrega de instantâneo.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou o **db_owner** banco de dados fixa podem executar **sp_resetsnapshotdeliveryprogress**.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
