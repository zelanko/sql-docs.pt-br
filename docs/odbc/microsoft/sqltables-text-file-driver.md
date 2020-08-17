---
description: SQLTables (Driver de Arquivo de texto)
title: Sqltablenames (driver de arquivo de texto) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], SQLTables
- SQLTables function [ODBC], Text File Driver
ms.assetid: f47fd1a4-5bd8-4b2e-8ae3-e595e49f4f95
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a6c6f65603cee70811d7c9894ba9d840d28ad4f4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339653"
---
# <a name="sqltables-text-file-driver"></a>SQLTables (Driver de Arquivo de texto)
> [!NOTE]  
>  Este tópico fornece informações específicas do driver de arquivo de texto. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Argumento|Comentários|  
|--------------|--------------|  
|*szTableOwner*|O único argumento válido para *szTableOwner* é nulo porque nenhum dos drivers dá suporte a nomes de proprietários. Com *szTableOwner* definido como NULL, todas as tabelas são retornadas. NULL é retornado na coluna TABLE_OWNER.|  
|*szTableQualifier*|Na coluna TABLE_QUALIFIER, **SQLTables** retornará o caminho para um diretório.|  
|*SzTableType*|"TABLE" é o único tipo de tabela com suporte.<br /><br /> Quando o driver de texto é usado, a lista de arquivos retornada por **SQLTables** é determinada pelas extensões de arquivo na caixa de **listagem extensões** na caixa de diálogo **configuração de texto ODBC** .|
