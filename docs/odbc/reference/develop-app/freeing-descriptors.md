---
title: Liberando descritores | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeHandle function [ODBC]
- descriptors [ODBC], allocating and freeing
- freeing descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 317213f4-0ebb-4bf8-a37a-4d6b1313823f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0977ba814841ab2fa445a1009262e4a2bfd3a5b3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="freeing-descriptors"></a>Descritores de liberação
Descritores explicitamente alocados podem ser liberada seja explicitamente, chamando **SQLFreeHandle** com *HandleType* de SQL_HANDLE_DESC ou implicitamente, quando o identificador de conexão é liberado. Quando um descritor alocado explicitamente é liberado, todos os identificadores de instrução para o qual o descritor livre aplicado automaticamente reverter para os descritores de alocado implicitamente para eles.  
  
 Descritores implicitamente alocados podem ser liberados apenas chamando **SQLDisconnect**, que descarta todas as instruções ou descritores de abrir a conexão, ou chamando **SQLFreeHandle** com um  *HandleType* sql_handle_stmt para liberar um identificador de instrução e todos os descritores de alocado implicitamente associados à instrução. Um descritor alocado implicitamente não pode ser liberado chamando **SQLFreeHandle** com um *HandleType* de SQL_HANDLE_DESC.  
  
 Mesmo quando liberado, um descritor alocado implicitamente permanece válido, e **SQLGetDescField** pode ser chamado em seus campos.
