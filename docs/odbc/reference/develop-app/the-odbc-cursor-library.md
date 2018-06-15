---
title: A biblioteca de cursores ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], about cursor library
- ODBC cursor library [ODBC]
- cursor library [ODBC], about cursor library
- scrollable cursors [ODBC]
- cursors [ODBC], cursor library
- block cursors [ODBC]
ms.assetid: 32fb7df0-953a-4f68-b041-7d2852e45d0f
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 861b4c98042dc5f7b94e831dc8ed1306ea8b3213
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32915061"
---
# <a name="the-odbc-cursor-library"></a>A biblioteca de cursores ODBC
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. A Microsoft recomenda o uso da funcionalidade de cursor do driver.  
  
 Bloco e cursores roláveis são adições muito útil para muitos aplicativos. No entanto, nem todos os drivers dão suporte a bloco e cursores roláveis. O mesmo é verdadeiro para atualização posicionada e instruções delete e **SQLSetPos**, que são abordadas na atualização de dados. Portanto, o componente ODBC do SDK do Windows, anteriormente incluída no Microsoft Data Access Components (MDAC) SDK, inclui uma biblioteca de cursor. A biblioteca de cursores implementa bloco, Cursores estáticos, posicionada instruções update e delete, e **SQLSetPos** para qualquer driver que atende o nível de conformidade de CLI de padrão de grupo aberto. A biblioteca de cursores pode ser redistribuída com aplicativos de ODBC. Consulte o contrato de licença no SDK para obter mais informações.  
  
 Para usar a biblioteca de cursores, um aplicativo define o atributo de conexão SQL_ATTR_ODBC_CURSORS antes de se conectar à fonte de dados. Para obter mais informações sobre a biblioteca de cursores, consulte [biblioteca de cursores de ODBC apêndice f:](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md).
