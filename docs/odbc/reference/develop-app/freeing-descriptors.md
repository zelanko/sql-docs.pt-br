---
title: Liberando Descritores | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: af30ceb29e032764b89aa2069086aa898a7d35db
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305597"
---
# <a name="freeing-descriptors"></a>Liberar descritores
Descritores explicitamente alocados podem ser liberados explicitamente, ligando para **SQLFreeHandle** com *HandleType* de SQL_HANDLE_DESC, ou implicitamente, quando o cabo de conexão é liberado. Quando um descritor explicitamente alocado é liberado, todas as alças de instrução às quais o descritor liberado aplicado automaticamente revertem para os descritores implicitamente alocados para eles.  
  
 Descritores implicitamente alocados só podem ser liberados ligando para **SQLDisconnect**, que descarta quaisquer instruções ou descritores abertos na conexão, ou ligando para **o SQLFreeHandle** com um *HandleType* de SQL_HANDLE_STMT para liberar uma alça de instrução e todos os descritores implicitamente alocados associados à instrução. Um descritor implicitamente alocado não pode ser liberado ligando para **SQLFreeHandle** com um *HandleType* de SQL_HANDLE_DESC.  
  
 Mesmo quando libertado, um descritor implicitamente alocado permanece válido, e **o SQLGetDescField** pode ser chamado em seus campos.
