---
title: Tipos definidos pelo usuário CLR grandes | Microsoft Docs
description: Saiba mais sobre as restrições de tamanho e o comportamento relacionado para tipos definidos pelo usuário no Common Language Runtime em diferentes versões do SQL Server.
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- large CLR user-defined types
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9fdc52df9307bbe4ce3e826ca682d787e1c11506
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88861468"
---
# <a name="large-clr-user-defined-types"></a>Tipos de dados CLR grandes definidos pelo usuário
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  No SQL Server 2005, os UDTs (tipos definidos pelo usuário) no CLR (Common Language Runtime) eram restritos a 8.000 bytes de tamanho. Essa restrição foi eliminada no [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] e em versões posteriores. Os UDTs CLR agora são tratados de maneira semelhante aos tipos LOB (objeto grande). Ou seja, os UDTs inferiores ou iguais a 8.000 bytes têm o mesmo comportamento que no SQL Server 2005, mas são suportados UDTs maiores que informam seu tamanho como "ilimitado".  
  
 Para obter mais informações, veja [Tipos CLR grandes definidos pelo usuário &#40;OLE DB&#41;](../../oledb/ole-db/large-clr-user-defined-types-ole-db.md).  
  
## <a name="use-cases"></a>Casos de uso   
  
 Para o OLE DB, o suporte a UDTs grandes inclui a capacidade de transmitir valores UDT bidirecionalmente no servidor usando a associação ISequentialStream.  
  
 Os UDTs inferiores ou iguais a 8.000 bytes se comportarão como no SQL Server 2005. Para o OLE DB, você ainda pode transmitir UDTs pequenos usando a associação ISequentialStream.  
  
 Às vezes, o código nativo terá de entender o conteúdo dos UDTs CLR, mas não terão de criar uma instância dos objetos gerenciados. Se esse for o caso, você poderá usar serialização personalizada para converter valores UDT no servidor em um formato bem conhecido para os clientes.  
  
 Para aplicativos com código de acesso a dados existente, você pode explorar o comportamento de UDTs CLR no cliente recuperando UDTs através de APIs nativas e criando instâncias deles com C++ CLI interop em aplicativos de modo misto.  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos do Driver do OLE DB para SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)    
  
  
