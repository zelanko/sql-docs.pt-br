---
title: SQLGetData (Drivers do banco de dados de área de trabalho) | Microsoft Docs
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
- SQLGetData function [ODBC], Desktop Database Drivers
ms.assetid: c9d9a32d-5dc2-4189-9bfb-2b008bc3d6a3
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eab1073046f314de01b7542e3bd4d1efaea802ca
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgetdata-desktop-database-drivers"></a>SQLGetData (Drivers do banco de dados de área de trabalho)
Essa função pode recuperar dados de qualquer coluna, ou não há colunas associadas depois dele e independentemente da ordem na qual as colunas são recuperadas.  
  
> [!NOTE]  
>  \*pcbValue em **SQLGetData** pode retornar caracteres como realmente disponíveis para dobro ao associar a dados ANSI excede 510 caracteres em um banco de dados Jet 4.0. Valores de caractere de 510 ou menos retornará o cbValue real.
