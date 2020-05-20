---
title: sp_addmergepartition (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergepartition
- sp_addmergepartition_TSQL
helpviewer_keywords:
- sp_addmergepartition
ms.assetid: 02a5f46b-e5ff-4932-a3ff-7f0fd82d0981
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0af6f62a45dd519f8a63839ae1435815569b93be
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82831770"
---
# <a name="sp_addmergepartition-transact-sql"></a>sp_addmergepartition (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Cria uma partição filtrada dinamicamente para uma assinatura filtrada pelos valores de [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) ou [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) no Assinante. Esse procedimento armazenado é executado no Publicador, no banco de dados que está sendo publicado, e é usado para gerar partições manualmente.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addmergepartition [ @publication = ] 'publication'  
        , [ @suser_sname = ] 'suser_sname'  
        , [ @host_name = ] 'host_name'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É a publicação de mesclagem na qual a partição está sendo criada. a *publicação* é **sysname**, sem padrão. Se *SUSER_SNAME* for especificado, o valor do *nome do host* deverá ser nulo.  
  
`[ @suser_sname = ] 'suser_sname'`É o valor usado ao criar a partição para uma assinatura que é filtrada pelo valor da função [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) no Assinante. *SUSER_SNAME* é **sysname**, sem padrão.  
  
`[ @host_name = ] 'host_name'`É o valor usado ao criar a partição para uma assinatura que é filtrada pelo valor da função [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) no Assinante. *HOST_NAME* é **sysname**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_addmergepartition** é usado na replicação de mesclagem.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_MergeDynamicPubPlusPartition](../../relational-databases/replication/codesnippet/tsql/sp-addmergepartition-tra_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_addmergepartition**.  
  
## <a name="see-also"></a>Consulte Também  
 [Criar um instantâneo para uma publicação de mesclagem com filtros com parâmetros](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)  
  
  
