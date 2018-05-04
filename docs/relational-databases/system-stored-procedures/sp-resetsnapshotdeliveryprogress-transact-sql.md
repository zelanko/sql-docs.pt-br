---
title: sp_resetsnapshotdeliveryprogress (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_resetsnapshotdeliveryprogress
- sp_resetsnapshotdeliveryprogress_TSQL
helpviewer_keywords:
- sp_resetsnapshotdeliveryprogress
ms.assetid: 5df7d86b-d343-4d9b-88b1-74429ed092e6
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 86ff0f1ffbe513d4d74c1cd5dffdcba6d63dea6c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
 Especifica a quantidade de informações a ser retornada. *verbose_level*é **int**, com um padrão de **1**. Um valor de **1** significa que um erro será retornado se os bloqueios necessários não podem ser obtidos no **MSsnapshotdeliveryprogress** tabela, e **0** significa que nenhum erro será retornado.  
  
 [ **@drop_table**=] **'***drop_table***'**  
 Especifica se deve descartar ou truncar as tabela contendo informações sobre o progresso do instantâneo. *drop_table* é **nvarchar (5)**, com um padrão de **FALSE**. false significa que a tabela é truncada, e true significa que a tabela é removida.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_resetsnapshotdeliveryprogress** remove todas as linhas de **MSsnapshotdeliveryprogress** tabela. Isso remove efetivamente todos os metadados deixados para trás no banco de dados de assinatura por qualquer progresso anterior feito nos processos de entrega de instantâneo.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_resetsnapshotdeliveryprogress**.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
