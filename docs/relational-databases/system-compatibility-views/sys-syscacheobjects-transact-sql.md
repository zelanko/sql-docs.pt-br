---
title: syscacheobjects (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-compatibility-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.syscacheobjects_TSQL
- sys.syscacheobjects
- syscacheobjects
- syscacheobjects_TSQL
dev_langs: TSQL
helpviewer_keywords:
- syscacheobjects system table
- sys.syscacheobjects compatibility view
ms.assetid: 9b14f37c-b7f5-4f71-b070-cce89a83f69e
caps.latest.revision: "37"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: aee1092010168413f316e3b42083bb752f2d9cfa
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="syssyscacheobjects-transact-sql"></a>sys.syscacheobjects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém informações sobre como o cache é usado.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**BucketID**|**int**|Identificação da partição de memória. O valor indica um intervalo de 0 a (tamanho de diretório - 1). O tamanho de diretório é o tamanho da tabela de hash.|  
|**cacheobjtype**|**nvarchar(17)**|Tipo de objeto no cache:<br /><br /> Plano compilado<br /><br /> Plano executável<br /><br /> Árvore de análise<br /><br /> Cursor<br /><br /> Procedimento armazenado estendido|  
|**ObjType**|**nvarchar (8)**|Tipo de objeto:<br /><br /> Procedimento armazenado<br /><br /> Instrução preparada<br /><br /> Consulta ad hoc ([!INCLUDE[tsql](../../includes/tsql-md.md)] enviado como eventos de linguagem do **sqlcmd** ou **osql** utilitários, em vez de chamadas de procedimento remoto)<br /><br /> ReplProc (procedimento de replicação)<br /><br /> Gatilho<br /><br /> Exibição<br /><br /> Default<br /><br /> Tabela de usuário<br /><br /> Tabela do sistema<br /><br /> Verificar<br /><br /> Regra|  
|**ObjID**|**int**|Uma das chaves principais usadas para pesquisar um objeto no cache. Este é o objeto ID armazenada na **sysobjects** para objetos de banco de dados (procedimentos, exibições, gatilhos e assim por diante). Para objetos de cache como ad hoc ou SQL preparado, **objid** é um valor gerado internamente.|  
|**DBID**|**smallint**|A identificação do banco de dados no qual o objeto de cache foi compilado.|  
|**dbidexec**|**smallint**|A identificação de banco de dados da qual a consulta é executada.<br /><br /> Para a maioria dos objetos, **dbidexec** tem o mesmo valor como **dbid**.<br /><br /> Para exibições do sistema, **dbidexec** é a ID de banco de dados do qual a consulta é executada.<br /><br /> Para consultas ad hoc, **dbidexec** é 0. Isso significa **dbidexec** tem o mesmo valor como **dbid**.|  
|**UID**|**smallint**|Indica o designer do plano para planos de consulta ad hoc e planos preparados.<br /><br /> -2 = O lote enviado não depende da resolução de nome implícita e pode ser compartilhado entre usuários diferentes. Este é o método preferencial. Qualquer outro valor representa a identificação do usuário que submete a consulta no banco de dados.<br /><br /> Excederá ou retornará NULL se o número de usuários e funções exceder 32.767.|  
|**refcounts**|**int**|Número de outros objetos de cache que fazem referência a este objeto de cache. Uma contagem de 1 é a base.|  
|**usecounts**|**int**|Número de vezes em que este objeto de cache foi usado desde o começo.|  
|**pagesused**|**int**|Número de páginas consumidas pelo objeto de cache.|  
|**setopts**|**int**|Configurações da opção SET que afetam um plano compilado. Essas configurações fazem parte da chave de cache. Alterações em valores desta coluna indica que os usuários modificaram as opções SET. Essas opções incluem:<br /><br /> **ANSI_PADDING**<br /><br /> **FORCEPLAN**<br /><br /> **CONCAT_NULL_YIELDS_NULL**<br /><br /> **ANSI_WARNINGS**<br /><br /> **ANSI_NULLS**<br /><br /> **QUOTED_IDENTIFIER**<br /><br /> **ANSI_NULL_DFLT_ON**<br /><br /> **ANSI_NULL_DFLT_OFF**|  
|**LANGID**|**smallint**|Identificação de idioma A identificação de idioma da conexão que criou o objeto de cache.|  
|**DateFormat**|**smallint**|O formato de data da conexão que criou o objeto de cache.|  
|**status**|**int**|Indica se o objeto de cache é um plano de cursor. Atualmente, apenas o bit menos significativo é usado.|  
|**lasttime**|**bigint**|Somente para compatibilidade com versões anteriores. Sempre retorna 0.|  
|**maxexectime**|**bigint**|Somente para compatibilidade com versões anteriores. Sempre retorna 0.|  
|**avgexectime**|**bigint**|Somente para compatibilidade com versões anteriores. Sempre retorna 0.|  
|**lastreads**|**bigint**|Somente para compatibilidade com versões anteriores. Sempre retorna 0.|  
|**lastwrites**|**bigint**|Somente para compatibilidade com versões anteriores. Sempre retorna 0.|  
|**SqlBytes**|**int**|O comprimento em bytes da definição de procedimento ou lote enviada.|  
|**SQL**|**nvarchar(3900)**|A definição de módulo ou os primeiros 3900 caracteres do lote enviados.|  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de compatibilidade &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  

