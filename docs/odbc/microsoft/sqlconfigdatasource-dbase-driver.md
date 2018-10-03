---
title: SQLConfigDataSource (Driver do dBASE) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 63d1951cfe835cbfca23ab366db2216215aa92c3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47631644"
---
# <a name="sqlconfigdatasource-dbase-driver"></a>SQLConfigDataSource (Driver do dBASE)
> [!NOTE]  
>  Este tópico fornece informações específicas do Driver do dBASE. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 O **SQLConfigDataSource** função que é usada para adicionar, modificar ou excluir uma fonte de dados usa as seguintes palavras-chave dinamicamente.  
  
|Palavra-chave|Description|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|A sequência na qual os campos são classificados.<br /><br /> A sequência pode ser: ASCII (o padrão) ou internacional.<br /><br /> Isso define a mesma opção como **sequência de agrupamento** na caixa de diálogo de instalação.|  
|DEFAULTDIR|A especificação de caminho para o diretório.|  
|DELETED|Para o driver do dBASE, especifica se linhas que foram marcadas como excluídos podem ser recuperadas ou posicionadas no. Se definido como 1, linhas excluídas não é exibido; Se definido como 0, linhas excluídas é tratadas como linhas não excluídos.<br /><br /> Isso define a mesma opção como **Mostrar linhas excluídas** na caixa de diálogo de instalação.|  
|DESCRIPTION|Uma descrição dos dados na fonte de dados.<br /><br /> Isso define a mesma opção como **descrição** na caixa de diálogo de instalação.|  
|DRIVER|A especificação de caminho para a DLL do driver.|  
|DRIVERID|Uma ID de inteiro para o driver.<br /><br /> 21 (dBASE III)<br /><br /> 277 (dBASE IV)<br /><br /> 533 (dBASE 5.0)|  
|FIL|Arquivos dBase III, dBase IV ou dBase 5 de tipo|  
|PAGETIMEOUT|Especifica o período de tempo, em décimos de segundo, que uma página (se não usado) permanece no buffer antes de serem removidos. O padrão é 600 décimos de segundo (60 segundos). Observe que essa opção se aplica a todas as fontes de dados que usam o driver ODBC.<br /><br /> Isso define a mesma opção como **Page Timeout** na caixa de diálogo de instalação.|  
|READONLY|TRUE para tornar o arquivo somente leitura; FALSE para tornar o arquivo não é somente leitura.<br /><br /> Isso define a mesma opção como **somente leitura** na caixa de diálogo de instalação.|  
|STATISTICS|Para o driver do dBASE, determina se as estatísticas de tamanho de tabela são aproximadas. Observe que essa opção se aplica a todas as fontes de dados que usam o driver ODBC.<br /><br /> Isso define a mesma opção como **contagem de linha aproximada** na caixa de diálogo de instalação.|  
|THREADS|O número de threads em segundo plano para o mecanismo a ser usado. Esse valor é 3 e não pode ser alterado.<br /><br /> Isso define a mesma opção como **Threads** na caixa de diálogo de instalação.|
