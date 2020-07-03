---
title: sys. database_filestream_options (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- database_filestream_options
- sys.database_filestream_options_TSQL
- database_filestream_options_TSQL
- sys.database_filestream_options
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_filestream_options catalog view
ms.assetid: 3383c607-0bbc-456a-ab37-7230f4cbf0e9
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2cb185c2cec6bd2a7104384b3b75e14e2de4167f
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85887935"
---
# <a name="sysdatabase_filestream_options-transact-sql"></a>sys.database_filestream_options (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Exibe informações sobre o nível de acesso não transacional a dados FILESTREAM em FileTables que estão habilitadas. Contém uma linha para cada banco de dados na instância do SQL Server.  
  
 Para obter mais informações sobre FileTables, veja [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md).  
  
  
|Coluna|Type|Descrição|  
|------------|----------|-----------------|  
|**database_id**|**int**|A ID do banco de dados. Esse valor é exclusivo na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**directory_name**|**nvarchar (255)**|O diretório no nível de banco de dados para todos os namespaces de FileTable.|  
|**non_transacted_access**|**tinyint**|O nível do acesso não transacional a dados de FILESTREAM que estão habilitados. O nível de acesso é definido pela opção NON_TRANSACTED_ACCESS da instrução **CREATE DATABASE** ou **ALTER DATABASE** .<br /><br /> Essa configuração tem um dos seguintes valores:<br /><br /> 0-não habilitado. Esse é o valor padrão. Esse nível é definido fornecendo o valor **desativado** para a opção **NON_TRANSACTED_ACCESS** .<br /><br /> 1-acesso somente leitura. Esse nível é definido fornecendo o valor **READ_ONLY** para a opção **NON_TRANSACTED_ACCESS** .<br /><br /> 3-acesso completo. Esse nível é definido fornecendo o valor **Full** para a opção **NON_TRANSACTED_ACCESS** .<br /><br /> 5 - Em transição para READONLY<br /><br /> 6-em transição para desativado|  
|**non_transacted_access_desc**|**nvarchar(60)**|A descrição do nível de acesso não transacional identificado em non_transacted_access.<br /><br /> Essa configuração tem um dos seguintes valores:<br /><br /> NENHUM-esse é o valor padrão.<br /><br /> READ_ONLY<br /><br /> FULL<br /><br /> IN_TRANSITION_TO_READ_ONLY<br /><br /> IN_TRANSITION_TO_OFF|  
  
## <a name="see-also"></a>Consulte Também  
 [Habilitar os pré-requisitos para FileTable](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)  
  
  
