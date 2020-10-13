---
description: sp_pdw_add_network_credentials (SQL Data Warehouse)
title: sp_pdw_add_network_credentials
titleSuffix: Azure Synapse Analytics
ms.date: 03/14/2017
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 0729eeff-ac7e-43f0-80fa-ff5346a75985
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.custom: seo-dt-2019
ms.openlocfilehash: a91960dc4dad3909e18003309bcd7f12f1461b67
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/13/2020
ms.locfileid: "92004540"
---
# <a name="sp_pdw_add_network_credentials-sql-data-warehouse"></a>sp_pdw_add_network_credentials (SQL Data Warehouse)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Isso armazena as credenciais de rede no [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e os associa a um servidor. Por exemplo, use esse procedimento armazenado para conceder [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] permissões de leitura/gravação apropriadas para executar operações de backup e restauração de banco de dados em um servidor de destino ou para criar um backup de um certificado usado para TDE.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql  
-- Syntax for Azure Synapse Analytics and Parallel Data Warehouse  
  
sp_pdw_add_network_credentials 'target_server_name',  'user_name', 'password'  
```  

[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]

## <a name="arguments"></a>Argumentos  
 '*target_server_name*'  
 Especifica o nome do host do servidor de destino ou o endereço IP. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] acessará esse servidor usando as credenciais de nome de usuário e senha passadas para este procedimento armazenado.  
  
 Para se conectar por meio da rede InfiniBand, use o endereço IP de InfiniBand do servidor de destino.  
  
 *target_server_name* é definido como nvarchar (337).  
  
 '*user_name*'  
 Especifica o user_name que tem permissões para acessar o servidor de destino. Se já existirem credenciais para o servidor de destino, elas serão atualizadas para as novas credenciais.  
  
 *user_name* é definido como nvarchar (513).  
  
 '*senha*"  
 Especifica a senha para *user_name*.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão **ALTER Server State** .  
  
## <a name="error-handling"></a>Tratamento de erros  
 Ocorrerá um erro se a adição de credenciais não tiver sucesso no nó de controle e em todos os nós de computação.  
  
## <a name="general-remarks"></a>Comentários gerais  
 Esse procedimento armazenado adiciona as credenciais de rede à conta NetworkService para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] . A conta NetworkService executa cada instância do SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no nó de controle e nos nós de computação. Por exemplo, quando uma operação de backup é executada, o nó de controle e cada nó de computação usarão as credenciais da conta NetworkService para obter permissão de leitura e gravação para o servidor de destino.  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-add-credentials-for-performing-a-database-backup"></a>a. Adicionar credenciais para executar um backup de banco de dados  
 O exemplo a seguir associa as credenciais de nome de usuário e senha para o usuário de domínio seattle\david com um servidor de destino que tem um endereço IP de 10.172.63.255. O usuário seattle\david tem permissões de leitura/gravação para o servidor de destino. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] o armazenará essas credenciais e as usará para ler e gravar no servidor de destino, conforme necessário para operações de backup e restauração.  
  
```sql  
EXEC sp_pdw_add_network_credentials '10.172.63.255', 'seattle\david', '********';  
```  
  
 O comando backup requer que o nome do servidor seja inserido como um endereço IP.  
  
> [!NOTE]  
>  Para executar o backup de banco de dados em InfiniBand, certifique-se de usar o endereço IP de InfiniBand do servidor de backup.  
  
## <a name="see-also"></a>Consulte Também  
 [sp_pdw_remove_network_credentials &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)  
  
  

