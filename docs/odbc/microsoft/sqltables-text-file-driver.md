---
title: SQLTables (Driver de arquivo de texto) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], SQLTables
- SQLTables function [ODBC], Text File Driver
ms.assetid: f47fd1a4-5bd8-4b2e-8ae3-e595e49f4f95
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc441c302d1d8e6589f885b41e9fa1ae7d6ab787
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqltables-text-file-driver"></a>SQLTables (Driver de arquivo de texto)
> [!NOTE]  
>  Este tópico fornece informações específicas de Driver do arquivo de texto. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Argumento|Comentários|  
|--------------|--------------|  
|*szTableOwner*|O argumento só é válido para *szTableOwner* é NULL porque nenhum dos drivers de suporte a nomes de proprietário. Com *szTableOwner* definido como NULL, todas as tabelas são retornadas. NULL é retornado na coluna TABLE_OWNER.|  
|*szTableQualifier*|Na coluna TABLE_QUALIFIER, **SQLTables** retornará o caminho para um diretório.|  
|*SzTableType*|"TABLE" é o único tipo de tabela com suporte.<br /><br /> Quando o driver de texto é usado, a lista de arquivos retornados por **SQLTables** é determinado pelas extensões de arquivo no **lista extensões** caixa o **config** caixa de diálogo.|
