---
title: SQLDriverConnect (driver do Excel) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLDriverConnect
- SQLDriverConnect function [ODBC], Excel Driver
ms.assetid: 285cb1ea-f461-4596-97f2-fc57af05dede
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e38f2f513b7da2c9342470ba75e2ee11b3d7e52a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68053906"
---
# <a name="sqldriverconnect-excel-driver"></a>SQLDriverConnect (Driver do Excel)
> [!NOTE]  
>  Este tópico fornece informações específicas do driver do Excel. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 O **SQLDriverConnect** permite que você se conecte a um driver sem criar uma fonte de dados (DSN).  
  
 As seguintes palavras-chave têm suporte na cadeia de conexão para todos os drivers: **DSN**, **DBQ**e **Fil**.  
  
 A tabela a seguir mostra as palavras-chave mínimas necessárias para se conectar a cada driver e fornece um exemplo de pares de palavra-chave/valor usados com **SQLDriverConnect**. Para obter uma lista completa dos valores de DRIVERid, consulte [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).  
  
> [!NOTE]  
>  Se DBQ ou DefaultDir não for especificado para o driver do Microsoft Excel 3,0 ou 4,0, o driver será conectado ao diretório atual.  
  
|Driver|Palavras-chave necessárias|Exemplos|  
|------------|-----------------------|--------------|  
|Microsoft Excel 3,0 ou 4,0|Driver, DriverID|Driver = {Microsoft Excel driver (*. xls)}; DBQ = c:\temp; DriverID = 278|  
|Microsoft Excel 5.0/7.0|Driver, DriverID, DBQ|Driver = {Microsoft Excel driver (*. xls)}; DBQ = c:\Temp\sample.xls; DriverID = 22|  
|Microsoft Excel 97 e posterior|Driver, DriverID, DBQ|Driver = {Microsoft Excel driver (*. xls)}; DBQ = c:\Temp\sample.xls; DriverID = 790|
