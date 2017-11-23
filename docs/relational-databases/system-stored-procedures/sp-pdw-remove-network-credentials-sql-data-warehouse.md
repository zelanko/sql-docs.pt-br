---
title: sp_pdw_remove_network_credentials (SQL Data Warehouse) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: system-stored-procedures
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: c12696a2-5939-402b-9866-8a837ca4c0a3
caps.latest.revision: "9"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 30f35803c804b6e895bf5287cb864c9cc979f013
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sppdwremovenetworkcredentials-sql-data-warehouse"></a>sp_pdw_remove_network_credentials (SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Isso remove as credenciais de rede armazenadas no [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] para acessar um compartilhamento de arquivos de rede. Por exemplo, use este procedimento armazenado para remover a permissão de [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] para realizar backup e restaurar operações em um servidor que reside dentro de sua própria rede.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "ícone de link do tópico") [convenções de sintaxe do Transact-SQL &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_remove_network_credentials 'target_server_name'  
```  
  
## <a name="arguments"></a>Argumentos  
 '*target_server_name*'  
 Especifica o nome de host do servidor de destino ou endereço IP. As credenciais para acessar este servidor serão removidas do [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. Isso não alterar ou remover todas as permissões no servidor de destino real que é gerenciado pela sua equipe.  
  
 *target_server_name* é definido como nvarchar(337).  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="permissions"></a>Permissões  
 Requer **ALTER SERVER STATE** permissão.  
  
## <a name="error-handling"></a>Tratamento de erros  
 Ocorrerá um erro se não for bem-sucedida remover credenciais no nó de controle e todos os nós de computação.  
  
## <a name="general-remarks"></a>Comentários gerais  
 Esse procedimento armazenado remove as credenciais de rede da conta NetworkService para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. A conta NetworkService executa cada instância de SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no nó de controle e os nós de computação. Por exemplo, quando uma operação de backup é executado, o nó de controle e cada nó de computação usará as credenciais da conta NetworkService para acessar o servidor de destino.  
  
## <a name="metadata"></a>Metadados  
 Para listar todas as credenciais e verifique se as credenciais foram removidas, use [sys.dm_pdw_network_credentials &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md).  
  
 Para adicionar as credenciais, use [sp_pdw_add_network_credentials &#40; SQL Data Warehouse &#41; ](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md).  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-remove-credentials-for-performing-a-database-backup"></a>A. Remover as credenciais para executar um backup de banco de dados  
 O exemplo a seguir remove as credenciais de nome e uma senha para acessar o servidor de destino que tem um endereço IP de 10.192.147.63.  
  
```  
EXEC sp_pdw_remove_network_credentials '10.192.147.63';  
```  
  
  

