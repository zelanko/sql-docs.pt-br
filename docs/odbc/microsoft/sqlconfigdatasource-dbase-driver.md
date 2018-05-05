---
title: SQLConfigDataSource (dBASE Driver) | Microsoft Docs
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
- DBase driver [ODBC], SQLConfigDataSource
- SQLConfigDataSource function [ODBC], dBASE Driver
ms.assetid: 19909902-054c-4e19-9c06-a212aace13fe
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 84f099d65ae97a524a219fbe289305cfd1166715
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlconfigdatasource-dbase-driver"></a>SQLConfigDataSource (dBASE Driver)
> [!NOTE]  
>  Este tópico fornece informações de dBASE específica do Driver. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 O **SQLConfigDataSource** função que é usada para adicionar, modificar ou excluir uma fonte de dados dinamicamente usa as seguintes palavras-chave.  
  
|Palavra-chave|Description|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|A sequência na qual os campos são classificados.<br /><br /> A sequência pode ser: ASCII (o padrão) ou internacional.<br /><br /> Isso define a mesma opção como **sequência de agrupamento** na caixa de diálogo de instalação.|  
|DEFAULTDIR|A especificação de caminho para o diretório.|  
|DELETED|Para o driver dBASE, especifica se linhas que foram marcadas como excluídos podem ser recuperadas ou posicionadas em. Se definido como 1, linhas excluídas não é exibido; Se definido como 0, linhas excluídas é tratados da mesma como linhas excluídas não.<br /><br /> Isso define a mesma opção como **Mostrar linhas excluídas** na caixa de diálogo de instalação.|  
|DESCRIPTION|Uma descrição dos dados na fonte de dados.<br /><br /> Isso define a mesma opção como **descrição** na caixa de diálogo de instalação.|  
|DRIVER|A especificação de caminho para a DLL do driver.|  
|DRIVERID|Uma ID de inteiro para o driver.<br /><br /> 21 (dBASE III)<br /><br /> 277 (dBASE IV)<br /><br /> 533 (dBASE 5.0)|  
|FIL|Arquivos dBase III, dBase IV ou dBase 5 de tipo|  
|PAGETIMEOUT|Especifica o período de tempo, em décimos de segundo, que uma página (se não usado) permanece no buffer antes de serem removidos. O padrão é 600 décimos de segundo (60 segundos). Observe que essa opção se aplica a todas as fontes de dados que usam o driver ODBC.<br /><br /> Isso define a mesma opção como **Page Timeout** na caixa de diálogo de instalação.|  
|READONLY|TRUE para tornar o arquivo somente leitura; FALSE para tornar o arquivo não é somente leitura.<br /><br /> Isso define a mesma opção como **somente leitura** na caixa de diálogo de instalação.|  
|STATISTICS|Para o driver dBASE, determina se as estatísticas de tamanho de tabela são aproximadas. Observe que essa opção se aplica a todas as fontes de dados que usam o driver ODBC.<br /><br /> Isso define a mesma opção como **contagem aproximada de linha** na caixa de diálogo de instalação.|  
|THREADS|O número de threads de plano de fundo para o mecanismo de usar. Esse valor é 3 e não pode ser alterado.<br /><br /> Isso define a mesma opção como **Threads** na caixa de diálogo de instalação.|
