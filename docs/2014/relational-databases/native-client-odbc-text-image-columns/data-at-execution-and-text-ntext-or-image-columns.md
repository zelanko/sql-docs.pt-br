---
title: Dados em execução e Text, ntext ou colunas de imagem | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
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
- data-at-execution
- ODBC data-at-execution
- image columns [ODBC]
ms.assetid: 67ffb1a6-f38d-4712-ba64-96bdd41ec2b2
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 90777c1f7f1ac50266eaf7fe473c5ca3b1c2f189
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117874"
---
# <a name="data-at-execution-and-text-ntext-or-image-columns"></a>Dados em execução e colunas Text, ntext ou Image
  Os dados em execução ODBC são um recurso que permite aos aplicativos trabalhar com quantidades extremamente grandes de dados em parâmetros ou colunas associadas. Ao recuperar grandes **texto**, **ntext**, ou **imagem** colunas, um aplicativo não consiga simplesmente alocar um buffer enorme, associar a coluna no buffer e buscar a linha. Ao atualizar muito grandes **texto**, **ntext**, ou **imagem** colunas, o aplicativo não consiga simplesmente alocar um buffer enorme, associá-lo a um marcador de parâmetro em um SQL instrução e, em seguida, execute a instrução. Nesses casos, o aplicativo deve usar [SQLGetData](../native-client-odbc-api/sqlgetdata.md) ou [SQLPutData](../native-client-odbc-api/sqlputdata.md) com suas opções de dados em execução.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciando colunas Text e Image](managing-text-and-image-columns.md)  
  
  