---
title: sys. dm_server_registry (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_server_registry_TSQL
- sys.dm_server_registry
- dm_server_registry
- sys.dm_server_registry_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_server_registry dynamic management view
ms.assetid: 9b3e0c74-2e99-4996-a383-104d51831e97
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8daa2d195ab1f4cf4602b9633394ed1705a3d7d2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "80530821"
---
# <a name="sysdm_server_registry-transact-sql"></a>sys.dm_server_registry (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações de configuração e instalação que estão armazenadas no registro do Windows para a instância atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Retorna uma linha por chave de registro. Use essa exibição de gerenciamento dinâmico para retornar informações como os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que estão disponíveis nos computadores host ou valores de configuração de rede para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|registry_key|**nvarchar(256)**|Nome da chave do Registro. Permite valor nulo.|  
|value_name|**nvarchar(256)**|Nome do valor da chave. Esse é o item mostrado na coluna **Name** do editor do registro. Permite valor nulo.|  
|value_data|**sql_variant**|Valor dos dados da chave. Esse é o valor mostrado na coluna de **dados** do editor do registro para uma determinada entrada. Permite valor nulo.|  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-display-the-sql-server-services"></a>a. Exibir os serviços do SQL Server  
 O exemplo a seguir retorna valores da chave do registro para os serviços do SQL Server e SQL Server Agent para a instância atual do SQL Server.  
  
```  
SELECT registry_key, value_name, value_data  
FROM sys.dm_server_registry  
WHERE registry_key LIKE N'%ControlSet%';  
```  
  
### <a name="b-display-the-sql-server-agent-registry-key-values"></a>B. Exibir os valores da chave do registro do SQL Server Agent  
 O exemplo a seguir retorna valores da chave do registro do SQL Server Agent para a instância atual do SQL Server.  
  
```  
SELECT registry_key, value_name, value_data  
FROM sys.dm_server_registry  
WHERE registry_key LIKE N'%SQLAgent%';  
```  
  
### <a name="c-display-the-current-version-of-the-instance-of-sql-server"></a>C. Exibir a versão atual da instância do SQL Server  
 O exemplo a seguir retorna a versão da instância atual do SQL Server.  
  
```  
SELECT registry_key, value_name, value_data  
FROM sys.dm_server_registry  
WHERE value_name = N'CurrentVersion';  
```  
  
### <a name="d-display-the-parameters-passed-to-the-instance-of-sql-server-during-startup"></a>D. Exibir os parâmetros passados para a instância do SQL Server durante a inicialização  
 O exemplo a seguir retorna os parâmetros que são passados para a instância do SQL Server durante a inicialização.  
  
```  
SELECT registry_key, value_name, value_data  
FROM sys.dm_server_registry  
WHERE registry_key LIKE N'%Parameters';  
```  
  
### <a name="e-return-network-configuration-information-for-the-instance-of-sql-server"></a>E. Retornar as informações de configuração de rede para a instância do SQL Server  
 O exemplo a seguir retorna valores de configuração de rede para a instância atual do SQL Server.  
  
```  
SELECT registry_key, value_name, value_data  
FROM sys.dm_server_registry  
WHERE registry_key LIKE N'%SuperSocketNetLib%';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [sys. dm_server_services &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-services-transact-sql.md)  
  
  
