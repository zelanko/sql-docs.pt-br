---
title: database_scoped_credentials (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.database_scoped_credentials
- sys.database_scoped_credentials_TSQL
- database_scoped_credentials
- database_scoped_credentials_TSQL
helpviewer_keywords:
- sys.database_scoped_credentials catalog view
ms.assetid: 68e8aa6b-bcdc-42aa-93d8-d498f724c188
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4d3718357b68aa47bbc32e4d975a546f3e86cb73
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47814834"
---
# <a name="sysdatabasescopedcredentials-transact-sql"></a>database_scoped_credentials (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Retorna uma linha para cada banco de dados com escopo de credencial no banco de dados.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|credential_id|**int**|ID da credencial no escopo do banco de dados. É exclusivo no banco de dados.|  
|nome|**sysname**|Credencial no escopo do nome do banco de dados. É exclusivo no banco de dados.|  
|credential_identity|**nvarchar(4000)**|Nome da identidade a ser usada. Geralmente é um usuário do Windows. Não precisa ser exclusivo.|  
|create_date|**datetime**|Hora em que a credencial no escopo do banco de dados foi criada.|  
|modify_date|**datetime**|Hora em que a credencial no escopo do banco de dados foi modificada pela última vez.|  
|target_type|**nvarchar(100)**|Credencial no escopo do tipo de banco de dados. Retorna `NULL` credenciais no escopo do banco de dados.|  
|target_id|**int**|ID do objeto mapeado para a credencial no escopo do banco de dados. Retorna 0 para o banco de dados de credenciais no escopo|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão `CONTROL` no banco de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Credenciais &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [ALTER DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)   
 [DROP DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
