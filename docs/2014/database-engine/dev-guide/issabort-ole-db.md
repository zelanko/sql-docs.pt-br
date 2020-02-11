---
title: ISSAbort (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- ISSAbort interface
ms.assetid: 7c4df482-4a83-4da0-802b-3637b507693a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 801eb84df08837ec8e49b6bb0e28fc1f1115e674
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62781032"
---
# <a name="issabort-ole-db"></a>ISSAbort (OLE DB)
  A interface **ISSAbort** , que é exposta no provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, fornece o método [ISSAbort::Abort](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md) que é usado para cancelar o conjunto de linhas atual, além de todos os comandos executados em lotes com o comando que gerou inicialmente o conjunto de linhas e cuja execução ainda não foi concluída.  
  
 **ISSAbort** é uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interface específica do provedor de cliente nativo disponível usando **QueryInterface** no objeto **IMultipleResults** retornado por **ICommand:: execute** ou **IOpenRowset:: OPENROWSET**.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Método|DESCRIÇÃO|  
|------------|-----------------|  
|[ISSAbort:: Abort &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md)|Cancela o conjunto de linhas atual, além de todos os comandos em lote associados ao comando atual.|  
  
## <a name="see-also"></a>Consulte Também  
 [Interfaces &#40;OLE DB&#41;](../../../2014/database-engine/dev-guide/interfaces-ole-db.md)  
  
  
