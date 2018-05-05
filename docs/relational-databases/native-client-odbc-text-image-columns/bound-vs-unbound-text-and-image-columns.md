---
title: Vs associados. Não associado a colunas de texto e imagem | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-text-image-columns
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
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
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 0811587077e54486e7e0b1200cc06e1e4a80bbf5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="bound-vs-unbound-text-and-image-columns"></a>Vs associados. Desassociado colunas de texto e imagem
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Ao usar cursores de servidor, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client é otimizado para não transmitir os dados para desassociada **texto**, **ntext**, ou **imagem** colunas no momento **SQLFetch** é executada. O **texto**, **ntext**, ou **imagem** dados não são realmente recuperados do servidor até que o aplicativo não emite [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) para a coluna.  
  
 Muitos aplicativos podem ser gravados para que nenhum **texto**, **ntext**, ou **imagem** dados são exibidos enquanto um usuário está simplesmente rolando para cima e para baixo em um cursor. Quando um usuário seleciona uma linha para obter mais detalhes, o aplicativo pode chamar **SQLGetData** para recuperar o **texto**, **ntext**, ou **imagem** dados. Isso impedirá a transmissão de **texto**, **ntext**, ou **imagem** dados para qualquer uma das linhas que o usuário seleciona e, portanto, pode impedir a transmissão de quantidades muito grandes de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar colunas de texto e imagem](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)   
 [Comportamentos de cursor](../../relational-databases/native-client-odbc-cursors/cursor-behaviors.md)  
  
  
