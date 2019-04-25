---
title: Colunas de texto e imagem associadas vs. Não associado a colunas Text e Image | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 1bf8ac0cf868394d9aa8063220939feee69ac2f6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62626579"
---
# <a name="bound-vs-unbound-text-and-image-columns"></a>Colunas de texto e imagem associadas vs. não associadas
  Ao usar cursores de servidor, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client é otimizado para não transmitir os dados para desassociada **texto**, **ntext**, ou **imagem** colunas no tempo **SQLFetch** é executada. O **texto**, **ntext**, ou **imagem** dados não são realmente recuperados do servidor até que os problemas de aplicativos [SQLGetData](../native-client-odbc-api/sqlgetdata.md) para o coluna.  
  
 Muitos aplicativos podem ser gravados para que nenhum **texto**, **ntext**, ou **imagem** dados seja exibidos enquanto um usuário está simplesmente rolando para cima para baixo em um cursor. Quando um usuário seleciona uma linha para obter mais detalhes, o aplicativo pode chamar **SQLGetData** para recuperar o **texto**, **ntext**, ou **imagem** dados. Esse procedimento impedirá a **texto**, **ntext**, ou **imagem** dados para qualquer uma das linhas que o usuário seleciona e pode, portanto, evitar a transmissão de muito grandes quantidades de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciando colunas Text e Image](managing-text-and-image-columns.md)   
 [Comportamentos de cursor](../native-client-odbc-cursors/cursor-behaviors.md)  
  
  
