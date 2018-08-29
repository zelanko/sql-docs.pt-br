---
title: sp_replmonitorhelppublisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
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
- sp_replmonitorhelppublisher_TSQL
- sp_replmonitorhelppublisher
helpviewer_keywords:
- sp_replmonitorhelppublisher
ms.assetid: 171501fe-4b74-4647-96c3-7691c777e01b
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9f2b7593890e4c3bab83855e74bb370e1411e74d
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43028221"
---
# <a name="spreplmonitorhelppublisher-transact-sql"></a>sp_replmonitorhelppublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações do status atual para um ou mais Publicadores associados a um Distribuidor. Esse procedimento armazenado, usado para monitorar a replicação, é executado no Distribuidor, no banco de dados de distribuição.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_replmonitorhelppublisher [ [ @publisher = ] 'publisher' ]  
    [ , [ @refreshpolicy = ] refreshpolicy ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@publisher** =] **'***publisher***'**  
 É o nome do Publicador do qual o status está sendo monitorado. *Publisher* está **sysname**, com um valor padrão de NULL. Se for NULL, as informações serão retornadas para todos os Publicadores que usam o Distribuidor.  
  
 [  **@refreshpolicy=** ] *refreshpolicy*  
 Somente para uso interno.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|É o nome de um Publicador.|  
|**distribution_db**|**sysname**|É o nome do banco de dados de distribuição usado por um determinado Publicador.|  
|**status**|**int**|Status máximo de todos os agentes de replicação associados com publicações neste Publicador, que pode ter um destes valores.<br /><br /> **1** = iniciado<br /><br /> **2** = foi bem-sucedida<br /><br /> **3** = em andamento<br /><br /> **4** = ocioso<br /><br /> **5** = tentando novamente<br /><br /> **6** = falha|  
|**Aviso**|**int**|Aviso de limite máximo gerado por uma assinatura pertencente a uma publicação neste Publicador, que pode ser o resultado do OR lógico de um ou mais destes valores.<br /><br /> **1** = expiration – uma assinatura para uma publicação transacional não foi sincronizada dentro do limite de período de retenção.<br /><br /> **2** = latency – o tempo necessário para replicar dados de um publicador transacional para o assinante excede o limite, em segundos.<br /><br /> **4** = mergeexpiration – uma assinatura para uma publicação de mesclagem não foi sincronizada dentro do limite de período de retenção.<br /><br /> **8** = mergefastrunduration – o tempo necessário para concluir a sincronização de uma assinatura de mesclagem excede o limite, em segundos, em uma conexão de rede rápida.<br /><br /> **16** = mergeslowrunduration - o tempo necessário para concluir a sincronização de uma assinatura de mesclagem excede o limite, em segundos, em uma conexão de rede lenta ou discada.<br /><br /> **32** = mergefastrunspeed – a taxa de entrega de linhas durante a sincronização de uma assinatura de mesclagem falhou em manter a taxa de limite, em linhas por segundo, em uma conexão de rede rápida.<br /><br /> **64** = mergeslowrunspeed – a taxa de entrega de linhas durante a sincronização de uma assinatura de mesclagem falhou em manter a taxa de limite, em linhas por segundo, em uma conexão de rede lenta ou discada.|  
|**publicationcount**|**int**|É o número de publicações que pertencem ao Publicador.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_replmonitorhelppublisher** é usado com todos os tipos de replicação.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa no distribuidor ou membros da **db_owner** ou **replmonitor** funções de banco de dados fixa no banco de dados de distribuição podem Execute **sp_replmonitorhelppublisher**.  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar programaticamente a replicação](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
