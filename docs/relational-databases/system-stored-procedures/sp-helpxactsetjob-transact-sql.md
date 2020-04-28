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
ms.openlocfilehash: 0fdd70480a63e334aa3e178d19287b30937e2f53
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74056790"
---
# <a name="sp_helpxactsetjob-transact-sql"></a>sp_helpxactsetjob (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exibe informações sobre o trabalho Xactset para um Editor Oracle. Esse procedimento armazenado é executado no Distribuidor em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpxactsetjob [ @publisher = ] 'publisher'   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'`É o nome do não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador ao qual o trabalho pertence. o *Publicador* é **sysname**, sem padrão.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**jobnumber**|**int**|Número do trabalho Oracle.|  
|**LASTDATE**|**varchar (22)**|Última data de execução do trabalho.|  
|**thisdate**|**varchar (22)**|Hora da alteração|  
|**nextdate**|**varchar (22)**|Próxima data de execução do trabalho.|  
|**broken**|**varchar(1)**|Sinalizador que indica se o trabalho foi interrompido.|  
|**intervalo**|**varchar (200)**|Intervalo para o trabalho.|  
|**sucedi**|**int**|Número de falhas para o trabalho.|  
|**xactsetjobwhat**|**varchar (200)**|Nome do procedimento executado pelo trabalho.|  
|**xactsetjob**|**varchar(1)**|Status do trabalho, que pode ser um dos seguintes:<br /><br /> **1** -o trabalho está habilitado.<br /><br /> **0** -o trabalho está desabilitado.|  
|**xactsetlonginterval**|**int**|Intervalo longo para o trabalho.|  
|**xactsetlongthreshold**|**int**|Limite longo para o trabalho.|  
|**xactsetshortinterval**|**int**|Intervalo curto para o trabalho.|  
|**xactsetshortthreshold**|**int**|Limite curto para o trabalho.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helpxactsetjob** é usado na replicação de instantâneos e na replicação transacional para Publicadores Oracle.  
  
 **sp_helpxactsetjob** sempre retorna as configurações atuais para o trabalho de Xactset (HREPL_XactSetJob) no Publicador. Se o trabalho Xactset estiver atualmente na fila de trabalhos, retornará adicionalmente atributos de trabalho da exibição de dicionário de dados USER_JOB criada na conta do administrador no Editor Oracle.  
  
## <a name="permissions"></a>Permissões  
 Somente um membro da função de servidor fixa **sysadmin** pode executar **sp_helpxactsetjob**.  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar o trabalho do conjunto de transações para um Publicador Oracle &#40;Programação Transact-SQL de replicação&#41;](../../relational-databases/replication/administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)   
 [&#41;&#40;Transact-SQL de sp_publisherproperty](../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md)  
  
  
