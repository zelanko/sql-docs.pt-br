---
title: SQLConfigDataSource (Driver de arquivo de texto) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], SQLConfigDataSource
- SQLConfigDataSource function [ODBC], Text File Driver
ms.assetid: c505d36e-1e72-47b2-a9e5-e4926b408468
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 46bb00fb01ed3fee8098420794af089f2d8b981e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68054078"
---
# <a name="sqlconfigdatasource-text-file-driver"></a>SQLConfigDataSource (Driver de Arquivo de texto)
> [!NOTE]  
>  Este tópico fornece informações específicas de Driver de arquivo de texto. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 O **SQLConfigDataSource** função que é usada para adicionar, modificar ou excluir uma fonte de dados usa as seguintes palavras-chave dinamicamente.  
  
|Palavra-chave|Descrição|  
|-------------|-----------------|  
|CHARACTERSET|Para o driver de texto, ANSI ou OEM.|  
|COLNAMEHEADER|Para o driver de texto, indica se o primeiro registro de dados especificará os nomes de coluna. VERDADEIRO ou falso.|  
|DEFAULTDIR|A especificação de caminho para o diretório.|  
|DESCRIPTION|Uma descrição dos dados na fonte de dados.<br /><br /> Isso define a mesma opção como **descrição** na caixa de diálogo de instalação.|  
|DRIVER|A especificação de caminho para a DLL do driver.|  
|DRIVERID|Uma ID de inteiro para o driver. 27 (texto)|  
|EXTENSÕES|Lista as extensões de nome de arquivo dos arquivos de texto na fonte de dados.<br /><br /> Isso define a mesma opção como **lista de extensões** na caixa de diálogo de instalação.|  
|FIL|Tipo de arquivo de texto|  
|TIPO DE ARQUIVO|Tipo de arquivo para o driver de texto (texto).|  
|FORMAT|Para o driver de texto, que pode ser FIXEDLENGTH, TABDELIMITED, CSVDELIMITED (por uma vírgula) ou DELIMITED() (pelo caractere especial especificado nos parênteses). O caractere especial é um caractere de comprimento e pode estar no formato de caractere, decimal ou hexadecimal.|  
|MAXSCANROWS|O número de linhas a serem examinadas ao definir o tipo de dados da coluna com base nos dados existentes.<br /><br /> Para o driver de texto, você pode inserir um número de 1 a 32767 para o número de linhas a serem examinadas; No entanto, o valor será sempre padrão 25. (Um número fora do limite retornará um erro.)<br /><br /> Isso define a mesma opção como **linhas a examinar** na caixa de diálogo de instalação.|  
|READONLY|TRUE para tornar o arquivo somente leitura; FALSE para tornar o arquivo não é somente leitura.<br /><br /> Isso define a mesma opção como **somente leitura** na caixa de diálogo de instalação.|
