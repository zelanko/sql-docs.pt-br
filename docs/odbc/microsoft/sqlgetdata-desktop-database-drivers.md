---
title: "SQLGetData (Drivers do banco de dados de área de trabalho) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLGetData function [ODBC], Desktop Database Drivers
ms.assetid: c9d9a32d-5dc2-4189-9bfb-2b008bc3d6a3
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e091bf31e034eaabb9c87931bc6b128f5bdeba84
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetdata-desktop-database-drivers"></a>SQLGetData (Drivers do banco de dados de área de trabalho)
Essa função pode recuperar dados de qualquer coluna, ou não há colunas associadas depois dele e independentemente da ordem na qual as colunas são recuperadas.  
  
> [!NOTE]  
>  \*pcbValue em **SQLGetData** pode retornar caracteres como realmente disponíveis para dobro ao associar a dados ANSI excede 510 caracteres em um banco de dados Jet 4.0. Valores de caractere de 510 ou menos retornará o cbValue real.
