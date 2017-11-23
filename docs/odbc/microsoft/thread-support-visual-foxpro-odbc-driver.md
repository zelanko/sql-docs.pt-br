---
title: Thread de suporte (Driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- thread support [ODBC]
- Visual FoxPro ODBC driver [ODBC], thread support
- FoxPro ODBC driver [ODBC], thread support
- multithreaded applications [ODBC]
ms.assetid: 0c6abbbc-012b-41aa-bded-5e7e362d015b
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 691ff249f971a7c7baa16a8409786cde455d58a5
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="thread-support-visual-foxpro-odbc-driver"></a>Suporte de thread (Driver ODBC do Visual FoxPro)
O Driver de ODBC do Visual FoxPro é thread-safe. Acesso aos identificadores de ambiente (*uando*), identificadores de conexão (*hdbc*) e identificadores de instrução (*hstmt*) é encapsulado em semáforos apropriados para impedir que outros processos Acessando e alterando potencialmente estruturas de dados interno do driver.  
  
 Em um aplicativo multithread, você pode cancelar uma função que está executando em modo síncrono em um *hstmt* chamando [SQLCancel](../../odbc/microsoft/sqlcancel-visual-foxpro-odbc-driver.md) em um thread separado.  
  
 O driver usa um thread separado para buscar dados quando você usa a busca progressivo. Para usar buscando progressivo para uma fonte de dados, selecione o **buscar dados no plano de fundo** caixa de seleção de [caixa de diálogo a instalação do Visual FoxPro ODBC](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md) ou use a palavra-chave de atributo BackgroundFetch na sua conexão cadeia de caracteres. Evite usar busca em segundo plano quando você chama o driver de aplicativos multithread. Para obter informações sobre palavras-chave atributo de cadeia de caracteres de conexão, consulte [usando cadeias de caracteres de Conexão](../../odbc/microsoft/using-connection-strings.md).  
  
 Para obter mais informações sobre threads e **SQLCancel**, consulte [SQLCancel](../../odbc/reference/syntax/sqlcancel-function.md) no *referência do programador de ODBC*.
