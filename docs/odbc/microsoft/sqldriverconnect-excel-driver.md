---
title: SQLDriverConnect (Driver do Excel) | Microsoft Docs
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
- Excel driver [ODBC], SQLDriverConnect
- SQLDriverConnect function [ODBC], Excel Driver
ms.assetid: 285cb1ea-f461-4596-97f2-fc57af05dede
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: eca660cf2c38539dbf4a0fa560bfc67a1b1be115
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqldriverconnect-excel-driver"></a>SQLDriverConnect (Driver do Excel)
> [!NOTE]  
>  Este tópico fornece informações específicas de Driver do Excel. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLDriverConnect** permite que você se conectar a um driver sem criar uma fonte de dados (DSN).  
  
 As seguintes palavras-chave têm suporte na cadeia de conexão para todos os drivers: **DSN**, **DBQ**, e **FIL**.  
  
 A tabela a seguir mostra as palavras-chave mínimo necessárias para se conectar a cada driver e fornece um exemplo de pares de palavra-chave/valor usados com **SQLDriverConnect**. Para obter uma lista completa de valores DRIVERID, consulte [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).  
  
> [!NOTE]  
>  Se DBQ ou DefaultDir não for especificado para o Microsoft Excel 3.0 ou 4.0 do driver, o driver se conectar ao diretório atual.  
  
|Driver|Palavras-chave necessárias|Exemplos|  
|------------|-----------------------|--------------|  
|O Microsoft Excel 3.0 ou 4.0|Driver, DriverID|Driver = {Driver do Microsoft Excel (*. xls)}; DBQ = c:\temp; DriverID = 278|  
|O Microsoft Excel 5.0/7.0|Driver, DriverID, DBQ|Driver = {Driver do Microsoft Excel (*. xls)}; DBQ=c:\Temp\sample.xls; DriverID = 22|  
|O Microsoft Excel 97 e posterior|Driver, DriverID, DBQ|Driver = {Driver do Microsoft Excel (*. xls)}; DBQ=c:\Temp\sample.xls; DriverID = 790|

