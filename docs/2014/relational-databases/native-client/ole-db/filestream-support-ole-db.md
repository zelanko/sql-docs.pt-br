---
title: Suporte a FILESTREAM (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB [FILESTREAM support]
- FILESTREAM [SQL Server], OLE DB
ms.assetid: c2bd3dfd-6103-43d1-859e-8ed8d19c58d3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ad6aa7b55906e68dba6615140ef2c6afcc3efaa5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62668929"
---
# <a name="filestream-support-ole-db"></a>Suporte a FILESTREAM (OLE DB)
  A partir [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e do cliente nativo 10,0, o OLE DB dá suporte ao recurso FileStream avançado. Para obter mais informações sobre esse recurso, consulte [suporte a FileStream](../features/filestream-support.md). Para obter exemplos, consulte [FileStream e OLE DB](../../native-client-ole-db-how-to/filestream/filestream-and-ole-db.md).  
  
 Para enviar e receber valores `varbinary(max)` maiores do que 2 GB, um aplicativo usa `DBTYPE_IUNKNOWN` em associações de parâmetro e resultado. Para parâmetros, o provedor deve chamar IUnknown:: QueryInterface para ISequentialStream e os resultados que retornam ISequentialStream.  
  
 Por OLE DB, a verificação relacionada aos valores de ISequentialStream será reduzida. Quando *wType* está `DBTYPE_IUNKNOWN` na struct `DBBINDING` , a verificação de comprimento pode ser desabilitada omitindo `DBPART_LENGTH` de *dwPart* ou definindo o comprimento dos dados (no deslocamento *obLength* no buffer de dados) para ~ 0. Nesse caso, o provedor não verificará o comprimento do valor, e solicitará e retornará todos os dados disponíveis através do fluxo. Essa alteração será aplicada a todos os tipos LOB (objeto grande) e XML, mas somente quando conectados a servidores [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] (ou posterior). Isso oferecerá maior flexibilidade para desenvolvedores, ao mesmo tempo mantendo a consistência e compatibilidade com aplicativos e servidores de versões anteriores existentes.  
  
 Essa alteração afeta todas as interfaces que transferem dados, principalmente IRowset:: GetData, ICommand:: execute e IRowsetFastLoad:: InsertRow.  
  
## <a name="see-also"></a>Consulte Também  
 [Programação do SQL Server Native Client](../sql-server-native-client-programming.md)  
  
  
