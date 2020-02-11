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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68114065"
---
# <a name="the-odbc-cursor-library"></a>A biblioteca de cursores ODBC
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Os cursores de bloqueio e rolagem são adições muito úteis a muitos aplicativos. No entanto, nem todos os drivers dão suporte a cursores de bloqueio e rolável. O mesmo se aplica às instruções UPDATE e DELETE posicionadas e **SQLSetPos**, que são discutidas na atualização de dados. Portanto, o componente ODBC do SDK do Windows, anteriormente incluído no SDK do MDAC (Microsoft Data Access Components), inclui uma biblioteca de cursores. A biblioteca de cursores implementa o bloco, cursores estáticos, instruções UPDATE e DELETE posicionadas e **SQLSetPos** para qualquer driver que atenda ao nível de conformidade da CLI padrão do grupo aberto. A biblioteca de cursores pode ser redistribuída com aplicativos ODBC; consulte o contrato de licenciamento no SDK para obter mais informações.  
  
 Para usar a biblioteca de cursores, um aplicativo define o atributo de conexão SQL_ATTR_ODBC_CURSORS antes de se conectar à fonte de dados. Para obter mais informações sobre a biblioteca de cursores, consulte o [Apêndice F: biblioteca de cursores ODBC](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md).
