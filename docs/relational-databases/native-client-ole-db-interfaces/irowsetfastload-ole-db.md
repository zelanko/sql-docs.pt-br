---
title: IRowsetFastLoad (OLE DB) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-interfaces
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apitype: COM
helpviewer_keywords: IRowsetFastLoad interface
ms.assetid: d19a7097-48d9-409a-aff9-277891b7aca7
caps.latest.revision: "35"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2c2dc8ba7de032f9f9dbdb21d51b22e7347a68fc
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="irowsetfastload-ole-db"></a>IRowsetFastLoad (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  O **IRowsetFastLoad** interface expõe o suporte para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] operações de cópia em massa com base em memória. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Os consumidores de provedor Native Client OLE DB usam a interface para adicionar dados rapidamente uma existente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela.  
  
 Se você definir SSPROP_ENABLEFASTLOAD como VARIANT_TRUE para uma sessão, não poderá ler dados de conjuntos de linhas subsequentemente passados como retorno dessa sessão. Quando SSPROP_ENABLEFASTLOAD é definido como VARIANT_TRUE, todos os conjuntos de linhas criados na sessão serão do tipo IRowsetFastLoad. Conjuntos de linhas iRowsetFastLoad não oferecem suporte a funcionalidade de busca do conjunto de linhas; Portanto, não não possível ler dados desses conjuntos de linhas.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Método|Description|  
|------------|-----------------|  
|[IRowsetFastLoad:: Commit &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-commit-ole-db.md)|Marca o término de um lote de linhas inseridas e escreve as linhas na tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[IRowsetFastLoad:: Insertrow &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-insertrow-ole-db.md)|Adiciona uma linha ao conjunto de linhas de cópia em massa.|  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces &#40; OLE DB &#41;](http://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)   
 [Em massa dados de cópia usando IRowsetFastLoad &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md)   
 [Enviar dados BLOB ao SQL SERVER usando IROWSETFASTLOAD e ISEQUENTIALSTREAM &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md)  
  
  
