---
title: SQLDriverConnect (Driver de acesso) | Microsoft Docs
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
- Access driver [ODBC], SQLDriverConnect
- SQLDriverConnect function [ODBC], Access Driver
ms.assetid: 9d133e9b-7545-464d-aa3c-677fa7e2a41d
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 450a30f8388b2ca7fb52f19cbda06ee27bf3fdb3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqldriverconnect-access-driver"></a>SQLDriverConnect (Driver de acesso)
> [!NOTE]  
>  Este tópico fornece informações específicas de Driver de acesso. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLDriverConnect** permite que você se conectar a um driver sem criar uma fonte de dados (DSN).  
  
 As seguintes palavras-chave têm suporte na cadeia de conexão para todos os drivers: **DSN**, **DBQ**, e **FIL**.  
  
 O **UID** e **PWD** palavras-chave também têm suporte.  
  
 A palavra-chave PWD não deve incluir os caracteres especiais (consulte SQL_SPECIAL_CHARACTERS em **SQLGetInfo** valores retornados).  
  
 A tabela a seguir mostra as palavras-chave mínimo necessárias para se conectar a cada driver e fornece um exemplo de pares de palavra-chave/valor usados com **SQLDriverConnect**. Para obter uma lista completa de valores DRIVERID, consulte [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).  
  
|Driver|Palavras-chave necessárias|Exemplos|  
|------------|-----------------------|--------------|  
|Microsoft Access|Driver, DBQ|Driver = {Driver do Microsoft Access (*.mdb)}; DBQ = c:\\\temp\\\sample.mdb|
