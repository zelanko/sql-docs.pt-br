---
title: Tipos de cursor | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- ODBC applications, cursors
- cursors [ODBC], types
- ODBC cursors, types
ms.assetid: 3a916cc7-f352-42cb-8b83-f78e06cef991
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a5b073ee58c0e29b1d7e6d02d079141838cef237
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705673"
---
# <a name="cursor-types"></a>Tipos de cursor
  O ODBC define quatro tipos de cursor com suporte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da Microsoft e do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Native Client. Esses cursores variam em sua capacidade de detectar alterações no conjunto de resultados e nos recursos que eles consomem, como memória e espaço em **tempdb**. Um cursor pode detectar alterações nas linhas apenas quando ele tenta buscar essas linhas novamente; não há como a fonte de dados notificar o cursor dessas alterações nas linhas que estão sendo buscadas atualmente. A capacidade de um cursor de detectar alterações que não foram feitas pelo cursor também é influenciada pelo nível de isolamento da transação.  
  
 Estes são os quatro tipos de cursor ODBC suportados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Cursores de somente avanço não suportam o recurso de rolagem; eles suportam apenas a busca de linhas em série do início ao fim do cursor.  
  
-   Cursores estáticos são criados em **tempdb** quando o cursor é aberto. Eles sempre exibem o conjunto de resultados da forma como ele estava quando o cursor foi aberto. Eles nunca refletem alterações aos dados. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cursores estáticos são sempre somente leitura. Como um cursor de servidor estático é criado como uma tabela de trabalho em **tempdb**, o tamanho do conjunto de resultados do cursor não pode exceder o tamanho máximo de linha permitido pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Os cursores controlados por conjunto de chaves têm a associação (membership) e a ordem das linhas fixas no conjunto de resultados quando o cursor é aberto. As alterações nas colunas não chave são visíveis pelo cursor.  
  
-   Os cursores dinâmicos são o oposto dos cursores estáticos. Eles refletem todas as alterações feitas nas linhas de seu conjunto de resultados. Os valores de dados, a ordem e a associação das linhas do conjunto de resultados podem ser alterados em cada busca.  
  
## <a name="see-also"></a>Consulte Também  
 [Usando cursores &#40;ODBC&#41;](using-cursors-odbc.md)  
  
  
