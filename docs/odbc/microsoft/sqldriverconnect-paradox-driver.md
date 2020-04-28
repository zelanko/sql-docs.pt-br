---
title: SQLDriverConnect (driver do Paradox) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 68171cfab2b65634433b107d829dd2a6e9b5c985
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307107"
---
# <a name="sqldriverconnect-paradox-driver"></a>SQLDriverConnect (Driver do Paradox)
> [!NOTE]  
>  Este tópico fornece informações específicas do driver do Paradox. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 O **SQLDriverConnect** permite que você se conecte a um driver sem criar uma fonte de dados (DSN).  
  
 As seguintes palavras-chave têm suporte na cadeia de conexão para todos os drivers: **DSN**, **DBQ**e **Fil**.  
  
 Também há suporte para a palavra-chave **pwd** . A palavra-chave PWD não deve incluir nenhum dos caracteres especiais (consulte SQL_SPECIAL_CHARACTERS em valores retornados **SQLGetInfo** ).  
  
 Depois que um arquivo protegido por senha tiver sido aberto por um usuário, outros usuários não terão permissão para abrir o mesmo arquivo.  
  
 A tabela a seguir mostra as palavras-chave mínimas necessárias para se conectar a cada driver e fornece um exemplo de pares de palavra-chave/valor usados com **SQLDriverConnect**. Para obter uma lista completa dos valores de DRIVERid, consulte [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).  
  
> [!NOTE]  
>  Se DBQ ou DefaultDir não for especificado para o driver do Paradox, o driver se conectará ao diretório atual.  
  
|Driver|Palavras-chave necessárias|Exemplo|  
|------------|-----------------------|-------------|  
|Paradox|Driver, DriverID|Driver = {Microsoft Paradox driver (*. DB)}; DBQ = c:\temp; DriverID = 26|
