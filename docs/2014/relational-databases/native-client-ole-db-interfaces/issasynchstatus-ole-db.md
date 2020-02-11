---
title: ISSAsynchStatus (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- ISSAsynchStatus (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- ISSAsynchStatus interface
ms.assetid: c643f09f-9ccc-4d8b-9243-3cde86c2bd46
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aeb6c6c789bfe1ca2af5616fb0a1ef9785700224
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63127763"
---
# <a name="issasynchstatus-ole-db"></a>ISSAsynchStatus (OLE DB)
  **ISSAsynchStatus** expõe suporte para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] operações assíncronas. Esta é uma interface opcional herdada da interface OLE DB central **IDBAsynchStatus**. Além dos métodos **Abort** e **GetStatus** herdados de **IDBAsynchStatus**, **ISSAsynchStatus** fornece um novo método usado para aguardar até que uma operação assíncrona tenha sido concluída ou um tempo limite tenha sido atingido.  
  
|Método|DESCRIÇÃO|  
|------------|-----------------|  
|[ISSAsynchStatus:: Abort &#40;OLE DB&#41;](issasynchstatus-abort-ole-db.md)|Cancela uma operação que está sendo executada de forma assíncrona.|  
|[ISSAsynchStatus:: GetStatus &#40;OLE DB&#41;](issasynchstatus-getstatus-ole-db.md)|Retorna o status de uma operação que está sendo executada de forma assíncrona.|  
|[ISSAsynchStatus:: WaitForAsynchCompletion &#40;OLE DB&#41;](issasynchstatus-waitforasynchcompletion-ole-db.md)|Aguarda até que a operação com execução assíncrona seja concluída ou um tempo limite seja atingido.|  
  
## <a name="remarks"></a>Comentários  
 A implementação de **ISSAsynchStatus** do método **ISSAsynchStatus::GetStatus** é a mesma do método **IDBAsynchStatus::GetStatus** , com exceção de que, se a inicialização de um objeto de fonte de dados for anulada, E_UNEXPECTED será retornado, em vez de DB_E_CANCELED (apesar de que **ISSAsynchStatus::WaitForAsynchCompletion** retorna DB_E_CANCELED). Isso ocorre porque o objeto de fonte de dados não é deixado no estado normal após uma operação de anulação, para que possa haver outras tentativas de operações de inicialização.  
  
 Os métodos a seguir suportam o uso da execução assíncrona no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   **ICommand:: execute**  
  
-   **IOpenRowset:: OpenRowset**  
  
-   **IMultipleResults:: GetResult**  
  
## <a name="see-also"></a>Consulte Também  
 [Interfaces &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)   
 [Executando operações assíncronas](../native-client/features/performing-asynchronous-operations.md)  
  
  
