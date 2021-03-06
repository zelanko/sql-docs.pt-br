---
description: sp_pdw_remove_network_credentials (Azure Synapse Analytics)
title: sp_pdw_remove_network_credentials
titleSuffix: Azure Synapse Analytics
ms.date: 03/14/2017
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.subservice: design
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: c12696a2-5939-402b-9866-8a837ca4c0a3
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest'
ms.custom: seo-dt-2019
ms.openlocfilehash: 2e69f8446bc7a98b6aa3bae68a169d5e88759ea2
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97461537"
---
# <a name="sp_pdw_remove_network_credentials-azure-synapse-analytics"></a>sp_pdw_remove_network_credentials (Azure Synapse Analytics)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Isso remove as credenciais de rede armazenadas no [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] para acessar um compartilhamento de arquivos de rede. Por exemplo, use esse procedimento armazenado para remover a permissão do para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] executar operações de backup e restauração em um servidor que reside em sua própria rede.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql  
-- Syntax for Azure Synapse Analytics and Parallel Data Warehouse  
  
sp_pdw_remove_network_credentials 'target_server_name'  
```

[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]

## <a name="arguments"></a>Argumentos  
 '*target_server_name*'  
 Especifica o nome do host do servidor de destino ou o endereço IP. As credenciais para acessar este servidor serão removidas do [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] . Isso não altera nem remove nenhuma permissão no servidor de destino real que é gerenciado por sua própria equipe.  
  
 *target_server_name* é definido como nvarchar (337).  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão **ALTER Server State** .  
  
## <a name="error-handling"></a>Tratamento de erros  
 Ocorrerá um erro se as credenciais de remoção não tiverem sucesso no nó de controle e em todos os nós de computação.  
  
## <a name="general-remarks"></a>Comentários gerais  
 Esse procedimento armazenado remove as credenciais de rede da conta NetworkService para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] . A conta NetworkService executa cada instância do SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no nó de controle e nos nós de computação. Por exemplo, quando uma operação de backup é executada, o nó de controle e cada nó de computação usarão as credenciais da conta NetworkService para acessar o servidor de destino.  
  
## <a name="metadata"></a>Metadados  
 Para listar todas as credenciais e verificar se as credenciais foram removidas, use [sys.dm_pdw_network_credentials &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md).  
  
 Para adicionar credenciais, use [sp_pdw_add_network_credentials &#40;Azure Synapse Analytics&#41;](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md).  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-remove-credentials-for-performing-a-database-backup"></a>a. Remover credenciais para executar um backup de banco de dados  
 O exemplo a seguir remove as credenciais de nome de usuário e senha para acessar o servidor de destino que tem um endereço IP de 10.192.147.63.  
  
```sql  
EXEC sp_pdw_remove_network_credentials '10.192.147.63';  
```  
  
  

