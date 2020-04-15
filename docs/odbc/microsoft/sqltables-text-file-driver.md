---
title: SQLTables (Driver de arquivo de texto) | Microsoft Docs
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
ms.openlocfilehash: 938ceba5da25d176628d5c1d9875383d977e3aec
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299326"
---
# <a name="sqltables-text-file-driver"></a>SQLTables (Driver de Arquivo de texto)
> [!NOTE]  
>  Este tópico fornece informações específicas do Driver de arquivo de texto. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Argumento|Comentários|  
|--------------|--------------|  
|*szTableOwner*|O único argumento válido para *szTableOwner* é NULL porque nenhum dos drivers suporta nomes de proprietários. Com *szTableOwner* definido como NULL, todas as tabelas são devolvidas. NULL é devolvido na coluna TABLE_OWNER.|  
|*szTableQualifier*|Na coluna TABLE_QUALIFIER, o **SQLTables** retornará o caminho para um diretório.|  
|*SzTableType*|"TABLE" é o único tipo de tabela suportado.<br /><br /> Quando o driver de texto é usado, a lista de arquivos retornados pelo **SQLTables** é determinada pelas extensões de arquivo na caixa **Lista de extensões** na caixa de diálogo **Configuração de texto ODBC.**|
