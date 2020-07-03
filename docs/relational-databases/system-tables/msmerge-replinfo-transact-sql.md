---
title: MSmerge_replinfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_replinfo_TSQL
- MSmerge_replinfo
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_replinfo system table
ms.assetid: b0924094-c0cc-49c1-869a-65be0d0465a0
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0add40a3062575e809b0e4c6e4f864eba6ec8e0d
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85889753"
---
# <a name="msmerge_replinfo-transact-sql"></a>MSmerge_replinfo (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela **MSmerge_replinfo** contém uma linha para cada assinatura. Essa tabela localiza informações sobre assinaturas. Essa tabela é armazenada nos bancos de dados de publicação e de assinatura.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**repid**|**uniqueidentifier**|A ID exclusiva da replicação.|  
|**use_interactive_resolver**|**bit**|Especifica se o resolvedor interativo é usado durante a reconciliação.<br /><br /> **0** = não use o resolvedor interativo.<br /><br /> **1** = usar o resolvedor interativo.|  
|**validation_level**|**int**|Tipo de validação para executar na assinatura. O nível de validação especificado pode ser um destes valores:<br /><br /> **0** = sem validação.<br /><br /> **1** = validação somente de número de linhas.<br /><br /> **2** = RowCount e a validação da soma de verificação.<br /><br /> **3** = RowCount e validação de soma de verificação binária.|  
|**resync_gen**|**bigint**|O número de geração usado para nova sincronização da assinatura. Um valor de **-1** indica que a assinatura não está marcada para ressincronização.|  
|**login_name**|**sysname**|O nome do usuário que criou a assinatura.|  
|**hostname**|**sysname**|O valor usado pelo filtro de linha com parâmetros ao gerar a partição para a assinatura.|  
|**merge_jobid**|**binary(16)**|A ID do trabalho de mesclagem para esta assinatura.|  
|**sync_info**|**int**|Interno-somente uso.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
