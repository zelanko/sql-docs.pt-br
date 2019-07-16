---
title: SQLDriverConnect (Driver do Paradox) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLDriverConnect function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLDriverConnect
ms.assetid: c2ba486e-5e01-4e67-adb1-68511f5f0206
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e17ca12e0c8745dcad30a3e5ce2c9689b041e7d2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67967488"
---
# <a name="sqldriverconnect-paradox-driver"></a>SQLDriverConnect (Paradox Driver)
> [!NOTE]  
>  Este tópico fornece informações específicas de Driver do Paradox. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLDriverConnect** permite que você se conecte a um driver sem criar uma fonte de dados (DSN).  
  
 As seguintes palavras-chave têm suporte na cadeia de conexão para todos os drivers: **DSN**, **DBQ**, e **FIL**.  
  
 O **PWD** também há suporte para a palavra-chave. A palavra-chave PWD não deve incluir os caracteres especiais (consulte SQL_SPECIAL_CHARACTERS na **SQLGetInfo** valores retornados).  
  
 Depois que um arquivo protegido por senha tiver sido aberto por um usuário, outros usuários não são permitidos para abrir o mesmo arquivo.  
  
 A tabela a seguir mostra as palavras-chave mínimas necessárias para conectar a cada driver e fornece um exemplo de pares de palavra-chave/valor usada com **SQLDriverConnect**. Para obter uma lista completa de valores DRIVERID, consulte [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).  
  
> [!NOTE]  
>  Se DBQ ou DefaultDir não for especificado para o driver do Paradox, o driver se conectar ao diretório atual.  
  
|Driver|Palavras-chave necessárias|Exemplo|  
|------------|-----------------------|-------------|  
|Paradox|Driver, DriverID|Driver={Microsoft Paradox Driver (*.db )}; DBQ=c:\temp;DriverID=26|
