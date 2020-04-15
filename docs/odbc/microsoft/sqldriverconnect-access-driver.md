---
title: SQLDriverConnect (driver de acesso) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7a679cbb16ece3f239b1d17daabc8a294b808287
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302907"
---
# <a name="sqldriverconnect-access-driver"></a>SQLDriverConnect (Driver do Access)
> [!NOTE]  
>  Este tópico fornece informações específicas do Access Driver. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **O SQLDriverConnect** permite que você se conecte a um driver sem criar uma fonte de dados (DSN).  
  
 As seguintes palavras-chave são suportadas na seqüência de conexões para todos os drivers: **DSN,** **DBQ**e **FIL**.  
  
 As **palavras-chave UID** e **PWD** também são suportadas.  
  
 A palavra-chave PWD não deve incluir nenhum dos caracteres especiais (veja SQL_SPECIAL_CHARACTERS em Valores Retornados **SQLGetInfo).**  
  
 A tabela a seguir mostra as palavras-chave mínimas necessárias para se conectar a cada driver e fornece um exemplo de pares de palavras-chave/valor usados com **SQLDriverConnect**. Para obter uma lista completa de valores driverid, consulte [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).  
  
|Driver|Palavras-chave necessárias|Exemplos|  
|------------|-----------------------|--------------|  
|Microsoft Access|Driver, DBQ|Driver={Microsoft Access Driver (*.mdb)}; DBQ=c:\\\temp\\\sample.mdb|
