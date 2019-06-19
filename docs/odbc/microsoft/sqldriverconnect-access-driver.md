---
title: SQLDriverConnect (Access Driver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLDriverConnect
- SQLDriverConnect function [ODBC], Access Driver
ms.assetid: 9d133e9b-7545-464d-aa3c-677fa7e2a41d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9a71874c91e48c25072fbfed8f66a312d65b4697
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63048470"
---
# <a name="sqldriverconnect-access-driver"></a>SQLDriverConnect (Driver do Access)
> [!NOTE]  
>  Este tópico fornece informações específicas de Driver do Access. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLDriverConnect** permite que você se conecte a um driver sem criar uma fonte de dados (DSN).  
  
 As seguintes palavras-chave têm suporte na cadeia de conexão para todos os drivers: **DSN**, **DBQ**, e **FIL**.  
  
 O **UID** e **PWD** palavras-chave também têm suporte.  
  
 A palavra-chave PWD não deve incluir os caracteres especiais (consulte SQL_SPECIAL_CHARACTERS na **SQLGetInfo** valores retornados).  
  
 A tabela a seguir mostra as palavras-chave mínimas necessárias para conectar a cada driver e fornece um exemplo de pares de palavra-chave/valor usada com **SQLDriverConnect**. Para obter uma lista completa de valores DRIVERID, consulte [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).  
  
|Driver|Palavras-chave necessárias|Exemplos|  
|------------|-----------------------|--------------|  
|Microsoft Access|Driver, DBQ|Driver={Microsoft Access Driver (*.mdb)}; DBQ=c:\\\temp\\\sample.mdb|
