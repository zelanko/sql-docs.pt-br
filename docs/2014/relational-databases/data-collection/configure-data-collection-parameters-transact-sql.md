---
title: Configurar parâmetros de coleta de dados (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- data collection [SQL Server]
ms.assetid: 850905b6-35d2-4ed1-ab51-de64daa832b2
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b9cdabe3a74570c44eba952137d6b9efb856a731
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62918558"
---
# <a name="configure-data-collection-parameters-transact-sql"></a>Configurar parâmetros de coleta de dados (Transact-SQL)
  Antes de criar um conjunto de coleta personalizado, primeiro configure os parâmetros da coleta de dados. Isso pode ser feito usando os procedimentos armazenados fornecidos com o coletor de dados. A realização dessa tarefa envolve o uso do Editor de Consultas no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para aplicar o procedimento a seguir.  
  
> [!NOTE]  
>  Você configura apenas uma vez os parâmetros de coleta de dados. Depois da configuração, esses parâmetros são usados para qualquer conjunto de coleta adicional que você criar.  
  
### <a name="configure-data-collection-parameters"></a>Configurar parâmetros de coleta de dados  
  
1.  Em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte ao banco de dados onde você quer criar um conjunto de coleta de dados.  
  
2.  No Editor de Consultas, emita as seguintes instruções:  
  
    ```sql  
    USE msdb;  
    EXEC sp_syscollector_set_warehouse_instance_name N'INSTANCE_NAME';-- where instance name is the name of the SQL Server instance  
    EXEC sp_syscollector_set_warehouse_database_name N'MDW';  
    EXEC sp_syscollector_set_cache_directory N'D:\tempdata';  
    ```  
  
## <a name="see-also"></a>Consulte Também  
 [Coleta de Dados](data-collection.md)   
 [Procedimentos armazenados de coletor de dados &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql)  
  
  
