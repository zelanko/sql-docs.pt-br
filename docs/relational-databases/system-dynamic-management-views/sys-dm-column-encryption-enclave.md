---
description: sys.dm_column_encryption_enclave (Transact-SQL)
title: sys.dm_column_encryption_enclave (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/11/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: system-objects
ms.topic: language-reference
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15'
ms.openlocfilehash: 6d15c17b4e023909210cef55884064757ae5ddc2
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97482777"
---
# <a name="sysdm_column_encryption_enclave-transact-sql"></a>sys.dm_column_encryption_enclave (Transact-SQL)
[!INCLUDE [sqlserver2019-windows-only](../../includes/applies-to-version/sqlserver2019-windows-only.md)]

Retorna contadores de desempenho para o enclave seguro para Always Encrypted. Para obter mais informações, consulte [Always Encrypted com enclaves seguros](../security/encryption/always-encrypted-enclaves.md).

Se o enclave estiver configurado e tiver sido inicializado corretamente após a última reinicialização do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a exibição conterá exatamente uma linha. Se o enclave não estiver configurado ou não tiver sido inicializado corretamente, a exibição não retornará nenhuma linha. 

|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|current_enclave_session_count|**int**|O número atual de sessões de cliente usando o enclave.|  
|current_column_encryption_key_count|**int**|A contagem de chaves de criptografia de coluna que o enclave contém atualmente.|  
|current_memory_size_kb|**bigint**|Tamanho da memória enclave em KB|  
|total_evicted_session_count|**bigint**|A contagem total de sessões enclave removidas desde a última reinicialização do servidor.|   
  
## <a name="permissions"></a>Permissões  
Requer a permissão `VIEW SERVER STATE`.   
  
## <a name="examples"></a>Exemplos  
 
```sql  
SELECT * FROM sys.dm_column_encryption_enclave;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar o tipo de enclave para a Opção de Configuração de Servidor Always Encrypted](../../database-engine/configure-windows/configure-column-encryption-enclave-type.md)
  
  
