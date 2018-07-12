---
title: Suporte a FILESTREAM (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: native-client-ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB [FILESTREAM support]
- FILESTREAM [SQL Server], OLE DB
ms.assetid: c2bd3dfd-6103-43d1-859e-8ed8d19c58d3
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ad287aad1d87310a93bb2917d889775bba1e0650
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37420005"
---
# <a name="filestream-support-ole-db"></a>Suporte a FILESTREAM (OLE DB)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Começando com [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] e [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, o OLE DB dá suporte ao recurso FILESTREAM aprimorado. Para obter mais informações sobre esse recurso, consulte [suporte a FILESTREAM](../../../relational-databases/native-client/features/filestream-support.md). Para obter exemplos, consulte [Filestream e OLE DB](../../../relational-databases/native-client-ole-db-how-to/filestream/filestream-and-ole-db.md).  
  
 Para enviar e receber **varbinary (max)** valores maiores que 2 GB, um aplicativo usa **DBTYPE_IUNKNOWN** nas associações de parâmetro e resultado. Para parâmetros de provedor deve chamar IUnknown:: QueryInterface para ISequentialStream e para resultados que retornam ISequentialStream.  
  
 Para OLE DB, a verificação relacionada aos valores de ISequentialStream será aliviada. Quando *wType* é **DBTYPE_IUNKNOWN** no **DBBINDING** struct, verificação de comprimento pode ser desabilitada omitindo **DBPART_LENGTH** partir *dwPart* ou definindo o comprimento dos dados (no deslocamento *obLength* no buffer de dados) para ~ 0. Nesse caso, o provedor não verificará o comprimento do valor, e solicitará e retornará todos os dados disponíveis através do fluxo. Essa alteração será aplicada a todos os tipos LOB (objeto grande) e XML, mas somente quando conectados a servidores [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] (ou posterior). Isso oferecerá maior flexibilidade para desenvolvedores, ao mesmo tempo mantendo a consistência e compatibilidade com aplicativos e servidores de versões anteriores existentes.  
  
 Essa alteração afeta todas as interfaces que transferem dados, principalmente IRowset:: GetData ICommand:: execute e IRowsetFastLoad:: Insertrow.  
  
## <a name="see-also"></a>Consulte também  
 [Programação do SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
