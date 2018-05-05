---
title: sp_get_distributor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- sp_get_distributor
- sp_get_distributor_TSQL
helpviewer_keywords:
- sp_get_distributor
ms.assetid: f0134448-bc17-4f2f-bd81-619351ce56ac
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 71be140eb309c36a9801f7d32b45123100704333
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**Instalado**|**Int**|**0** = não; **1** = Sim|  
|**servidor de distribuição**|**sysname**|O nome do servidor Distribuidor.|  
|**banco de dados de distribuição instalado**|**Int**|**0** = não; **1** = Sim|  
|**é o publicador de distribuição**|**Int**|**0** = não; **1** = Sim|  
|**possui publicador de distribuição remoto**|**Int**|**0** = não; **1** = Sim|  
  
## <a name="remarks"></a>Remarks  
 **sp_get_distributor** é usado principalmente pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] no instantâneo, transacional e replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Qualquer usuário pode executar **sp_get_distributor**. Um conjunto de resultados não nulo é retornado quando este armazenado procedimento é executado por membros do **db_owner** ou **replmonitor** banco de dados fixa no banco de dados de distribuição ou membros do  **db_owner** função de banco de dados fixa pelo menos um banco de dados publicado. Um conjunto de resultados nulos também é retornado quando esse procedimento armazenado é executado por usuários na lista de acesso da publicação (PAL) pelo menos um banco de dados publicado ou da PAL do banco de dados de distribuição para um publicador não SQL Server, também podem executar **sp _get_distributor**.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar a publicação e a distribuição](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Script de informações do Distribuidor e Publicador](../../relational-databases/replication/administration/distributor-and-publisher-information-script.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
