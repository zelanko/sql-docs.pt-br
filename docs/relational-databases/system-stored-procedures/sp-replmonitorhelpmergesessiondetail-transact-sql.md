---
title: sp_replmonitorhelpmergesessiondetail (T-SQL)
description: Descreve o sp_replmonitorhelpmergesessiondetail procedimento armazenado que retorna informações detalhadas em nível de artigo sobre uma sessão de Agente de Mesclagem de replicação específica.
ms.custom: seo-lt-2019
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
ms.openlocfilehash: b5e29916d4dc8419311c9639cc5321b1cf391940
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75321613"
---
# <a name="sp_replmonitorhelpmergesessiondetail-transact-sql"></a>sp_replmonitorhelpmergesessiondetail (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Retorna informações detalhadas, de nível de artigo, sobre uma sessão específica de replicação do Merge Agent usada para monitorar replicação de mesclagem. O conjunto de resultados inclui uma linha de detalhes para cada artigo sincronizado durante a sessão. Também uma inclui uma linha que representa a inicialização da sessão e linhas que resumem as fases de carregamento e download da sessão. Esse procedimento armazenado é executado no Distribuidor, no banco de dados de distribuição, ou no Assinante, no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_replmonitorhelpmergesessiondetail [ @session_id = ] session_id  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @session_id = ] session_id`Especifica uma sessão de agente. *session_id* é **int** sem padrão.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**PhaseID**|**int**|É a fase da sessão de sincronização que pode ser uma das seguintes:<br /><br /> **0** = linha de inicialização ou Resumo<br /><br /> **1** = carregar<br /><br /> **2** = baixar|  
|**ArticleName**|**sysname**|É o nome do artigo que está sendo sincronizado. O **artigoname** também contém informações resumidas para linhas no conjunto de resultados que não representam os detalhes do artigo.|  
|**PercentComplete**|**decimal**|Indica a porcentagem do total de alterações aplicada a uma linha de detalhe de um determinado artigo em sessões atualmente em execução ou com falha.|  
|**RelativeCost**|**decimal**|Indica o tempo gasto para sincronizar o artigo como uma porcentagem do tempo de sincronização total para a sessão.|  
|**Duration**|**int**|Duração da sessão do agente.|  
|**Insere**|**int**|Número de inserções em uma sessão.|  
|**Atualizações**|**int**|Número de atualizações em uma sessão.|  
|**Deletes**|**int**|Número de exclusões em uma sessão.|  
|**Conflicts**|**int**|Número de conflitos ocorrido em uma sessão.|  
|**ErrorID**|**int**|ID de um erro de sessão.|  
|**SeqNo**|**int**|Ordem das sessões no conjunto de resultados.|  
|**RowType**|**int**|Indica que tipo de informação que cada linha no conjunto de resultados representa.<br /><br /> **0** = inicialização<br /><br /> **1** = carregar Resumo<br /><br /> **2** = detalhes do carregamento do artigo<br /><br /> **3** = Resumo de download<br /><br /> **4** = detalhes do download do artigo|  
|**SchemaChanges**|**int**|Número de alterações de esquema em uma sessão.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_replmonitorhelpmergesessiondetail** é usado para monitorar a replicação de mesclagem.  
  
 Quando executado no Assinante, **sp_replmonitorhelpmergesessiondetail** retorna apenas informações detalhadas sobre as últimas 5 sessões de agente de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de banco de dados fixa **db_owner** ou **replmonitor** no banco de dados de distribuição no distribuidor ou no banco de dados de assinatura no assinante podem executar **sp_replmonitorhelpmergesessiondetail**.  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar programaticamente a replicação](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
