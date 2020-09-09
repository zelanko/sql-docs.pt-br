---
description: sys.dm_io_cluster_valid_path_names (Transact-SQL)
title: sys. dm_io_cluster_valid_path_names (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_io_cluster_valid_path_names
- dm_io_cluster_valid_path_names_TSQL
- sys.dm_io_cluster_valid_path_names_TSQL
- dm_io_cluster_valid_path_names
dev_langs:
- TSQL
helpviewer_keywords:
- dm_io_cluster_valid_path_names
- sys.dm_io_cluster_valid_path_names
- cluster valid path names
- csv name
- cluster shared volume names
ms.assetid: 5bc8a0e5-6c72-425b-8c58-f276eb9add2c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 18a1e01e893486a7ce32f1c3510fb52d5fd7ec0e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89531989"
---
# <a name="sysdm_io_cluster_valid_path_names-transact-sql"></a>sys.dm_io_cluster_valid_path_names (Transact-SQL)
[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]

  Retorna informações sobre todos os discos compartilhados válidos, inclusive volumes compartilhados agrupados, para uma instância de cluster de failover do SQL Server. Se a instância não for clusterizada, um conjunto de linhas vazio será retornado.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**path_name**|**Nvarchar (512)**|Ponto de montagem do volume ou caminho da unidade que pode ser usado como um diretório raiz para o banco de dados e os arquivos de log. Não permite valor nulo.|  
|**cluster_owner_node**|**Nvarchar (64)**|Proprietário atual da unidade. Para os volumes compartilhados de cluster (CSV), o proprietário é o nó que está hospedando o servidor de metadados. Não permite valor nulo.|  
|**is_cluster_shared_volume**|**Parte**|Retornará 1 se a unidade em que esse caminho está localizado estiver em um volume compartilhado de cluster; caso contrário, retornará 0.|  
  
## <a name="remarks"></a>Comentários  
 Uma instância de cluster de failover (FCI) do SQL Server deve usar armazenamento compartilhado entre todos os nós da FCI para o armazenamento de dados e de arquivo de log. Os discos listados nesta exibição são aqueles que estão no grupo de recursos de cluster associados com a instância e são os únicos discos que podem ser usados para o armazenamento de dados ou de arquivo de log.  
  
> [!NOTE]  
>  Essa exibição substituirá [Sys. dm_io_cluster_shared_drives &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-shared-drives-transact-sql.md) em uma versão futura.  
  
## <a name="permissions"></a>Permissões  
 O usuário deve ter a permissão VIEW SERVER STATE para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa sys.dm_io_cluster_valid_path_names para determinar as unidades compartilhadas em uma instância de servidor clusterizado:  
  
```  
SELECT * FROM sys.dm_io_cluster_valid_path_names;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [sys. dm_os_cluster_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md)   
 [sys. dm_io_cluster_shared_drives &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-shared-drives-transact-sql.md)   
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

