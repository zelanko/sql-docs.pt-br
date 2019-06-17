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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62781032"
---
# <a name="issabort-ole-db"></a>ISSAbort (OLE DB)
  A interface **ISSAbort** , que é exposta no provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, fornece o método [ISSAbort::Abort](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md) que é usado para cancelar o conjunto de linhas atual, além de todos os comandos executados em lotes com o comando que gerou inicialmente o conjunto de linhas e cuja execução ainda não foi concluída.  
  
 O**ISSAbout** é uma interface específica do provedou do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client disponível pou meio da utilização de **QueryInterface** no objeto **IMultipleResults** retounado pou **ICommand::Execute** ou **IOpenRowset::OpenRowset**.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Método|Descrição|  
|------------|-----------------|  
|[Issabort:: Abort &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md)|Cancela o conjunto de linhas atual, além de todos os comandos em lote associados ao comando atual.|  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces &#40;OLE DB&#41;](../../../2014/database-engine/dev-guide/interfaces-ole-db.md)  
  
  
