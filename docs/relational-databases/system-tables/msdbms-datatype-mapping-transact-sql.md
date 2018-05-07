---
title: MSdbms_datatype_mapping (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSdbms_datatype_mapping_TSQL
- MSdbms_datatype_mapping
dev_langs:
- TSQL
helpviewer_keywords:
- MSdbms_datatype_mapping system table
ms.assetid: 13289a0b-dfb0-4771-ad80-4c5f83cded99
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 69bc82596929c5ba42c7f67b63c8c57b56cb3561
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="msdbmsdatatypemapping-transact-sql"></a>MSdbms_datatype_mapping (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSdbms_datatype_mapping** tabela contém os mapeamentos de tipo de dados permitida do tipo de dados no sistema de gerenciamento de banco de dados (DBMS) origem para um ou mais tipos de dados específicos no DBMS de destino. Essa tabela é armazenada no **msdb** banco de dados e é usado para replicação de banco de dados heterogênea.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**datatype_mapping_id**|**Int**|Identifica cada mapeamento de tipo de dados exclusivo.|  
|**map_id**|**Int**|Identifica o tipo de dados de origem.|  
|**dest_datatype_id**|**Int**|Identifica o tipo de dados de destino.|  
|**dest_precision**|**bigint**|Define a precisão do tipo de dados de destino, onde um valor NULL significa que a precisão não é usada, e um valor de **-1** significa que a precisão do tipo de dados de origem é usada.|  
|**dest_scale**|**Int**|Define a escala do tipo de dados de destino, onde um valor NULL significa que a escala não é usada, e um valor de **-1** significa que a escala do tipo de dados de origem é usada.|  
|**dest_length**|**bigint**|Define o comprimento do tipo de dados de destino, onde um valor NULL significa que o comprimento não é usado, e um valor de **-1** significa que o comprimento do tipo de dados de origem é usado.|  
|**dest_nullable**|**bit**|Indica se a coluna de destino no mapeamento permite valores NULL, onde um valor de NULL significa que essa definição não é exigida.|  
|**dest_createparams**|**Int**|O bitmap que descreve quais as combinações de comprimento, precisão e escala são aplicáveis para cada tipo de dados, incluindo:<br /><br /> **0x1** = precisão.<br /><br /> **0x2** = escala.<br /><br /> **0x4** = comprimento.|  
  
## <a name="see-also"></a>Consulte também  
 [Replicação de banco de dados heterogênea](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Especificar mapeamentos de tipo de dados para um publicador Oracle](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
