---
title: sp_helpxactsetjob (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- sp_helpxactsetjob
- sp_helpxactsetjob_TSQL
helpviewer_keywords:
- sp_helpxactsetjob
ms.assetid: 242cea3e-e6ac-4f84-a072-b003b920eb33
caps.latest.revision: 19
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: ef643efb849a0f178ac98bf439360fca87d21983
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32997203"
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
 [**@publisher** =] **'***publicador***'**  
 É o nome do Publicador que não é do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao qual o trabalho pertence. *publicador* é **sysname**, sem padrão.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**número_do_trabalho**|**Int**|Número do trabalho Oracle.|  
|**lastdate**|**varchar(22)**|Última data de execução do trabalho.|  
|**thisdate**|**varchar(22)**|Hora da alteração|  
|**nextdate**|**varchar(22)**|Próxima data de execução do trabalho.|  
|**dividido**|**varchar (1)**|Sinalizador que indica se o trabalho foi interrompido.|  
|**Intervalo**|**varchar(200)**|Intervalo para o trabalho.|  
|**falhas**|**Int**|Número de falhas para o trabalho.|  
|**xactsetjobwhat**|**varchar(200)**|Nome do procedimento executado pelo trabalho.|  
|**xactsetjob**|**varchar (1)**|Status do trabalho, que pode ser um dos seguintes:<br /><br /> **1** -o trabalho está habilitado.<br /><br /> **0** -o trabalho está desabilitado.|  
|**xactsetlonginterval**|**Int**|Intervalo longo para o trabalho.|  
|**xactsetlongthreshold**|**Int**|Limite longo para o trabalho.|  
|**xactsetshortinterval**|**Int**|Intervalo curto para o trabalho.|  
|**xactsetshortthreshold**|**Int**|Limite curto para o trabalho.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_helpxactsetjob** é usado em replicação de instantâneo e replicação transacional para editores Oracle.  
  
 **sp_helpxactsetjob** sempre retorna as configurações atuais para o trabalho de Xactset (HREPL_XactSetJob) no publicador. Se o trabalho Xactset estiver atualmente na fila de trabalhos, retornará adicionalmente atributos de trabalho da exibição de dicionário de dados USER_JOB criada na conta do administrador no Editor Oracle.  
  
## <a name="permissions"></a>Permissões  
 Somente um membro do **sysadmin** pode executar a função de servidor fixa **sp_helpxactsetjob**.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar o trabalho do conjunto de transações para um Publicador Oracle &#40;programação Transact-SQL de replicação&#41;](../../relational-databases/replication/administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)   
 [sp_publisherproperty &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md)  
  
  
