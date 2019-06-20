---
title: sp_get_distributor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_get_distributor
- sp_get_distributor_TSQL
helpviewer_keywords:
- sp_get_distributor
ms.assetid: f0134448-bc17-4f2f-bd81-619351ce56ac
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ccdc8529bb62e4e1db15f0a5ea85a64c5b679abf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62520988"
---
# <a name="spgetdistributor-transact-sql"></a>sp_get_distributor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Determina se um Distribuidor é instalado em um servidor. Esse procedimento armazenado é executado no computador onde o Distribuidor está sendo procurado, em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_get_distributor   
```  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**installed**|**int**|**0** = não; **1** = Sim|  
|**servidor de distribuição**|**sysname**|O nome do servidor Distribuidor.|  
|**BD de distribuição instalado**|**int**|**0** = não; **1** = Sim|  
|**é o publicador de distribuição**|**int**|**0** = não; **1** = Sim|  
|**possui publicador de distribuição remoto**|**int**|**0** = não; **1** = Sim|  
  
## <a name="remarks"></a>Comentários  
 **sp_get_distributor** é usado principalmente pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] no instantâneo, transacional e replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Qualquer usuário pode executar **sp_get_distributor**. Um conjunto de resultado não nulo é retornado quando este armazenado procedimento é executado por membros dos **db_owner** ou **replmonitor** banco de dados fixa no banco de dados de distribuição ou os membros a  **db_owner** função de banco de dados fixa em pelo menos um banco de dados publicado. Um conjunto de resultados nulos também é retornado quando esse procedimento armazenado é executado pelos usuários na lista de acesso da publicação (PAL) pelo menos um banco de dados publicado ou na PAL do banco de dados de distribuição para um publicador não SQL Server, também pode executar **sp _get_distributor**.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar a publicação e a distribuição](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Script de informações do Distribuidor e Publicador](../../relational-databases/replication/administration/distributor-and-publisher-information-script.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
