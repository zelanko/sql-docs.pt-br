---
title: Suporte a thread (driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- thread support [ODBC]
- Visual FoxPro ODBC driver [ODBC], thread support
- FoxPro ODBC driver [ODBC], thread support
- multithreaded applications [ODBC]
ms.assetid: 0c6abbbc-012b-41aa-bded-5e7e362d015b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 72672cfc20b5d363229fd1ba49278d11e6d6793d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67912411"
---
# <a name="thread-support-visual-foxpro-odbc-driver"></a>Suporte a thread (Driver ODBC do Visual FoxPro)
O driver ODBC do Visual FoxPro é thread-safe. O acesso a identificadores de ambiente (*galinha*), identificadores de conexão (*HDBC*) e identificadores de instrução (*HSTMT*) é encapsulado em semáforos apropriados para impedir que outros processos acessem e potencialmente alterem as estruturas de dados internas do driver.  
  
 Em um aplicativo multithread, você pode cancelar uma função que está sendo executada de forma síncrona em um *HSTMT* chamando [SQLCancel](../../odbc/microsoft/sqlcancel-visual-foxpro-odbc-driver.md) em um thread separado.  
  
 O driver usa um thread separado para buscar dados quando você usa a busca progressiva. Para usar a busca progressiva de uma fonte de dados, marque a caixa de seleção **buscar dados em segundo plano** na [caixa de diálogo configuração do ODBC do Visual FoxPro](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md) ou use a palavra-chave do atributo BackgroundFetch na cadeia de conexão. Evite usar a busca em segundo plano ao chamar o driver de aplicativos multissegmentados. Para obter informações sobre palavras-chave de atributo de cadeia de conexão, consulte [usando cadeias de conexão](../../odbc/microsoft/using-connection-strings.md).  
  
 Para obter mais informações sobre threads e **SQLCancel**, consulte [SQLCancel](../../odbc/reference/syntax/sqlcancel-function.md) na *referência do programador de ODBC*.
