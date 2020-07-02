---
title: sys. fulltext_document_types (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fulltext_document_types_TSQL
- fulltext_document_types
- fulltext_document_types_TSQL
- sys.fulltext_document_types
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fulltext_document_types catalog view
ms.assetid: 156fcfa4-7304-4a5c-b96f-1c3e061e5df0
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 454b1460b0f1db0da7298e640b7b4cf081bb90b3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85790537"
---
# <a name="sysfulltext_document_types-transact-sql"></a>sys.fulltext_document_types (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna uma linha para cada tipo de documento disponível para operações de indexação de texto completo. Cada linha representa a interface IFilter registrada na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**document_type**|**sysname**|A extensão de arquivo do tipo de documento com suporte.<br /><br /> Esse valor pode ser usado para identificar o filtro que será usado durante a indexação de texto completo das colunas do tipo **varbinary (max)** ou **Image**.|  
|**class_id**|**uniqueidentifier**|GUID da classe IFilter que oferece suporte à extensão de arquivo.|  
|**path**|**nvarchar(260)**|O caminho da DLL de IFilter. O caminho está visível somente para membros da função de servidor fixa **serveradmin** .|  
|**version**|**sysname**|Versão da DLL do IFilter.|  
|**manufacturer**|**sysname**|Nome do fabricante do IFilter.<br /><br /> Observação: há suporte apenas para documentos com o fabricante [!INCLUDE[msCoName](../../includes/msconame-md.md)] no [!INCLUDE[ssSDS](../../includes/sssds-md.md)] .|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
