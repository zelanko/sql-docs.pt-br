---
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
ms.openlocfilehash: 2d2809f9b15dd6843e4404c7cf1887c3caa015a3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283916"
---
# <a name="sqlconfigdatasource-text-file-driver"></a>SQLConfigDataSource (Driver de Arquivo de texto)
> [!NOTE]  
>  Este tópico fornece informações específicas do Driver de arquivo de texto. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 A função **SQLConfigDataSource,** usada para adicionar, modificar ou excluir uma fonte de dados, usa dinamicamente as seguintes palavras-chave.  
  
|Palavra-chave|Descrição|  
|-------------|-----------------|  
|Characterset|Para o driver de texto, OEM ou ANSI.|  
|COLNAMEHEADER|Para o driver Texto, indica se o primeiro registro de dados especificará os nomes da coluna. SEJA VERDADEIRO OU FALSO.|  
|Defaultdir|A especificação do caminho para o diretório.|  
|DESCRIPTION|Uma descrição dos dados na fonte de dados.<br /><br /> Isso define a mesma opção **que Description** na caixa de diálogo de configuração.|  
|DRIVER|A especificação do caminho para o driver DLL.|  
|DRIVERID|Uma id inteira para o motorista. 27 (Texto)|  
|Extensões|Lista as extensões do nome do arquivo dos arquivos Texto na fonte de dados.<br /><br /> Isso define a mesma opção **que a lista de extensões** na caixa de diálogo de configuração.|  
|Fil|Texto do tipo de arquivo|  
|Filetype|Tipo de arquivo para o driver texto (Texto).|  
|FORMAT|Para o driver texto, pode ser FIXLENGTH, TABDELIMITED, CSVDELIMITED (por uma vírgula) ou DELIMITED() (pelo caractere especial especificado nos parênteses). O personagem especial é um personagem de comprimento e pode estar em caráter, decimal ou formato hexadecimal.|  
|MAXSCANROWS|O número de linhas a serem digitalizadas ao definir o tipo de dados de uma coluna com base nos dados existentes.<br /><br /> Para o driver Texto, você pode inserir um número de 1 a 32767 para o número de linhas a serem escaneadas; no entanto, o valor sempre será padrão para 25. (Um número fora do limite retornará um erro.)<br /><br /> Isso define a mesma opção **que Linhas para Scan na** caixa de diálogo de configuração.|  
|READONLY|TRUE para tornar somente leitura de arquivo; FALSO para fazer o arquivo não ler somente.<br /><br /> Isso define a mesma opção **que Read Only** na caixa de diálogo de configuração.|
