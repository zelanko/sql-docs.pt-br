---
title: SQLGetData (Drivers de banco de dados de desktop) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetData function [ODBC], Desktop Database Drivers
ms.assetid: c9d9a32d-5dc2-4189-9bfb-2b008bc3d6a3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2b102d8435831d45aad3c2049581513e0493de9a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304117"
---
# <a name="sqlgetdata-desktop-database-drivers"></a>SQLGetData (Drivers de banco de dados de área de trabalho)
Esta função pode recuperar dados de qualquer coluna, independentemente de haver colunas vinculadas depois dela e independentemente da ordem em que as colunas são recuperadas.  
  
> [!NOTE]  
>  \*pcbValue no **SQLGetData** pode retornar o dobro de caracteres que realmente disponíveis quando vinculado a dados ANSI com mais de 510 caracteres em um banco de dados Jet 4.0. Os valores de caractere de 510 ou menos retornarão o cbValue real.
