---
title: sp_dropdistributiondb (Transact-SQL) | Microsoft Docs
description: Descarta um banco de dados de distribuição e os arquivos usados por ele se eles não forem usados por outro banco de dados. Esse procedimento armazenado é executado no distribuidor em qualquer banco de dados.
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropdistributiondb_TSQL
- sp_dropdistributiondb
helpviewer_keywords:
- sp_dropdistributiondb
ms.assetid: b6dd1846-2259-4d29-93af-a70a5d25a0c5
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ff09552fcc8a79abcae877191b4456c0958d1ea2
ms.sourcegitcommit: 19ff45e8a2f4193fe8827f39258d8040a88befc7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2020
ms.locfileid: "83807756"
---
# <a name="sp_dropdistributiondb-transact-sql"></a>sp_dropdistributiondb (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Descarta um banco de dados de distribuição. Descartará os arquivos físicos usados pelo banco de dados se eles não forem usados por outro banco de dados. Esse procedimento armazenado é executado no Distribuidor em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dropdistributiondb [ @database= ] 'database'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @database = ] 'database'`É o banco de dados a ser solto. o *banco de dados* é **sysname**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_dropdistributiondb** é usado em todos os tipos de replicação.  
  
 Esse procedimento armazenado deve ser executado antes de descartar o distribuidor executando **sp_dropdistributor**.  
  
 **sp_dropdistributiondb** também removerá um trabalho de Queue Reader Agent para o banco de dados de distribuição, se existir um.  
  
 Para desabilitar distribuição, o banco de dados de distribuição deve estar online. Se um instantâneo do banco de dados existir para o banco de dados de distribuição, deverá ser descartado antes de desabilitar distribuição. O instantâneo do banco de dados é uma cópia offline somente leitura de um banco de dados e não está relacionado a um instantâneo de replicação. Para obter mais informações, consulte [Instantâneos de banco de dados &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md).  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_DropDistPub](../../relational-databases/replication/codesnippet/tsql/sp-dropdistributiondb-tr_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_dropdistributiondb**.  
  
## <a name="see-also"></a>Consulte Também  
 [Desabilitar publicação e distribuição](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [&#41;&#40;Transact-SQL de sp_adddistributiondb](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_changedistributiondb](../../relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpdistributiondb](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
