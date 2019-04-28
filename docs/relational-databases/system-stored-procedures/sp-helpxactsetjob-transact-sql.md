---
title: sp_helpxactsetjob (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpxactsetjob
- sp_helpxactsetjob_TSQL
helpviewer_keywords:
- sp_helpxactsetjob
ms.assetid: 242cea3e-e6ac-4f84-a072-b003b920eb33
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7402fcc825e6f537703268c1fd3fead9c88b1f5e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62959606"
---
# <a name="sphelpxactsetjob-transact-sql"></a>sp_helpxactsetjob (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exibe informações sobre o trabalho Xactset para um Editor Oracle. Esse procedimento armazenado é executado no Distribuidor em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpxactsetjob [ @publisher = ] 'publisher'   
```  
  
## <a name="arguments"></a>Argumentos  
 [**@publisher** = ] **'***publisher***'**  
 É o nome do não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador ao qual o trabalho pertence. *Publisher* está **sysname**, sem padrão.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**jobnumber**|**int**|Número do trabalho Oracle.|  
|**lastdate**|**varchar(22)**|Última data de execução do trabalho.|  
|**thisdate**|**varchar(22)**|Hora da alteração|  
|**nextdate**|**varchar(22)**|Próxima data de execução do trabalho.|  
|**broken**|**varchar(1)**|Sinalizador que indica se o trabalho foi interrompido.|  
|**interval**|**varchar(200)**|Intervalo para o trabalho.|  
|**failures**|**int**|Número de falhas para o trabalho.|  
|**xactsetjobwhat**|**varchar(200)**|Nome do procedimento executado pelo trabalho.|  
|**xactsetjob**|**varchar(1)**|Status do trabalho, que pode ser um dos seguintes:<br /><br /> **1** -o trabalho está habilitado.<br /><br /> **0** -o trabalho está desabilitado.|  
|**xactsetlonginterval**|**int**|Intervalo longo para o trabalho.|  
|**xactsetlongthreshold**|**int**|Limite longo para o trabalho.|  
|**xactsetshortinterval**|**int**|Intervalo curto para o trabalho.|  
|**xactsetshortthreshold**|**int**|Limite curto para o trabalho.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helpxactsetjob** é usado em replicação de instantâneo e replicação transacional para editores Oracle.  
  
 **sp_helpxactsetjob** sempre retorna as configurações atuais para o trabalho de Xactset (HREPL_XactSetJob) no publicador. Se o trabalho Xactset estiver atualmente na fila de trabalhos, retornará adicionalmente atributos de trabalho da exibição de dicionário de dados USER_JOB criada na conta do administrador no Editor Oracle.  
  
## <a name="permissions"></a>Permissões  
 Somente um membro dos **sysadmin** pode executar a função de servidor fixa **sp_helpxactsetjob**.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar o trabalho do conjunto de transações para um Publicador Oracle &#40;programação Transact-SQL de replicação&#41;](../../relational-databases/replication/administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)   
 [sp_publisherproperty &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md)  
  
  
