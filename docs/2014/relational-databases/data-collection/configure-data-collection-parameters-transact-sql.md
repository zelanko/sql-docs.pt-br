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
ms.openlocfilehash: 51e0b8360c0b5aa6662fb317a62d7ce52bf4fc41
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52748898"
---
# <a name="configure-data-collection-parameters-transact-sql"></a>Configurar parâmetros de coleta de dados (Transact-SQL)
  Antes de criar um conjunto de coleta personalizado, primeiro configure os parâmetros da coleta de dados. Isso pode ser feito usando os procedimentos armazenados fornecidos com o coletor de dados. A realização dessa tarefa envolve o uso do Editor de Consultas no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para aplicar o procedimento a seguir.  
  
> [!NOTE]  
>  Você configura apenas uma vez os parâmetros de coleta de dados. Depois da configuração, esses parâmetros são usados para qualquer conjunto de coleta adicional que você criar.  
  
### <a name="configure-data-collection-parameters"></a>Configurar parâmetros de coleta de dados  
  
1.  Em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte ao banco de dados onde você quer criar um conjunto de coleta de dados.  
  
2.  No Editor de Consultas, emita as seguintes instruções:  
  
    ```tsql  
    USE msdb;  
    EXEC sp_syscollector_set_warehouse_instance_name N'INSTANCE_NAME';-- where instance name is the name of the SQL Server instance  
    EXEC sp_syscollector_set_warehouse_database_name N'MDW';  
    EXEC sp_syscollector_set_cache_directory N'D:\tempdata';  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [Coleta de dados](data-collection.md)   
 [Procedimentos armazenados de coletor de dados &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql)  
  
  
