---
title: ISSAsynchStatus (OLE DB) | Microsoft Docs
description: ISSAsynchStatus (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSAsynchStatus (OLE DB)
apitype: COM
helpviewer_keywords:
- ISSAsynchStatus interface
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 73ee8ab77cab188cf4a3d0d98c5dc1f238c8e3f0
ms.sourcegitcommit: 03ba89937daeab08aa410eb03a52f1e0d212b44f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/16/2018
ms.locfileid: "35689089"
---
# <a name="issasynchstatus-ole-db"></a>ISSAsynchStatus (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  **ISSAsynchStatus** interface expõe o suporte para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] operações assíncronas. É uma interface opcional que herda da interface OLE DB **IDBAsynchStatus**. Além dos métodos **Abort** e **GetStatus** herdados de **IDBAsynchStatus**, **ISSAsynchStatus** fornece um novo método usado para aguardar até que uma operação assíncrona tenha sido concluída ou um tempo limite tenha sido atingido.  
  
|Método|Description|  
|------------|-----------------|  
|[Issasynchstatus:: Abort &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/issasynchstatus-abort-ole-db.md)|Cancela uma operação que está sendo executada de forma assíncrona.|  
|[Issasynchstatus:: getStatus &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/issasynchstatus-getstatus-ole-db.md)|Retorna o status de uma operação que está sendo executada de forma assíncrona.|  
|[Issasynchstatus:: Waitforasynchcompletion &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/issasynchstatus-waitforasynchcompletion-ole-db.md)|Aguarda até que a operação com execução assíncrona seja concluída ou um tempo limite seja atingido.|  
  
## <a name="remarks"></a>Remarks  
 A implementação de **ISSAsynchStatus** do método **ISSAsynchStatus::GetStatus** é a mesma do método **IDBAsynchStatus::GetStatus** , com exceção de que, se a inicialização de um objeto de fonte de dados for anulada, E_UNEXPECTED será retornado, em vez de DB_E_CANCELED (apesar de que **ISSAsynchStatus::WaitForAsynchCompletion** retorna DB_E_CANCELED). É porque o objeto de fonte de dados não é deixado no estado normal após uma operação de anulação, para que outras operações de inicialização possam ser tentadas.  
  
 Os métodos a seguir suportam o uso da execução assíncrona no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:  
  
-   **ICommand:: execute**  
  
-   **IOpenRowset::OpenRowset**  
  
-   **IMultipleResults::GetResult**  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)    
 [Executando operações assíncronas](../../oledb/features/performing-asynchronous-operations.md)  
  
  
