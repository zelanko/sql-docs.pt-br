---
title: sp_helparticledts (Transact-SQL) | Microsoft Docs
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
- sp_helparticledts
- sp_helparticledts_TSQL
helpviewer_keywords:
- sp_helparticledts
ms.assetid: cd1aed60-e056-4ff3-86ee-62b19433d890
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: e296b7e03f64fc95338750ef57360dd3f250af98
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32994743"
---
# <a name="sphelparticledts-transact-sql"></a>sp_helparticledts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Usado para obter informações sobre nomes corretos de tarefas personalizadas para usar ao criar uma assinatura de transformação usando [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helparticledts [ @publication = ] 'publication', [ @article = ] 'article'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication =**] **'***publicação***'**  
 É o nome da publicação. *publicação* é **sysname**, sem padrão.  
  
 [  **@article=**] **'***artigo***'**  
 É o nome de um artigo na publicação. *artigo* é **sysname**, sem padrão.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**pre_script_ignore_error_task_name**|**sysname**|Nome de tarefa para a tarefa de programação que ocorre antes que os dados de instantâneo sejam copiados. A execução do programa deve continuar se um erro de script for encontrado.|  
|**pre_script_task_name**|**sysname**|Nome de tarefa para a tarefa de programação que ocorre antes que os dados de instantâneo sejam copiados. A execução do programa para ao encontrar um erro.|  
|**transformation_task_name**|**sysname**|Nome de tarefa para a tarefa da programação, ao usar uma tarefa de Consulta Controlada por Dados.|  
|**post_script_ignore_error_task_name**|**sysname**|Nome de tarefa para a tarefa de programação que ocorre depois que os dados do instantâneo são copiados. A execução do programa deve continuar se um erro de script for encontrado.|  
|**post_script_task_name**|**sysname**|Nome de tarefa para a tarefa de programação que ocorre depois que os dados do instantâneo são copiados. A execução do programa para ao encontrar um erro.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_helparticledts** é usado em replicação de instantâneo e replicação transacional.  
  
 Existem convenções de nomenclatura, solicitadas pelos agentes de replicação, que devem ser seguidas ao nomear tarefas em um programa DTS (Data Transformation Services). Para tarefas personalizadas, como uma tarefa Executar SQL, o nome é uma cadeia de caracteres concatenada que consiste no nome do artigo, no prefixo e em uma parte opcional. Ao escrever o código, se você não tiver certeza dos nomes das tarefas, o conjunto de resultados dá os nomes de tarefas que devem ser usados.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função fixa de servidor e o **db_owner** pode executar a função de banco de dados fixa **sp_helparticledts**.  
  
  
