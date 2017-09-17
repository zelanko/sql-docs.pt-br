---
title: ODBC Jet SQLConfigDataSource (Driver do Excel) | Microsoft Docs
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
- SQLConfigDataSource function [ODBC], Excel Driver
- Excel driver [ODBC], SqlConfigDataSource
ms.assetid: 885b3bea-f4b6-4902-b994-f78a912b612f
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9a4d5d0b2feb0a09aafeb441c6b33260e4f0738b
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-jet-sqlconfigdatasource-excel-driver"></a>ODBC Jet SQLConfigDataSource (Driver do Excel)
> [!NOTE]  
>  Este tópico fornece informações específicas de Driver do Excel. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 O **SQLConfigDataSource** função que é usada para adicionar, modificar ou excluir uma fonte de dados dinamicamente usa as seguintes palavras-chave.  
  
|Palavra-chave|Description|  
|-------------|-----------------|  
|DBQ|Para o driver do Microsoft Excel ao acessar o Microsoft Excel 5.0 ou posteriores arquivos, o nome do arquivo de pasta de trabalho.<br /><br /> Isso define a mesma opção como **banco de dados** na caixa de diálogo de instalação.|  
|DEFAULTDIR|A especificação de caminho para o diretório.<br /><br /> Isso define a mesma opção como **Selecionar diretório** ou **Selecionar pasta de trabalho** na caixa de diálogo de instalação.|  
|DESCRIPTION|Uma descrição dos dados na fonte de dados.<br /><br /> Isso define a mesma opção como **descrição** na caixa de diálogo de instalação.|  
|DRIVER|A especificação de caminho para a DLL do driver.|  
|DRIVERID|Uma ID de inteiro para o driver.<br /><br /> 534 (Microsoft Excel 3.0)<br /><br /> 278 (Microsoft Excel 4.0)<br /><br /> 22 (Microsoft Excel 5.0/7.0)<br /><br /> 790 (Microsoft Excel 97-2003)|  
|FIL|Tipo de arquivo, por exemplo, Excel 3.0, Excel 4.0, 5.0 do Excel, Excel 7.0, Excel 97, Excel 2000 ou Excel 2003.|  
|FIRSTROWHASNAMES|Indica se as células da primeira linha do intervalo contêm os nomes de coluna para a tabela (1) ou não (0).|  
|MAXSCANROWS|O número de linhas a serem examinadas ao definir o tipo de dados da coluna com base em dados existentes.<br /><br /> Um número de 1 a 16 pode ser inserido para as linhas a serem examinadas. O valor padrão é 8; Se estiver definido como 0, todas as linhas são examinadas. (Um número fora do limite retornará um erro.)<br /><br /> Isso define a mesma opção como **linhas a examinar** na caixa de diálogo de instalação.|  
|READONLY|TRUE para tornar o arquivo somente leitura; FALSE para tornar o arquivo não é somente leitura.<br /><br /> Isso define a mesma opção como **somente leitura** na caixa de diálogo de instalação.|  
|THREADS|O número de threads de plano de fundo para o mecanismo de usar. Para o driver do Microsoft Access, esse valor padrão é 3, mas pode ser alterado. Para o dBASE MicrosoftExceldriver esse valor é 3 e não pode ser alterado.<br /><br /> Isso define a mesma opção como **Threads** na caixa de diálogo de instalação.|
