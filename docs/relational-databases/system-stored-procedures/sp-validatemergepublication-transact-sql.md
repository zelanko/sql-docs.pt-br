---
title: sp_validatemergepublication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_validatemergepublication
- sp_validatemergepublication_TSQL
helpviewer_keywords:
- sp_validatemergepublication
ms.assetid: 5a862f1a-2be1-4758-9954-4cdc8c77d149
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6a0ca36329c8ddb68c9727fe1b9d2cf17674c93a
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82808754"
---
# <a name="sp_validatemergepublication-transact-sql"></a>sp_validatemergepublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Executa uma validação em todas as publicações, na qual todas as assinaturas (push, pull e anônima) serão validadas uma vez. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_validatemergepublication [@publication=] 'publication'  
        , [ @level = ] level  
```  
  
## <a name="arguments"></a>Argumentos  
 [** \@ publicação =**] **'***publicação***'**  
 É o nome da publicação. a *publicação* é **sysname**, sem padrão.  
  
`[ @level = ] level`É o tipo de validação a ser executada. o *nível* é **tinyint**, sem padrão. O nível pode ser um destes valores:  
  
|Valor de nível|Descrição|  
|-----------------|-----------------|  
|**1**|Validação só de número de linhas.|  
|**2**|Validação de número de linhas e soma de verificação. Para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] assinantes, isso é definido automaticamente como **3**.|  
|**3**|Esse é o valor recomendado.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_validatemergepublication** é usado na replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_validatemergepublication**.  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do sistema &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Validar dados replicados](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [&#41;&#40;Transact-SQL de sp_validatemergesubscription](../../relational-databases/system-stored-procedures/sp-validatemergesubscription-transact-sql.md)  
  
  
