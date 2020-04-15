---
title: Suporte a roscas (driver Visual FoxPro ODBC) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2aa19eb233525b5a65ef67fe9903814fc1163177
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303077"
---
# <a name="thread-support-visual-foxpro-odbc-driver"></a>Suporte a thread (Driver ODBC do Visual FoxPro)
O driver Visual FoxPro ODBC é seguro para rosca. O acesso às alças do ambiente *(galinha),* alças de conexão *(hdbc)* e alças de declaração *(hstmt)* é envolto em semáforos apropriados para evitar que outros processos acessem e potencialmente alterem as estruturas internas de dados do motorista.  
  
 Em um aplicativo multithreaded, você pode cancelar uma função que está sendo executado sincronizadamente em um *hstmt* chamando [SQLCancel](../../odbc/microsoft/sqlcancel-visual-foxpro-odbc-driver.md) em um segmento separado.  
  
 O driver usa um segmento separado para obter dados quando você usa busca progressiva. Para usar a busca progressiva para uma fonte de dados, selecione os **dados do Fetch na** caixa de seleção de fundo na caixa de diálogo [Deconfiguração Visual FoxPro do ODBC](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md) ou use a palavra-chave de atributo BackgroundFetch na seqüência de conexões. Evite usar o background fetch quando você chamar o driver de aplicativos multithreaded. Para obter informações sobre palavras-chave de atributo de seqüência de conexão, consulte [Usando strings de conexão](../../odbc/microsoft/using-connection-strings.md).  
  
 Para obter mais informações sobre threads e **SQLCancel,** consulte [SQLCancel](../../odbc/reference/syntax/sqlcancel-function.md) na *referência do programador ODBC*.
