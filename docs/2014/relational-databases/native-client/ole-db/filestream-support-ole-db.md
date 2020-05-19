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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f50f002514977f60fb07358293ecbdd524884e58
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704247"
---
# <a name="filestream-support-ole-db"></a>Suporte a FILESTREAM (OLE DB)
  A partir [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] do e do cliente nativo 10,0, o OLE DB dá suporte ao recurso FileStream avançado. Para obter mais informações sobre esse recurso, consulte [suporte a FileStream](../features/filestream-support.md). Para ver exemplos, confira [Fluxo de arquivos e OLE DB](../../native-client-ole-db-how-to/filestream/filestream-and-ole-db.md).  
  
 Para enviar e receber valores `varbinary(max)` maiores do que 2 GB, um aplicativo usa `DBTYPE_IUNKNOWN` em associações de parâmetro e resultado. Para os parâmetros, o provedor precisa chamar IUnknown::QueryInterface para ISequentialStream e os resultados que retornam ISequentialStream.  
  
 Para o OLE DB, a verificação relacionada aos valores ISequentialStream será aliviada. Quando *wType* está `DBTYPE_IUNKNOWN` na `DBBINDING` struct, a verificação de comprimento pode ser desabilitada omitindo `DBPART_LENGTH` de *dwPart* ou definindo o comprimento dos dados (no deslocamento *obLength* no buffer de dados) para ~ 0. Nesse caso, o provedor não verificará o comprimento do valor, e solicitará e retornará todos os dados disponíveis através do fluxo. Essa alteração será aplicada a todos os tipos LOB (objeto grande) e XML, mas somente quando conectados a servidores [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] (ou posterior). Isso oferecerá maior flexibilidade para desenvolvedores, ao mesmo tempo mantendo a consistência e compatibilidade com aplicativos e servidores de versões anteriores existentes.  
  
 Essa alteração afeta todas as interfaces que transferem dados, principalmente IRowset::GetData, ICommand::Execute e IRowsetFastLoad::InsertRow.  
  
## <a name="see-also"></a>Consulte Também  
 [Programação do SQL Server Native Client](../sql-server-native-client-programming.md)  
  
  
