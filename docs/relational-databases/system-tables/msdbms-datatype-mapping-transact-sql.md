---
description: MSdbms_datatype_mapping (Transact-SQL)
title: MSdbms_datatype_mapping (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdbms_datatype_mapping_TSQL
- MSdbms_datatype_mapping
dev_langs:
- TSQL
helpviewer_keywords:
- MSdbms_datatype_mapping system table
ms.assetid: 13289a0b-dfb0-4771-ad80-4c5f83cded99
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: bfdf9ab815a1623aa6c323c256b9f7a4d4e27263
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88488775"
---
# <a name="msdbms_datatype_mapping-transact-sql"></a>MSdbms_datatype_mapping (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela **MSdbms_datatype_mapping** contém os mapeamentos de tipo de dados permitidos do tipo de dados no sistema de gerenciamento de banco de dados de origem (DBMS) para um ou mais tipos de dados específicos no DBMS de destino. Essa tabela é armazenada no banco de dados **msdb** e é usada para replicação de banco de dados heterogêneo.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**datatype_mapping_id**|**int**|Identifica cada mapeamento de tipo de dados exclusivo.|  
|**map_id**|**int**|Identifica o tipo de dados de origem.|  
|**dest_datatype_id**|**int**|Identifica o tipo de dados de destino.|  
|**dest_precision**|**bigint**|Define a precisão do tipo de dados de destino, em que um valor de NULL significa que a precisão não é usada, e um valor de **-1** significa que a precisão do tipo de dados de origem é usada.|  
|**dest_scale**|**int**|Define a escala do tipo de dados de destino, em que um valor nulo significa que a escala não é usada, e um valor de **-1** significa que a escala do tipo de dados de origem é usada.|  
|**dest_length**|**bigint**|Define o comprimento do tipo de dados de destino, em que um valor nulo significa que o comprimento não é usado, e um valor de **-1** significa que o comprimento do tipo de dados de origem é usado.|  
|**dest_nullable**|**bit**|Indica se a coluna de destino no mapeamento permite valores NULL, onde um valor de NULL significa que essa definição não é exigida.|  
|**dest_createparams**|**int**|O bitmap que descreve quais as combinações de comprimento, precisão e escala são aplicáveis para cada tipo de dados, incluindo:<br /><br /> **0x1** = precisão.<br /><br /> **0x2** = escala.<br /><br /> **0x4** = comprimento.|  
  
## <a name="see-also"></a>Consulte Também  
 [Replicação de banco de dados heterogênea](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Especificar mapeamentos de tipo de dados para um Publicador Oracle](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
