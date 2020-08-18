---
description: SQLConfigDataSource (Driver do dBASE)
title: SQLConfigDataSource (driver do dBASE) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBase driver [ODBC], SQLConfigDataSource
- SQLConfigDataSource function [ODBC], dBASE Driver
ms.assetid: 19909902-054c-4e19-9c06-a212aace13fe
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 23e734c5aafc903e210eea18f002f4c5e8d7a456
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411952"
---
# <a name="sqlconfigdatasource-dbase-driver"></a>SQLConfigDataSource (Driver do dBASE)
> [!NOTE]  
>  Este tópico fornece informações específicas do driver do dBASE. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 A função **SQLConfigDataSource** que é usada para adicionar, modificar ou excluir uma fonte de dados usa dinamicamente as seguintes palavras-chave.  
  
|Palavra-chave|Descrição|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|A sequência na qual os campos são classificados.<br /><br /> A sequência pode ser: ASCII (o padrão) ou internacional.<br /><br /> Isso define a mesma opção que a **sequência de agrupamento** na caixa de diálogo de instalação.|  
|DEFAULTDIR|A especificação de caminho para o diretório.|  
|DELETED|Para o driver do dBASE, especifica se as linhas que foram marcadas como excluídas podem ser recuperadas ou posicionadas. Se definido como 1, as linhas excluídas não serão exibidas; Se definido como 0, as linhas excluídas serão tratadas da mesma forma que as linhas não excluídas.<br /><br /> Isso define a mesma opção que **Mostrar linhas excluídas** na caixa de diálogo de instalação.|  
|DESCRIPTION|Uma descrição dos dados na fonte de dados.<br /><br /> Isso define a mesma opção que a **Descrição** na caixa de diálogo de instalação.|  
|DRIVER|A especificação de caminho para a DLL do driver.|  
|DRIVERid|Uma ID de inteiro para o driver.<br /><br /> 21 (dBASE III)<br /><br /> 277 (dBASE IV)<br /><br /> 533 (dBASE 5,0)|  
|FIL|Tipo de arquivo dBase III, dBase IV ou dBase 5|  
|PAGETIMEOUT|Especifica o período de tempo, em décimos de segundo, que uma página (se não usada) permanece no buffer antes de ser removida. O padrão é 600 décimos de segundo (60 segundos). Observe que essa opção se aplica a todas as fontes de dados que usam o driver ODBC.<br /><br /> Isso define a mesma opção como **tempo limite de página** na caixa de diálogo de instalação.|  
|READONLY|TRUE para tornar o arquivo somente leitura; FALSE para tornar o arquivo não somente leitura.<br /><br /> Isso define a mesma opção como **somente leitura** na caixa de diálogo de instalação.|  
|STATISTICS|Para o driver do dBASE, determina se as estatísticas de tamanho da tabela são aproximadas. Observe que essa opção se aplica a todas as fontes de dados que usam o driver ODBC.<br /><br /> Isso define a mesma opção que a **contagem aproximada de linhas** na caixa de diálogo de instalação.|  
|THREADS|O número de threads em segundo plano a ser usado pelo mecanismo. Esse valor é 3 e não pode ser alterado.<br /><br /> Isso define a mesma opção que os **threads** na caixa de diálogo de instalação.|
