---
title: SQLConfigDataSource (Driver de arquivo de texto) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- text file driver [ODBC], SQLConfigDataSource
- SQLConfigDataSource function [ODBC], Text File Driver
ms.assetid: c505d36e-1e72-47b2-a9e5-e4926b408468
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b26eba11563baeef77e0fc47597a50776c5dc179
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlconfigdatasource-text-file-driver"></a>SQLConfigDataSource (Driver de arquivo de texto)
> [!NOTE]  
>  Este tópico fornece informações específicas de Driver do arquivo de texto. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 O **SQLConfigDataSource** função que é usada para adicionar, modificar ou excluir uma fonte de dados dinamicamente usa as seguintes palavras-chave.  
  
|Palavra-chave|Description|  
|-------------|-----------------|  
|CHARACTERSET|Para o driver de texto, OEM ou ANSI.|  
|COLNAMEHEADER|Para o driver de texto, indica se o primeiro registro de dados especificará os nomes de coluna. VERDADEIRO ou falso.|  
|DEFAULTDIR|A especificação de caminho para o diretório.|  
|DESCRIPTION|Uma descrição dos dados na fonte de dados.<br /><br /> Isso define a mesma opção como **descrição** na caixa de diálogo de instalação.|  
|DRIVER|A especificação de caminho para a DLL do driver.|  
|DRIVERID|Uma ID de inteiro para o driver. 27 (texto)|  
|EXTENSÕES|Lista as extensões de nome de arquivo dos arquivos de texto na fonte de dados.<br /><br /> Isso define a mesma opção como **lista extensões** na caixa de diálogo de instalação.|  
|FIL|Tipo de arquivo de texto|  
|TIPO DE ARQUIVO|Tipo de arquivo para o driver de texto (texto).|  
|FORMAT|Para o driver de texto, pode ser FIXEDLENGTH, TABDELIMITED, CSVDELIMITED (por uma vírgula) ou DELIMITED() (pelo caractere especial especificado entre parênteses). O caractere especial é um caractere de comprimento e pode estar no formato de caractere, decimal ou hexadecimal.|  
|MAXSCANROWS|O número de linhas a serem examinadas ao definir o tipo de dados da coluna com base em dados existentes.<br /><br /> Para o driver de texto, você pode inserir um número de 1 a 32767 para o número de linhas a serem examinadas; No entanto, o valor padrão será sempre 25. (Um número fora do limite retornará um erro.)<br /><br /> Isso define a mesma opção como **linhas a examinar** na caixa de diálogo de instalação.|  
|READONLY|TRUE para tornar o arquivo somente leitura; FALSE para tornar o arquivo não é somente leitura.<br /><br /> Isso define a mesma opção como **somente leitura** na caixa de diálogo de instalação.|
