---
title: SQLDriverConnect (driver de arquivo de texto) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLDriverConnect function [ODBC], Text File Driver
- text file driver [ODBC], SQLDriverConnect
ms.assetid: d7769021-bd18-4d8e-96e0-e184a82d6ca3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2768669b7dbb2066de0acedd5711911be0eac8fa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307097"
---
# <a name="sqldriverconnect-text-file-driver"></a>SQLDriverConnect (Driver de Arquivo de texto)
> [!NOTE]  
>  Este tópico fornece informações específicas do Driver de arquivo de texto. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **O SQLDriverConnect** permite que você se conecte a um driver sem criar uma fonte de dados (DSN).  
  
 As seguintes palavras-chave são suportadas na seqüência de conexões para todos os drivers: **DSN,** **DBQ**e **FIL**.  
  
 A tabela a seguir mostra as palavras-chave mínimas necessárias para se conectar a cada driver e fornece um exemplo de pares de palavras-chave/valor usados com **SQLDriverConnect**. Para obter uma lista completa de valores driverid, consulte [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).  
  
> [!NOTE]  
>  Se DBQ ou DefaultDir não forem especificados para o driver Texto, o driver se conectará ao diretório atual.  
  
|Driver|Palavras-chave necessárias|Exemplos|  
|------------|-----------------------|--------------|  
|Texto|Driver|Driver={Microsoft Text Driver (*.txt;\*. csv)}; DefaultDir=c:\temp|
