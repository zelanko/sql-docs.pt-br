---
title: Limite vs. Não associado a colunas Text e Image | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
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
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5dbf3bd249285cb41fd49919ec76f5801e9bc0bd
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37416925"
---
# <a name="bound-vs-unbound-text-and-image-columns"></a>Limite vs. Colunas não associada Text e Image
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Ao usar cursores de servidor, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client é otimizado para não transmitir os dados para desassociada **texto**, **ntext**, ou **imagem** colunas no tempo **SQLFetch** é executada. O **texto**, **ntext**, ou **imagem** dados não são realmente recuperados do servidor até que os problemas de aplicativos [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) para o coluna.  
  
 Muitos aplicativos podem ser gravados para que nenhum **texto**, **ntext**, ou **imagem** dados seja exibidos enquanto um usuário está simplesmente rolando para cima para baixo em um cursor. Quando um usuário seleciona uma linha para obter mais detalhes, o aplicativo pode chamar **SQLGetData** para recuperar o **texto**, **ntext**, ou **imagem** dados. Esse procedimento impedirá a **texto**, **ntext**, ou **imagem** dados para qualquer uma das linhas que o usuário seleciona e pode, portanto, evitar a transmissão de muito grandes quantidades de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciando colunas Text e Image](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)   
 [Comportamentos de cursor](../../relational-databases/native-client-odbc-cursors/cursor-behaviors.md)  
  
  
