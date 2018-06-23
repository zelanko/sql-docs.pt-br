---
title: Vs associados. Não associado a colunas de texto e imagem | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
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
- image columns [ODBC]
ms.assetid: ffd3442e-d880-46e9-b848-2365a09a2406
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c5129c6b865723721bbb6f176893c950cdf905fe
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009533"
---
# <a name="bound-vs-unbound-text-and-image-columns"></a>Vs associados. Desassociado colunas de texto e imagem
  Ao usar cursores de servidor, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client é otimizado para não transmitir os dados para desassociada **texto**, **ntext**, ou **imagem** colunas do tempo **SQLFetch** é executada. O **texto**, **ntext**, ou **imagem** dados não são realmente recuperados do servidor até que o aplicativo não emite [SQLGetData](../native-client-odbc-api/sqlgetdata.md) para o coluna.  
  
 Muitos aplicativos podem ser gravados para que nenhum **texto**, **ntext**, ou **imagem** dados são exibidos enquanto um usuário está simplesmente rolando para cima e para baixo em um cursor. Quando um usuário seleciona uma linha para obter mais detalhes, o aplicativo pode chamar **SQLGetData** para recuperar o **texto**, **ntext**, ou **imagem** dados. Isso impedirá a transmissão de **texto**, **ntext**, ou **imagem** dados para qualquer uma das linhas que o usuário seleciona e, portanto, pode impedir a transmissão de grandes quantidades de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar colunas de texto e imagem](managing-text-and-image-columns.md)   
 [Comportamentos de cursor](../native-client-odbc-cursors/cursor-behaviors.md)  
  
  