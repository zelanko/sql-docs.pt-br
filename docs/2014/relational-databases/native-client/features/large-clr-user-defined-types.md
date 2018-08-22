---
title: Tipos definidos pelo usuário CLR grandes | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- large CLR user-defined types
ms.assetid: b65eb61d-ccf6-49c0-98e7-9a4ef4b2f790
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dce8331ff68d9be17fc21e67a5891a4dbc4762bf
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40392683"
---
# <a name="large-clr-user-defined-types"></a>Tipos de dados CLR grandes definidos pelo usuário
  No SQL Server 2005, os UDTs (tipos definidos pelo usuário) no CLR (Common Language Runtime) eram restritos a 8.000 bytes de tamanho. Essa restrição foi eliminada no [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] e em versões posteriores. Os UDTs CLR agora são tratados de maneira semelhante aos tipos LOB (objeto grande). Ou seja, os UDTs inferiores ou iguais a 8.000 bytes têm o mesmo comportamento que no SQL Server 2005, mas são suportados UDTs maiores que informam seu tamanho como "ilimitado".  
  
 Para obter mais informações, consulte [Large CLR User-Defined tipos &#40;OLE DB&#41; ](../ole-db/large-clr-user-defined-types-ole-db.md) e [Large CLR User-Defined tipos &#40;ODBC&#41;](../odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="use-cases"></a>Casos de uso  
 Para o ODBC, o suporte a UDTs grandes inclui a capacidade de enviar valores UDT em partes como parâmetros de dados em execução. Isso é feito usando o SQLPutData.  
  
 Para o OLE DB, o suporte a UDTs grandes inclui a capacidade de transmitir valores UDT bidirecionalmente no servidor usando a associação ISequentialStream.  
  
 Os UDTs inferiores ou iguais a 8.000 bytes se comportarão como no SQL Server 2005. Para OLE DB, você ainda pode transmitir UDTs pequenos usando associação de ISequentialStream.  
  
 Às vezes, o código nativo terá de entender o conteúdo dos UDTs CLR, mas não terão de criar uma instância dos objetos gerenciados. Se esse for o caso, você poderá usar serialização personalizada para converter valores UDT no servidor em um formato bem conhecido para os clientes.  
  
 Para aplicativos com código de acesso a dados existente, você pode explorar o comportamento de UDTs CLR no cliente recuperando UDTs através de APIs nativas e criando instâncias deles com C++ CLI interop em aplicativos de modo misto.  
  
## <a name="see-also"></a>Consulte também  
 [Recursos do SQL Server Native Client](sql-server-native-client-features.md)  
  
  
