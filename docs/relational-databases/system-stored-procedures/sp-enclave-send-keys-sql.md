---
title: sp_enclave_send_keys (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_enclave_send_keys
- sp_enclave_send_keys_TSQL
- sys.sp_enclave_send_keys
- sys.sp_enclave_send_keys_TSQL
helpviewer_keywords:
- sp_enclave_send_keys
author: jaszymas
ms.author: jaszymas
manager: craigg
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 6540cdd36cccba4f5a7ccb3beddf31ce00cd9107
ms.sourcegitcommit: ce5770d8b91c18ba5ad031e1a96a657bde4cae55
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2019
ms.locfileid: "67394138"
---
# <a name="spenclavesendkeys----transact-sql"></a>sp_enclave_send_keys    (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Envia coluna habilitado de enclave todas as chaves de criptografia no banco de dados para o enclave usado pelo [Always Encrypted com enclaves seguras &#40;mecanismo de banco de dados&#41;](../../relational-databases/security/encryption/always-encrypted-enclaves.md).

## <a name="syntax"></a>Sintaxe  
  
```
sp_enclave_send_keys
[ ;]  
```

## <a name="arguments"></a>Argumentos

Esse procedimento armazenado não tem argumentos.

## <a name="return-value"></a>Valor retornado

Esse procedimento armazenado não tem nenhum valor de retorno.
  
## <a name="result-sets"></a>Conjuntos de resultados

Esse procedimento armazenado não tem nenhum conjunto de resultados.
  
## <a name="remarks"></a>Comentários

**sp_enclave_send_keys** envia as chaves de criptografia de coluna habilitada para enclave para o enclave se todas as seguintes condições forem atendidas:

- O enclave está habilitado na instância do SQL Server.
- **sp_enclave_send_keys** foi chamado de um aplicativo usando um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver do cliente, com suporte para Always Encrypted com enclaves seguras usando uma conexão de banco de dados que tem Always Encrypted e o enclave computações habilitadas.

## <a name="permissions"></a>Permissões

 Exigir a **VIEW ANY COLUMN ENCRYPTION KEY DEFINITION** e **VIEW ANY COLUMN MASTER KEY DEFINITION** permissões no banco de dados.  
  
## <a name="examples"></a>Exemplos  
  
```sql
EXEC sp_enclave_send_keys;  
```

## <a name="see-also"></a>Confira também

 [Always Encrypted com enclaves seguros &#40;mecanismo de banco de dados&#41;](../../relational-databases/security/encryption/always-encrypted-enclaves.md)   
 [Tutorial: Criando e usando índices em colunas habilitada para enclave usando a criptografia aleatória](../security/tutorial-creating-using-indexes-on-enclave-enabled-columns-using-randomized-encryption.md#step-3-create-an-index-with-role-separation)   
 [Invocar operações de indexação usando chaves de criptografia de coluna armazenada em cache](../security/encryption/configure-always-encrypted-enclaves.md#invoke-indexing-operations-using-cached-column-encryption-keys)   
 [Índices em colunas habilitada para Enclave usando a criptografia aleatória](../security/encryption/always-encrypted-enclaves.md#indexes-on-enclave-enabled-columns-using-randomized-encryption)   
 [Considerações sobre a migração de banco de dados e do AlwaysOn](../security/encryption/always-encrypted-enclaves.md#considerations-for-alwayson-and-database-migration)
