---
title: sp_helparticledts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helparticledts
- sp_helparticledts_TSQL
helpviewer_keywords:
- sp_helparticledts
ms.assetid: cd1aed60-e056-4ff3-86ee-62b19433d890
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1b5355ea4993944a4a47b59eb2cad0565e0c396c
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82815448"
---
# <a name="sp_helparticledts-transact-sql"></a>sp_helparticledts (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Usado para obter informações sobre nomes corretos de tarefas personalizadas para usar ao criar uma assinatura de transformação usando [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helparticledts [ @publication = ] 'publication', [ @article = ] 'article'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação. a *publicação* é **sysname**, sem padrão.  
  
`[ @article = ] 'article'`É o nome de um artigo na publicação. o *artigo* é **sysname**, sem padrão.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**pre_script_ignore_error_task_name**|**sysname**|Nome de tarefa para a tarefa de programação que ocorre antes que os dados de instantâneo sejam copiados. A execução do programa deve continuar se um erro de script for encontrado.|  
|**pre_script_task_name**|**sysname**|Nome de tarefa para a tarefa de programação que ocorre antes que os dados de instantâneo sejam copiados. A execução do programa para ao encontrar um erro.|  
|**transformation_task_name**|**sysname**|Nome de tarefa para a tarefa da programação, ao usar uma tarefa de Consulta Controlada por Dados.|  
|**post_script_ignore_error_task_name**|**sysname**|Nome de tarefa para a tarefa de programação que ocorre depois que os dados do instantâneo são copiados. A execução do programa deve continuar se um erro de script for encontrado.|  
|**post_script_task_name**|**sysname**|Nome de tarefa para a tarefa de programação que ocorre depois que os dados do instantâneo são copiados. A execução do programa para ao encontrar um erro.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helparticledts** é usado na replicação de instantâneo e na replicação transacional.  
  
 Existem convenções de nomenclatura, solicitadas pelos agentes de replicação, que devem ser seguidas ao nomear tarefas em um programa DTS (Data Transformation Services). Para tarefas personalizadas, como uma tarefa Executar SQL, o nome é uma cadeia de caracteres concatenada que consiste no nome do artigo, no prefixo e em uma parte opcional. Ao escrever o código, se você não tiver certeza dos nomes das tarefas, o conjunto de resultados dá os nomes de tarefas que devem ser usados.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** e a função de banco de dados fixa **db_owner** podem executar **sp_helparticledts**.  
  
  
