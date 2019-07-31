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
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: b4ced2feee2227ba1db492f721f57907069c5d99
ms.sourcegitcommit: 97e94b76f9f48d161798afcf89a8c2ac0f09c584
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68661354"
---
# <a name="spenclavesendkeys----transact-sql"></a>sp_enclave_send_keys    (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Envia todas as chaves de criptografia de coluna habilitadas para enclave no banco de dados para o enclave usado pelo [Always Encrypted com o Secure enclaves &#40;mecanismo de banco de dados&#41;](../../relational-databases/security/encryption/always-encrypted-enclaves.md).

## <a name="syntax"></a>Sintaxe  
  
```
sp_enclave_send_keys
[ ;]  
```

## <a name="arguments"></a>Argumentos

Este procedimento armazenado não tem argumentos.

## <a name="return-value"></a>Valor retornado

Este procedimento armazenado não tem nenhum valor de retorno.
  
## <a name="result-sets"></a>Conjuntos de resultados

Este procedimento armazenado não tem conjuntos de resultados.
  
## <a name="remarks"></a>Comentários

**sp_enclave_send_keys** envia chaves de criptografia de coluna habilitadas para enclave para o enclave se todas as seguintes condições forem atendidas:

- O enclave está habilitado na instância de SQL Server.
- **sp_enclave_send_keys** foi invocado de um aplicativo usando um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver de cliente, dando suporte a Always Encrypted com Secure enclaves usando uma conexão de banco de dados que tenha os cálculos de Always Encrypted e enclave habilitados.

## <a name="permissions"></a>Permissões

 Exija as permissões de definição de **chave de criptografia de qualquer coluna** e **exibição qualquer coluna de definição de chave mestra** no banco de dados.  
  
## <a name="examples"></a>Exemplos  
  
```sql
EXEC sp_enclave_send_keys;  
```

## <a name="see-also"></a>Confira também

 [Always Encrypted com o Secure &#40;enclaves mecanismo de banco de dados&#41;](../../relational-databases/security/encryption/always-encrypted-enclaves.md)   
 [Tutorial: Criando e usando índices em colunas habilitadas para enclave usando criptografia aleatória](../security/tutorial-creating-using-indexes-on-enclave-enabled-columns-using-randomized-encryption.md#step-3-create-an-index-with-role-separation)   
 [Invocar operações de indexação usando chaves de criptografia de coluna em cache](../security/encryption/configure-always-encrypted-enclaves.md#invoke-indexing-operations-using-cached-column-encryption-keys)   
 [Índices em colunas habilitadas para enclave usando criptografia aleatória](../security/encryption/always-encrypted-enclaves.md#indexes-on-enclave-enabled-columns-using-randomized-encryption)   
 [Considerações sobre o AlwaysOn e a migração de banco de dados](../security/encryption/always-encrypted-enclaves.md#anchorname-1-considerations-availability-groups-db-migration)
