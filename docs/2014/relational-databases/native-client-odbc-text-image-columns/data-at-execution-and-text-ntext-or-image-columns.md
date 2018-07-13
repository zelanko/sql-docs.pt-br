---
title: Dados em execução e Text, ntext ou colunas de imagem | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
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
- data-at-execution
- ODBC data-at-execution
- image columns [ODBC]
ms.assetid: 67ffb1a6-f38d-4712-ba64-96bdd41ec2b2
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d0e03c12fe94755e42c5838a66c85242cae59a62
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37416245"
---
# <a name="data-at-execution-and-text-ntext-or-image-columns"></a>Dados em execução e colunas Text, ntext ou Image
  Os dados em execução ODBC são um recurso que permite aos aplicativos trabalhar com quantidades extremamente grandes de dados em parâmetros ou colunas associadas. Ao recuperar grandes **texto**, **ntext**, ou **imagem** colunas, um aplicativo talvez não consiga simplesmente alocar um buffer enorme, associar a coluna no buffer e buscar a linha. Ao atualizar muito grandes **texto**, **ntext**, ou **imagem** colunas, o aplicativo pode não conseguir simplesmente alocar um buffer enorme, associá-lo a um marcador de parâmetro em um SQL instrução e, em seguida, execute a instrução. Nesses casos, o aplicativo deve usar [SQLGetData](../native-client-odbc-api/sqlgetdata.md) ou [SQLPutData](../native-client-odbc-api/sqlputdata.md) com suas opções de dados em execução.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciando colunas Text e Image](managing-text-and-image-columns.md)  
  
  
