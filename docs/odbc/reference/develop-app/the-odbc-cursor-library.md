---
title: A biblioteca de cursores ODBC | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a896a5bb41c5530c65573fa22c418199a043f8fa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114065"
---
# <a name="the-odbc-cursor-library"></a>A biblioteca de cursores ODBC
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que usam esse recurso atualmente. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Bloco e cursores roláveis são adições úteis para muitos aplicativos. No entanto, nem todos os drivers dão suporte a cursores roláveis e bloco. O mesmo é verdadeiro para atualização posicionadas e instruções delete e **SQLSetPos**, que são abordadas na atualização de dados. Portanto, o componente ODBC do SDK do Windows, anteriormente incluídas no Microsoft Data Access Components (MDAC) SDK, inclui uma biblioteca de cursor. A biblioteca de cursores implementa o bloco, Cursores estáticos, instruções de exclusão e atualização posicionadas e **SQLSetPos** para qualquer driver que satisfaça o nível de conformidade com a CLI de padrão de grupo aberto. A biblioteca de cursores pode ser redistribuída com aplicativos de ODBC; Consulte o contrato de licenciamento no SDK para obter mais informações.  
  
 Para usar a biblioteca de cursores, um aplicativo define o atributo de conexão SQL_ATTR_ODBC_CURSORS antes de se conectar à fonte de dados. Para obter mais informações sobre a biblioteca de cursores, consulte [apêndice f: Biblioteca de cursores ODBC](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md).
