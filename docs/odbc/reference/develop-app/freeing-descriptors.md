---
title: Liberar descritores | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68069768"
---
# <a name="freeing-descriptors"></a>Liberar descritores
Os descritores explicitamente alocados podem ser liberados explicitamente, chamando **SQLFreeHandle** com *handletype* de SQL_HANDLE_DESC, ou implicitamente, quando o identificador de conexão é liberado. Quando um descritor explicitamente alocado é liberado, todos os identificadores de instrução para os quais o descritor liberado foi aplicado são revertidos automaticamente para os descritores implicitamente alocados para eles.  
  
 Os descritores implicitamente alocados só podem ser liberados chamando **SQLDisconnect**, o que descarta quaisquer instruções ou descritores abertos na conexão, ou chamando **SQLFreeHandle** com um *HandleType* de SQL_HANDLE_STMT para liberar um identificador de instrução e todos os descritores implicitamente alocados associados à instrução. Um descritor implicitamente alocado não pode ser liberado chamando **SQLFreeHandle** com um *handletype* de SQL_HANDLE_DESC.  
  
 Mesmo quando liberados, um descritor implicitamente alocado permanece válido e **SQLGetDescField** pode ser chamado em seus campos.
