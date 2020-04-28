---
title: sp_replmonitorhelppublisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorhelppublisher_TSQL
- sp_replmonitorhelppublisher
helpviewer_keywords:
- sp_replmonitorhelppublisher
ms.assetid: 171501fe-4b74-4647-96c3-7691c777e01b
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5db934c972282609e9b2978a66034b39bb38a092
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68771186"
---
# <a name="sp_replmonitorhelppublisher-transact-sql"></a>sp_replmonitorhelppublisher (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Retorna informações do status atual para um ou mais Publicadores associados a um Distribuidor. Esse procedimento armazenado, usado para monitorar a replicação, é executado no Distribuidor, no banco de dados de distribuição.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_replmonitorhelppublisher [ [ @publisher = ] 'publisher' ]  
    [ , [ @refreshpolicy = ] refreshpolicy ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'`É o nome do Publicador cujo status está sendo monitorado. o *Publicador* é **sysname**, com um valor padrão de NULL. Se for NULL, as informações serão retornadas para todos os Publicadores que usam o Distribuidor.  
  
`[ @refreshpolicy = ] refreshpolicy`Somente para uso interno.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**programa**|**sysname**|É o nome de um Publicador.|  
|**distribution_db**|**sysname**|É o nome do banco de dados de distribuição usado por um determinado Publicador.|  
|**status**|**int**|Status máximo de todos os agentes de replicação associados com publicações neste Publicador, que pode ter um destes valores.<br /><br /> **1** = iniciado<br /><br /> **2** = com êxito<br /><br /> **3** = em andamento<br /><br /> **4** = ocioso<br /><br /> **5** = repetindo<br /><br /> **6** = com falha|  
|**warning**|**int**|Aviso de limite máximo gerado por uma assinatura pertencente a uma publicação neste Publicador, que pode ser o resultado do OR lógico de um ou mais destes valores.<br /><br /> **1** = expiração-uma assinatura para uma publicação transacional não foi sincronizada dentro do limite do período de retenção.<br /><br /> **2** = latência-o tempo necessário para replicar dados de um Publicador transacional para o assinante excede o limite, em segundos.<br /><br /> **4** = mergeexpiration-uma assinatura para uma publicação de mesclagem não foi sincronizada dentro do limite do período de retenção.<br /><br /> **8** = mergefastrunduration-o tempo necessário para concluir a sincronização de uma assinatura de mesclagem excede o limite, em segundos, em uma conexão de rede rápida.<br /><br /> **16** = mergeslowrunduration-o tempo necessário para concluir a sincronização de uma assinatura de mesclagem excede o limite, em segundos, em uma conexão de rede lenta ou discada.<br /><br /> **32** = mergefastrunspeed-a taxa de entrega para linhas durante a sincronização de uma assinatura de mesclagem não conseguiu manter a taxa de limite, em linhas por segundo, em uma conexão de rede rápida.<br /><br /> **64** = mergeslowrunspeed-a taxa de entrega para linhas durante a sincronização de uma assinatura de mesclagem não conseguiu manter a taxa de limite, em linhas por segundo, em uma conexão de rede lenta ou discada.|  
|**publicationcount**|**int**|É o número de publicações que pertencem ao Publicador.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_replmonitorhelppublisher** é usado com todos os tipos de replicação.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** no distribuidor ou membros das funções de banco de dados fixas **db_owner** ou **replmonitor** no banco de dados de distribuição podem executar **sp_replmonitorhelppublisher**.  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar a replicação de forma programática](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
