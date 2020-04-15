---
title: Bound vs. Colunas de texto e imagem desvinculadas | Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0cfa05f7019342d63ab6f3092c3b6df5ae6e8daa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297726"
---
# <a name="bound-vs-unbound-text-and-image-columns"></a>Colunas de texto e imagem associadas vs. não associadas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Ao usar cursores [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de servidor, o driver ODBC do Cliente Nativo é otimizado para não transmitir os dados para colunas de **texto**não vinculadas, **ntext**ou **imagens** no momento em que o **SQLFetch** é executado. Os dados **de texto,** **ntext**ou **imagem** não são realmente recuperados do servidor até que o aplicativo emita [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) para a coluna.  
  
 Muitos aplicativos podem ser gravados para que nenhum **texto,** **ntext**ou dados **de imagem** sejam exibidos enquanto um usuário está simplesmente rolando para cima e para baixo em um cursor. Quando um usuário seleciona uma linha para obter mais detalhes, o aplicativo pode então chamar **SQLGetData** para recuperar o **texto,** **ntext**ou dados **de imagem.** Isso impedirá a transmissão de dados de **texto,** **ntext**ou **imagem** para qualquer uma das linhas que o usuário não selecionar, podendo, portanto, impedir a transmissão de quantidades muito grandes de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciamento de colunas de texto e imagem](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)   
 [Comportamentos de cursor](../../relational-databases/native-client-odbc-cursors/cursor-behaviors.md)  
  
  
