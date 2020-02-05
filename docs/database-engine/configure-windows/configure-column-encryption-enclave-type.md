---
title: Configurar o tipo de enclave para a Opção de Configuração de Servidor Always Encrypted | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 4786c512850d161d9b7ab33f2a12cd0bd077b2bd
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "73593828"
---
# <a name="configure-the-enclave-type-for-always-encrypted-server-configuration-option"></a>Configurar o tipo de enclave para a Opção de Configuração de Servidor Always Encrypted
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

Este artigo descreve como habilitar ou desabilitar um enclave seguro para Always Encrypted com enclaves seguros. Para obter mais informações, consulte [Always Encrypted com enclaves seguros](../../relational-databases/security/encryption/always-encrypted-enclaves.md).

A Opção de Configuração do Servidor de **tipo de enclave de criptografia de coluna** controla o tipo de enclave seguro usado para Always Encrypted. A opção pode ser definida como um dos valores a seguir:  
  
|Valor|DESCRIÇÃO|  
|-------------------|-----------------| 
|0|**Nenhum enclave seguro**. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] não inicializará o enclave seguro para o Always Encrypted. Como resultado, a funcionalidade do Always Encrypted com enclaves seguros não estará disponível.|  
|1|**VBS (segurança baseada em virtualização)** . O [!INCLUDE[ssDE](../../includes/ssde-md.md)] tentará inicializar um enclave de VBS (segurança baseada em virtualização).

> [!IMPORTANT]
> Alterações ao **tipo de enclave de criptografia de coluna** não entrarão em vigor até que você reinicie a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
   
Você pode verificar o valor do tipo de enclave configurado e o valor do tipo de enclave atualmente em vigor usando a exibição [sys.configurations (Transact-SQL)](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md). 

Para confirmar que um enclave do tipo (maior que 0) que está atualmente em vigor foi inicializado corretamente após a última reinicialização de [!INCLUDE [ssnoversion-md](../../includes/ssnoversion-md.md)], confira a exibição [sys.dm_column_encryption_enclave (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-column-encryption-enclave.md):
 - Se a exibição contém exatamente uma linha, o enclave foi inicializado corretamente. 
 - Se a exibição não contém nenhuma linha, verifique o log de erros do SQL Server para ver os erros de inicialização do enclave. Confira [Exibir log de erro do SQL Server (SQL Server Management Studio)](../../relational-databases/performance/view-the-sql-server-error-log-sql-server-management-studio.md).

Para obter instruções passo a passo sobre como configurar um enclave do VBS enclave, confira [Habilitar Always Encrypted com enclaves seguros no SQL Server](../../relational-databases/security/tutorial-getting-started-with-always-encrypted-enclaves.md#step-3-enable-always-encrypted-with-secure-enclaves-in-sql-server).

## <a name="examples"></a>Exemplos  
 O exemplo a seguir habilita o enclave seguro e define o tipo enclave como VBS:

```sql  
sp_configure 'column encryption enclave type', 1;  
GO  
RECONFIGURE;  
GO  
```  

O exemplo a seguir desabilita o enclave seguro:  

```sql  
sp_configure 'column encryption enclave type', 0;  
GO  
RECONFIGURE;  
GO  
```  

A consulta a seguir recupera o tipo enclave configurado e o tipo enclave que está atualmente em vigor:

```sql  
USE [master];
GO
SELECT
[value]
, CASE [value] WHEN 0 THEN 'No enclave' WHEN 1 THEN 'VBS' ELSE 'Other' END AS [value_description]
, [value_in_use]
, CASE [value_in_use] WHEN 0 THEN 'No enclave' WHEN 1 THEN 'VBS' ELSE 'Other' END AS [value_in_use_description]
FROM sys.configurations
WHERE [name] = 'column encryption enclave type'; 
```  
## <a name="next-steps"></a>Próximas etapas
 [Gerenciar chaves para Always Encrypted com enclaves seguros](../../relational-databases/security/encryption/always-encrypted-enclaves-manage-keys.md)

## <a name="see-also"></a>Consulte Também  
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [sys.configurations (Transact-SQL)](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [sys.dm_column_encryption_enclave (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-column-encryption-enclave.md)   
