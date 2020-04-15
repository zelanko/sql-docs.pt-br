---
title: A Biblioteca Cursor ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], about cursor library
- ODBC cursor library [ODBC]
- cursor library [ODBC], about cursor library
- scrollable cursors [ODBC]
- cursors [ODBC], cursor library
- block cursors [ODBC]
ms.assetid: 32fb7df0-953a-4f68-b041-7d2852e45d0f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b243e8ae2dc931830a249d4392da308e68722cdf
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300046"
---
# <a name="the-odbc-cursor-library"></a>A biblioteca de cursores ODBC
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar aplicativos que atualmente usam esse recurso. A Microsoft recomenda o uso da funcionalidade do cursor do driver.  
  
 Cursores de blocos e roláveis são adições muito úteis para muitos aplicativos. No entanto, nem todos os drivers suportam cursores de bloco e roláveis. O mesmo se aplica às declarações de atualização e exclusão posicionadas e **SQLSetPos**, que são discutidas na Atualização de Dados. Portanto, o componente ODBC do Windows SDK, anteriormente incluído no Microsoft Data Access Components (MDAC) SDK, inclui uma biblioteca de cursor. A biblioteca do cursor implementa cursores de bloco, cursores estáticos, instruções de atualização e exclusão posicionadas e **SQLSetPos** para qualquer driver que atenda ao nível de conformidade CLI padrão do Grupo Aberto. A biblioteca do cursor pode ser redistribuída com aplicativos ODBC; consulte o contrato de licenciamento no SDK para obter mais informações.  
  
 Para usar a biblioteca do cursor, um aplicativo define o atributo de conexão SQL_ATTR_ODBC_CURSORS antes de se conectar à fonte de dados. Para obter mais informações sobre a biblioteca do cursor, consulte [o apêndice F: ODBC Cursor Library](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md).
