---
title: Filestream Support (OLE DB) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: da09fc65de4be75798730fd0cc9785204a0c6917
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303650"
---
# <a name="filestream-support-ole-db"></a>Suporte a FILESTREAM (OLE DB)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Começando [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] com [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e Cliente Nativo 10.0, o OLE DB suporta o recurso FILESTREAM aprimorado. Para obter mais informações sobre esse recurso, consulte [FILESTREAM Support](../../../relational-databases/native-client/features/filestream-support.md). Para ver exemplos, confira [Fluxo de arquivos e OLE DB](../../../relational-databases/native-client-ole-db-how-to/filestream/filestream-and-ole-db.md).  
  
 Para enviar e receber valores **varbinary(max)** maiores que 2 GB, um aplicativo usa **DBTYPE_IUNKNOWN** nas associações de parâmetro e resultado. Para os parâmetros, o provedor precisa chamar IUnknown::QueryInterface para ISequentialStream e os resultados que retornam ISequentialStream.  
  
 Para o OLE DB, a verificação relacionada aos valores ISequentialStream será aliviada. Quando *wType* for **DBTYPE_IUNKNOWN** no struct **DBBINDING**, a verificação do comprimento poderá ser desabilitada pela omissão de **DBPART_LENGTH** de *dwPart* ou pela configuração do comprimento dos dados (no deslocamento *obLength* no buffer de dados) para aproximadamente 0. Nesse caso, o provedor não verificará o comprimento do valor, e solicitará e retornará todos os dados disponíveis através do fluxo. Essa alteração será aplicada a todos os tipos LOB (objeto grande) e XML, mas somente quando conectados a servidores [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] (ou posterior). Isso oferecerá maior flexibilidade para desenvolvedores, ao mesmo tempo mantendo a consistência e compatibilidade com aplicativos e servidores de versões anteriores existentes.  
  
 Essa alteração afeta todas as interfaces que transferem dados, principalmente IRowset::GetData, ICommand::Execute e IRowsetFastLoad::InsertRow.  
  
## <a name="see-also"></a>Consulte Também  
 [Programação do SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
