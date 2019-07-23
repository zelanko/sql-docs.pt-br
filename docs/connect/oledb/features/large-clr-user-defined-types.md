---
title: Tipos de CLR grandes definidos pelo usuário | Microsoft Docs
description: Tipos de CLR grandes definidos pelo usuário no driver de OLE DB para SQL Server
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- large CLR user-defined types
author: pmasl
ms.author: pelopes
ms.openlocfilehash: acbdd170808ed9f6d7f67265a4e0d18f3b9e8eb0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989071"
---
# <a name="large-clr-user-defined-types"></a>Tipos de dados CLR grandes definidos pelo usuário
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  No SQL Server 2005, os UDTs (tipos definidos pelo usuário) no CLR (Common Language Runtime) eram restritos a 8.000 bytes de tamanho. Essa restrição foi eliminada no [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] e em versões posteriores. Os UDTs CLR agora são tratados de maneira semelhante aos tipos LOB (objeto grande). Ou seja, os UDTs inferiores ou iguais a 8.000 bytes têm o mesmo comportamento que no SQL Server 2005, mas são suportados UDTs maiores que informam seu tamanho como "ilimitado".  
  
 Para obter mais informações, consulte [tipos &#40;CLR grandes definidos pelo usuário&#41;OLE DB](../../oledb/ole-db/large-clr-user-defined-types-ole-db.md).  
  
## <a name="use-cases"></a>Casos de uso   
  
 Para o OLE DB, o suporte a UDTs grandes inclui a capacidade de transmitir valores UDT bidirecionalmente no servidor usando a associação ISequentialStream.  
  
 Os UDTs inferiores ou iguais a 8.000 bytes se comportarão como no SQL Server 2005. Por OLE DB, você ainda pode transmitir pequenos UDTs usando a associação ISequentialStream.  
  
 Às vezes, o código nativo terá de entender o conteúdo dos UDTs CLR, mas não terão de criar uma instância dos objetos gerenciados. Se esse for o caso, você poderá usar serialização personalizada para converter valores UDT no servidor em um formato bem conhecido para os clientes.  
  
 Para aplicativos com código de acesso a dados existente, você pode explorar o comportamento de UDTs CLR no cliente recuperando UDTs através de APIs nativas e criando instâncias deles com C++ CLI interop em aplicativos de modo misto.  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos do Driver do OLE DB para SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)    
  
  
