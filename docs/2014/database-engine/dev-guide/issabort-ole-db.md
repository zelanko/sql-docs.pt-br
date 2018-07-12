---
title: ISSAbort (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- ISSAbort interface
ms.assetid: 7c4df482-4a83-4da0-802b-3637b507693a
caps.latest.revision: 11
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6ace6518c1a0f4ece66ec0b9b24cb9e109db7ffa
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37180343"
---
# <a name="issabort-ole-db"></a>ISSAbort (OLE DB)
  O **ISSAbort** interface, que é exposta na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client, fornece o [issabort:: Abort](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md) método que é usado para cancelar o conjunto de linhas atual, além de todos os comandos em lote com o comando que gerou inicialmente o conjunto de linhas, e que ainda não concluiu a execução.  
  
 **ISSAbort** é um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interface específica do provedor de Native Client disponível por meio **QueryInterface** sobre o **IMultipleResults** objeto retornado por  **ICommand:: execute** ou **IOpenRowset:: OPENROWSET**.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Método|Description|  
|------------|-----------------|  
|[Issabort:: Abort &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md)|Cancela o conjunto de linhas atual, além de todos os comandos em lote associados ao comando atual.|  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces &#40;OLE DB&#41;](../../../2014/database-engine/dev-guide/interfaces-ole-db.md)  
  
  
