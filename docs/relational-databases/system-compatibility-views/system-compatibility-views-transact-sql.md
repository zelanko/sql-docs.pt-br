---
title: Exibições de compatibilidade do sistema (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- compatibility views [SQL Server]
- system tables [SQL Server], compatibility views
- type IDs [SQL Server]
- system views [SQL Server], compatibility
- metadata [SQL Server], views
- backward compatibility [SQL Server], compatibility views
- compatibility [SQL Server], compatibility views
- backward compatibility [SQL Server], system tables
- compatibility [SQL Server], system tables
- user IDs [SQL Server]
ms.assetid: 8e4624f5-9d36-4ce7-9c9e-1fe010fa2122
author: rothja
ms.author: jroth
ms.openlocfilehash: 466dc68da1c5cef56a7debe3953ba38956bb2993
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68018028"
---
# <a name="system-compatibility-views-transact-sql"></a>Exibições de compatibilidade do sistema (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Muitas das tabelas do sistema de versões anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são implementadas agora como um conjunto de exibições. Essas exibições são conhecidas como exibições de compatibilidade e destinam-se à compatibilidade com versões anteriores apenas. As exibições de compatibilidade expõem os mesmos metadados disponíveis em [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. Entretanto, as exibições de compatibilidade não expõem quaisquer metadados relacionados a recursos introduzidos em [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e posteriores. Sendo assim, quando você usa recursos novos, como [!INCLUDE[ssSB](../../includes/sssb-md.md)] ou particionamento, você deve alternar para as exibições do catálogo.  
  
 Outro motivo para atualizar às exibições do catálogo é que as colunas de exibição de compatibilidade que armazenam identificações de usuário e de tipo podem retornar NULL ou estouros aritméticos de gatilho. Isto é porque você pode criar mais de 32.767 usuários, grupos e funções, e 32.767 tipos de dados. Por exemplo, se você criar 32.768 usuários e, então, executar a seguinte consulta: `SELECT * FROM sys.sysusers`. Se ARITHABORT for definido como ON, a consulta falhará com um erro de estouro aritmético. Se ARITHABORT for definido como OFF, a coluna **UID** retornará NULL.  
  
 Para evitar esses problemas, recomendamos que você use as novas exibições do catálogo que podem controlar o número maior de identificações de usuários e de tipo. A tabela a seguir lista as colunas sujeitas a esse estouro.  
  
|Nome da coluna|Exibição de compatibilidade|Exibição SQL Server 2005|  
|-----------------|------------------------|--------------------------|  
|**xusertype**|**syscolumns**|**sys.columns**|  
|**UserType**|**syscolumns**|**sys.columns**|  
|**memberuid**|**sysmembers**|**sys.database_role_members**|  
|**groupuid**|**sysmembers**|**sys.database_role_members**|  
|**UID**|**sysobjects**|**sys.objects**|  
|**UID**|**sysprotects**|**sys.database_permissions**<br /><br /> **sys.server_permissions**|  
|**grantor**|**sysprotects**|**sys.database_permissions**<br /><br /> **sys.server_permissions**|  
|**xusertype**|**systypes**|**sys.types**|  
|**UID**|**systypes**|**sys.types**|  
|**UID**|**sysusers**|**sys.database_principals**|  
|**altuid**|**sysusers**|**sys.database_principals**|  
|**gid**|**sysusers**|**sys.database_principals**|  
|**UID**|**syscacheobjects**|**sys.dm_exec_plan_attributes**|  
|**UID**|**sysprocesses**|**sys.dm_exec_requests**|  
  
 Quando referenciado em um banco de dados de usuário, as tabelas do sistema que foram anunciadas como preteridas no SQL Server 2000 (como **syslanguages** ou **syscacheobjects**) agora estão associadas à exibição de compatibilidade traseira no esquema **Sys** . Desde que as tabelas de sistema do SQL Server 2000 foram substituídas por várias versões, essa alteração não é considerada uma alteração de quebra.  
  
 Exemplo: se um usuário criar uma tabela de usuário chamada **syslanguages** em um banco de dados de usuário, no SQL Server 2008, `SELECT * from dbo.syslanguages;` a instrução nesse banco de dados retornará os valores da tabela de usuário. A partir do SQL Server 2012, essa prática retornará dados da exibição do sistema **Sys. syslanguages**.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Mapeando tabelas do sistema para exibições do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)  
  
  
