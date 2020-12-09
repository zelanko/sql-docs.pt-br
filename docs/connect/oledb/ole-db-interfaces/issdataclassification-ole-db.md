---
title: ISSDataClassification | Microsoft Docs
description: Interface ISSDataClassification
ms.custom: ''
ms.date: 09/30/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- ISSDataClassification
apitype: COM
helpviewer_keywords:
- ISSDataClassification interface
author: bazizi
ms.author: v-beaziz
ms.openlocfilehash: 328110f81f993c66a9455324ff8ec830b329b41b
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96506630"
---
# <a name="issdataclassification"></a>ISSDataClassification
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW](../../../includes/applies-to-version/sql-asdb-asa.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  A interface **ISSDataClassification** oferece a funcionalidade de recuperação de dados de classificação de confidencialidade para o conjunto de linhas ativo conforme recebido do SQL Server.
  

## <a name="methods"></a>Métodos

|Método|Descrição|  
|------------|-----------------|  
|[ISSDataClassification::GetSensitivityClassification](../../oledb/ole-db-interfaces/issdataclassification-getsensitivityclassification-ole-db.md)|Retorna um ponteiro para uma estrutura SENSITIVITYCLASSIFICATION contendo informações de classificação de confidencialidade.|  

## <a name="see-also"></a>Consulte Também  
 [Interfaces do &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)   
 [Conjuntos de linhas](../ole-db-rowsets/rowsets.md)   
 [Usar a classificação de dados](../features/using-data-classification.md)
