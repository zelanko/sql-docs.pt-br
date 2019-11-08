---
title: Colunas de texto e imagem acopladas versus não associadas | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], image
- data types [ODBC], text
- columns [ODBC]
- ODBC data types, image columns
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: ffd3442e-d880-46e9-b848-2365a09a2406
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d23b999c40aaa6a7cd8200185f18f14ac759403f
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73778876"
---
# <a name="bound-vs-unbound-text-and-image-columns"></a>Colunas image e text associadas e não associadas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Ao usar cursores de servidor, o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client é otimizado para não transmitir os dados para colunas **Text**, **ntext**ou **Image** não associadas no momento em que **SQLFetch** é executado. Os dados **Text**, **ntext**ou **Image** não são realmente recuperados do servidor até que o aplicativo emita [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) para a coluna.  
  
 Muitos aplicativos podem ser escritos para que nenhum dado de **Text**, **ntext**ou **Image** seja exibido enquanto um usuário está simplesmente rolando para cima e para baixo em um cursor. Quando um usuário seleciona uma linha para obter mais detalhes, o aplicativo pode chamar **SQLGetData** para recuperar os dados de **Text**, **ntext**ou **Image** . Isso impedirá a transmissão dos dados **Text**, **ntext**ou **Image** para qualquer uma das linhas que o usuário não selecionar e, portanto, poderá impedir a transmissão de grandes quantidades de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciando colunas de texto e imagem](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)   
 [Comportamentos de cursor](../../relational-databases/native-client-odbc-cursors/cursor-behaviors.md)  
  
  
