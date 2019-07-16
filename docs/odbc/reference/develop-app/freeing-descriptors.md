---
title: Liberando descritores | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeHandle function [ODBC]
- descriptors [ODBC], allocating and freeing
- freeing descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 317213f4-0ebb-4bf8-a37a-4d6b1313823f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fe489222c026c1499135b716f0485bb04f51bad9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069768"
---
# <a name="freeing-descriptors"></a>Liberar descritores
Descritores explicitamente alocados podem ser liberado um explicitamente, chamando **SQLFreeHandle** com *HandleType* de SQL_HANDLE_DESC ou implicitamente, quando o identificador de conexão é liberado. Quando um descritor alocado explicitamente é liberado, todos os identificadores de instrução para o qual o descritor liberado aplicado automaticamente reverter para os descritores implicitamente alocados para eles.  
  
 Descritores implicitamente alocados podem ser liberados apenas chamando **SQLDisconnect**, que descarta todas as instruções ou descritores de abrir a conexão, ou chamando **SQLFreeHandle** com um  *HandleType* sql_handle_stmt para liberar um identificador de instrução e todos os descritores implicitamente alocados associados à instrução. Um descritor de implicitamente alocado não pode ser liberado chamando **SQLFreeHandle** com um *HandleType* de SQL_HANDLE_DESC.  
  
 Mesmo quando liberada, um descritor de implicitamente alocado permanece válido, e **SQLGetDescField** pode ser chamado em seus campos.
