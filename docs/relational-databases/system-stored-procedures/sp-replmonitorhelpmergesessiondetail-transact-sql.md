---
title: sp_replmonitorhelpmergesessiondetail (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorhelpmergesessiondetail
- sp_replmonitorhelpmergesessiondetail_TSQL
helpviewer_keywords:
- sp_replmonitorhelpmergesessiondetail
ms.assetid: 805c92fc-3169-410c-984d-f37e063b791d
author: stevestein
ms.author: sstein
ms.openlocfilehash: c9f883b7eafc59a3d9d93541e07fe4c4db08b9c9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67950590"
---
# <a name="spreplmonitorhelpmergesessiondetail-transact-sql"></a>sp_replmonitorhelpmergesessiondetail (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações detalhadas, de nível de artigo, sobre uma sessão específica de replicação do Merge Agent usada para monitorar replicação de mesclagem. O conjunto de resultados inclui uma linha de detalhes para cada artigo sincronizado durante a sessão. Também uma inclui uma linha que representa a inicialização da sessão e linhas que resumem as fases de carregamento e download da sessão. Esse procedimento armazenado é executado no Distribuidor, no banco de dados de distribuição, ou no Assinante, no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_replmonitorhelpmergesessiondetail [ @session_id = ] session_id  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @session_id = ] session_id` Especifica uma sessão de agente. *session_id* está **int** sem nenhum padrão.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**PhaseID**|**int**|É a fase da sessão de sincronização que pode ser uma das seguintes:<br /><br /> **0** = inicialização ou linha de resumo<br /><br /> **1** = carregamento<br /><br /> **2** = download|  
|**ArticleName**|**sysname**|É o nome do artigo que está sendo sincronizado. **ArticleName** também contém informações resumidas de linhas no conjunto de resultados que não representam detalhes do artigo.|  
|**PercentComplete**|**decimal**|Indica a porcentagem do total de alterações aplicada a uma linha de detalhe de um determinado artigo em sessões atualmente em execução ou com falha.|  
|**RelativeCost**|**decimal**|Indica o tempo gasto para sincronizar o artigo como uma porcentagem do tempo de sincronização total para a sessão.|  
|**Duration**|**int**|Duração da sessão do agente.|  
|**Insere**|**int**|Número de inserções em uma sessão.|  
|**Updates**|**int**|Número de atualizações em uma sessão.|  
|**Deletes**|**int**|Número de exclusões em uma sessão.|  
|**Conflicts**|**int**|Número de conflitos ocorrido em uma sessão.|  
|**ErrorID**|**int**|ID de um erro de sessão.|  
|**SeqNo**|**int**|Ordem das sessões no conjunto de resultados.|  
|**RowType**|**int**|Indica que tipo de informação que cada linha no conjunto de resultados representa.<br /><br /> **0** = inicialização<br /><br /> **1** = resumo de carregamento<br /><br /> **2** = detalhes do carregamento do artigo<br /><br /> **3** = resumo de download<br /><br /> **4** = detalhes de download do artigo|  
|**SchemaChanges**|**int**|Número de alterações de esquema em uma sessão.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_replmonitorhelpmergesessiondetail** é usado para monitorar a replicação de mesclagem.  
  
 Quando executado no assinante, **sp_replmonitorhelpmergesessiondetail** só retorna informações detalhadas sobre as últimas 5 sessões do Merge Agent.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **db_owner** ou **replmonitor** banco de dados fixa no banco de dados de distribuição no distribuidor ou no banco de dados de assinatura no assinante podem executar **SP _ replmonitorhelpmergesessiondetail**.  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar programaticamente a replicação](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
