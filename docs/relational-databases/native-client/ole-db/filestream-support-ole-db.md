---
title: Suporte a FILESTREAM (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB [FILESTREAM support]
- FILESTREAM [SQL Server], OLE DB
ms.assetid: c2bd3dfd-6103-43d1-859e-8ed8d19c58d3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3ff05424d9b8726f21c8c4aa2facd42b87961cc2
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73760880"
---
# <a name="filestream-support-ole-db"></a>Suporte a FILESTREAM (OLE DB)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  A partir do [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] e do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10,0, o OLE DB oferece suporte ao recurso FILESTREAM avançado. Para obter mais informações sobre esse recurso, consulte [suporte a FileStream](../../../relational-databases/native-client/features/filestream-support.md). Para obter exemplos, consulte [FileStream e OLE DB](../../../relational-databases/native-client-ole-db-how-to/filestream/filestream-and-ole-db.md).  
  
 Para enviar e receber valores **varbinary (max)** maiores que 2 GB, um aplicativo usa **DBTYPE_IUNKNOWN** em associações de parâmetro e de resultado. Para parâmetros, o provedor deve chamar IUnknown:: QueryInterface para ISequentialStream e os resultados que retornam ISequentialStream.  
  
 Por OLE DB, a verificação relacionada aos valores de ISequentialStream será reduzida. Quando *wType* é **DBTYPE_IUNKNOWN** na struct **DBBINDING** , a verificação de comprimento pode ser desabilitada omitindo **DBPART_LENGTH** de *dwPart* ou definindo o comprimento dos dados (no deslocamento *obLength* nos dados buffer) para ~ 0. Nesse caso, o provedor não verificará o comprimento do valor, e solicitará e retornará todos os dados disponíveis através do fluxo. Essa alteração será aplicada a todos os tipos LOB (objeto grande) e XML, mas somente quando conectados a servidores [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] (ou posterior). Isso oferecerá maior flexibilidade para desenvolvedores, ao mesmo tempo mantendo a consistência e compatibilidade com aplicativos e servidores de versões anteriores existentes.  
  
 Essa alteração afeta todas as interfaces que transferem dados, principalmente IRowset:: GetData, ICommand:: execute e IRowsetFastLoad:: InsertRow.  
  
## <a name="see-also"></a>Consulte também  
 [Programação do SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
