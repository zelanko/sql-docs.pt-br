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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f9343361e7ad6fbfdf68b82218a39a56fa8d928e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68053916"
---
# <a name="sqldriverconnect-text-file-driver"></a>SQLDriverConnect (Driver de Arquivo de texto)
> [!NOTE]  
>  Este tópico fornece informações específicas do driver de arquivo de texto. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 O **SQLDriverConnect** permite que você se conecte a um driver sem criar uma fonte de dados (DSN).  
  
 As seguintes palavras-chave têm suporte na cadeia de conexão para todos os drivers: **DSN**, **DBQ**e **Fil**.  
  
 A tabela a seguir mostra as palavras-chave mínimas necessárias para se conectar a cada driver e fornece um exemplo de pares de palavra-chave/valor usados com **SQLDriverConnect**. Para obter uma lista completa dos valores de DRIVERid, consulte [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).  
  
> [!NOTE]  
>  Se DBQ ou DefaultDir não for especificado para o driver de texto, o driver se conectará ao diretório atual.  
  
|Driver|Palavras-chave necessárias|Exemplos|  
|------------|-----------------------|--------------|  
|Texto|Driver|Driver = {Microsoft Text driver (*. txt;\*. CSV)}; DefaultDir = c:\temp|
