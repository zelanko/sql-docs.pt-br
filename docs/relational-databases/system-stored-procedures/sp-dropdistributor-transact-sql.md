---
title: sp_dropdistributor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- sp_dropdistributor
- sp_dropdistributor_TSQL
helpviewer_keywords:
- sp_dropdistributor
ms.assetid: 0644032f-5ff0-4718-8dde-321bc9967a03
caps.latest.revision: 33
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 0288daacc8f88decf6af642d0a864f3f08057fbd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32989731"
---
# <a name="spdropdistributor-transact-sql"></a>sp_dropdistributor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Desinstala o Distribuidor. Esse procedimento armazenado é executado no Distribuidor ou em qualquer banco de dados, exceto no banco de dados de distribuição.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dropdistributor [ [ @no_checks= ] no_checks ]   
    [ , [ @ignore_distributor= ] ignore_distributor ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@no_checks=**] *no_checks*  
 Indica se os objetos dependentes devem ser verificados antes da remoção do Distribuidor. *no_checks* é **bit**, com um padrão de 0.  
  
 Se **0**, **sp_dropdistributor** verifica para garantir que todos os objetos de publicação e distribuição, além do distribuidor tem sido descartados.  
  
 Se **1**, **sp_dropdistributor** descarta todos os objetos de publicação e distribuição antes de desinstalar o distribuidor.  
  
 [  **@ignore_distributor=**] *ignore_distributor*  
 Indica se esse procedimento armazenado será executado sem se conectar ao Distribuidor. *ignore_distributor* é **bit**, com um padrão de **0**.  
  
 Se **0**, **sp_dropdistributor** conecta-se ao distribuidor e remove todos os objetos de replicação. Se **sp_dropdistributor** não pode se conectar ao distribuidor, o procedimento armazenado falhará.  
  
 Se **1**, nenhuma conexão é feita com o distribuidor e os objetos de replicação não são removidos. Será usado se o Distribuidor estiver sendo desinstalado ou estiver permanentemente offline. Os objetos desse Publicador no Distribuidor não serão removidos até que o Distribuidor seja reinstalado futuramente.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_dropdistributor** é usado em todos os tipos de replicação.  
  
 Se outros objetos de distribuição ou o publicador existem no servidor, **sp_dropdistributor** falhará a menos que **@no_checks** é definido como **1**.  
  
 Esse procedimento armazenado deve ser executado depois de descartar o banco de dados de distribuição executando **sp_dropdistributiondb**.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_DropDistPub](../../relational-databases/replication/codesnippet/tsql/sp-dropdistributor-trans_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** pode executar a função de servidor fixa **sp_dropdistributor**.  
  
## <a name="see-also"></a>Consulte também  
 [Desabilitar a publicação e a distribuição](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [sp_adddistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md)   
 [sp_changedistributor_property &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistributor-property-transact-sql.md)   
 [sp_helpdistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
