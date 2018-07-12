---
title: IRowsetFastLoad (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- IRowsetFastLoad interface
ms.assetid: d19a7097-48d9-409a-aff9-277891b7aca7
caps.latest.revision: 36
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 60d4d982eb88498cf3d56f14efdffae05a71d26a
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37415085"
---
# <a name="irowsetfastload-ole-db"></a>IRowsetFastLoad (OLE DB)
  O `IRowsetFastLoad` interface expõe o suporte para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] operações de cópia em massa baseadas em memória. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Consumidores do provedor de dados OLE DB nativos usam a interface para adicionar dados rapidamente uma existente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela.  
  
 Se você definir SSPROP_ENABLEFASTLOAD como VARIANT_TRUE para uma sessão, não poderá ler dados de conjuntos de linhas subsequentemente passados como retorno dessa sessão. Quando SSPROP_ENABLEFASTLOAD é definido como VARIANT_TRUE, todos os conjuntos de linhas criados na sessão serão do tipo IRowsetFastLoad. Conjuntos de linhas iRowsetFastLoad não dão suporte a funcionalidade de busca do conjunto de linhas; Portanto, não não possível ler dados desses conjuntos de linhas.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Método|Description|  
|------------|-----------------|  
|[IRowsetFastLoad:: Commit &#40;OLE DB&#41;](irowsetfastload-commit-ole-db.md)|Marca o término de um lote de linhas inseridas e escreve as linhas na tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[IRowsetFastLoad:: Insertrow &#40;OLE DB&#41;](irowsetfastload-insertrow-ole-db.md)|Adiciona uma linha ao conjunto de linhas de cópia em massa.|  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)   
 [Copiar dados usando IRowsetFastLoad em massa &#40;OLE DB&#41;](../native-client-ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md)   
 [Enviar dados BLOB ao SQL SERVER usando IROWSETFASTLOAD e ISEQUENTIALSTREAM &#40;OLE DB&#41;](../native-client-ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md)  
  
  
