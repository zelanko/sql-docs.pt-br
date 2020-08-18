---
description: SQLConfigDataSource (Driver de Arquivo de texto)
title: SQLConfigDataSource (driver de arquivo de texto) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 400b83d382140d4661b103e24449f14ecdfda43d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411862"
---
# <a name="sqlconfigdatasource-text-file-driver"></a>SQLConfigDataSource (Driver de Arquivo de texto)
> [!NOTE]  
>  Este tópico fornece informações específicas do driver de arquivo de texto. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 A função **SQLConfigDataSource** que é usada para adicionar, modificar ou excluir uma fonte de dados usa dinamicamente as seguintes palavras-chave.  
  
|Palavra-chave|Descrição|  
|-------------|-----------------|  
|CHARACTERSET|Para o driver de texto, OEM ou ANSI.|  
|COLNAMEHEADER|Para o driver de texto, indica se o primeiro registro de dados especificará os nomes de coluna. TRUE ou FALSE.|  
|DEFAULTDIR|A especificação de caminho para o diretório.|  
|DESCRIPTION|Uma descrição dos dados na fonte de dados.<br /><br /> Isso define a mesma opção que a **Descrição** na caixa de diálogo de instalação.|  
|DRIVER|A especificação de caminho para a DLL do driver.|  
|DRIVERid|Uma ID de inteiro para o driver. 27 (texto)|  
|WMZ|Lista as extensões de nome de arquivo dos arquivos de texto na fonte de dados.<br /><br /> Isso define a mesma opção que a **lista de extensões** na caixa de diálogo de instalação.|  
|FIL|Texto do tipo de arquivo|  
|Talvez|Tipo de arquivo do driver de texto (texto).|  
|FORMAT|Para o driver de texto, pode ser cadeia, TABDELIMITED, CSVDELIMITED (por uma vírgula) ou delimitado () (pelo caractere especial especificado entre parênteses). O caractere especial tem um caractere de comprimento e pode estar em formato de caractere, decimal ou hexadecimal.|  
|MAXSCANROWS|O número de linhas a serem examinadas ao definir o tipo de dados de uma coluna com base nos dados existentes.<br /><br /> Para o driver de texto, você pode inserir um número de 1 a 32767 para o número de linhas a serem verificadas; no entanto, o valor sempre usará como padrão 25. (Um número fora do limite retornará um erro.)<br /><br /> Isso define a mesma opção que as **linhas a serem verificadas** na caixa de diálogo de instalação.|  
|READONLY|TRUE para tornar o arquivo somente leitura; FALSE para tornar o arquivo não somente leitura.<br /><br /> Isso define a mesma opção como **somente leitura** na caixa de diálogo de instalação.|
