---
title: sp_dropdistributiondb (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
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
- sp_dropdistributiondb_TSQL
- sp_dropdistributiondb
helpviewer_keywords:
- sp_dropdistributiondb
ms.assetid: b6dd1846-2259-4d29-93af-a70a5d25a0c5
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 31d57763ffed40661be4cb7eaa878a3b2e7b26c6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="spdropdistributiondb-transact-sql"></a>sp_dropdistributiondb (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Descarta um banco de dados de distribuição. Descartará os arquivos físicos usados pelo banco de dados se eles não forem usados por outro banco de dados. Esse procedimento armazenado é executado no Distribuidor em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dropdistributiondb [ @database= ] 'database'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@database=**] **'***banco de dados***'**  
 É o banco de dados a ser removido. *banco de dados* é **sysname**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_dropdistributiondb** é usado em todos os tipos de replicação.  
  
 Esse procedimento armazenado deve ser executado antes de descartar o distribuidor executando **sp_dropdistributor**.  
  
 **sp_dropdistributiondb** também remove um trabalho do Queue Reader Agent para o banco de dados de distribuição, se houver um.  
  
 Para desabilitar distribuição, o banco de dados de distribuição deve estar online. Se um instantâneo do banco de dados existir para o banco de dados de distribuição, deverá ser descartado antes de desabilitar distribuição. O instantâneo do banco de dados é uma cópia offline somente leitura de um banco de dados e não está relacionado a um instantâneo de replicação. Para obter mais informações, consulte [Instantâneos de banco de dados &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md).  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_DropDistPub](../../relational-databases/replication/codesnippet/tsql/sp-dropdistributiondb-tr_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** pode executar a função de servidor fixa **sp_dropdistributiondb**.  
  
## <a name="see-also"></a>Consulte também  
 [Desabilitar a publicação e a distribuição](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [sp_adddistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)   
 [sp_changedistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql.md)   
 [sp_helpdistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
