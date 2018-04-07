---
title: Suporte a FILESTREAM (OLE DB) | Microsoft Docs
description: Suporte a FILESTREAM (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB [FILESTREAM support]
- FILESTREAM [SQL Server], OLE DB
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: efbe3ce15444b0c6556cf3cef0267e99bb55657f
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
# <a name="filestream-support-ole-db"></a>Suporte a FILESTREAM (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Começando com [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] e OLE DB Driver para SQL Server, OLE DB dá suporte ao recurso FILESTREAM aprimorado. Para obter mais informações sobre esse recurso, consulte [suporte a FILESTREAM](../../oledb/features/filestream-support.md). Para obter exemplos, consulte [Filestream e BD OLE](../../oledb/ole-db-how-to/filestream/filestream-and-ole-db.md).  
  
 Para enviar e receber **varbinary (max)** valores maiores que 2 GB, um aplicativo usa **DBTYPE_IUNKNOWN** em associações de parâmetro e resultado. Para parâmetros de provedor deve chamar IUnknown:: QueryInterface para ISequentialStream e para resultados que retornam ISequentialStream.  
  
 Para OLE DB, a verificação relacionada aos valores de ISequentialStream será aliviada. Quando *wType* é **DBTYPE_IUNKNOWN** no **DBBINDING** struct, verificação de comprimento pode ser desabilitada omitindo **DBPART_LENGTH** de *dwPart* ou definindo o tamanho dos dados (no deslocamento *obLength* no buffer de dados) para ~ 0. Nesse caso, o provedor não verificará o comprimento do valor, e solicitará e retornará todos os dados disponíveis através do fluxo. Essa alteração será aplicada a todos os tipos LOB (objeto grande) e XML, mas somente quando conectados a servidores [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] (ou posterior). Isso oferecerá maior flexibilidade para desenvolvedores, ao mesmo tempo mantendo a consistência e compatibilidade com aplicativos e servidores de versões anteriores existentes.  
  
 Esta alteração afeta todas as interfaces que transferem dados, principalmente IRowset:: GetData ICommand:: execute e IRowsetFastLoad:: Insertrow.  
  
## <a name="see-also"></a>Consulte também  
 [Programação no Driver do OLE DB para SQL Server](../../oledb/oledb-driver-for-sql-server-programming.md)  
  
  
