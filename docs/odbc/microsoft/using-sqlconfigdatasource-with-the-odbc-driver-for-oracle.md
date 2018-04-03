---
title: Usando SQLConfigDatasource com o Driver ODBC para Oracle | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], ODBC driver for Oracle
ms.assetid: e535d1ef-aff9-4ae7-a3ed-ef4ca2584289
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 90ebd3887adec06bfc0ec100101adf7ad7302645
ms.sourcegitcommit: 8f1d1363e18e0c32ff250617ab6cb2da2147bf8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/03/2018
---
# <a name="using-sqlconfigdatasource-with-the-odbc-driver-for-oracle"></a>Usando SQLConfigDatasource com o Driver ODBC para Oracle
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 A seguinte tabela lista válida **SQLConfigDatasource** configurações para o Microsoft ODBC Driver for Oracle, versão 1.0 (Msorcl10.dll) e o Microsoft ODBC Driver for Oracle, versão 2.0 (msorcl32. dll).  
  
> [!NOTE]  
>  O driver Msorcl10.dll (versão 1.0) oferece suporte a todas as configurações, exceto **Server**. O driver msorcl32. dll (versão 2.0 e posterior) dá suporte a todas as configurações.  
  
 Algumas configurações são ignoradas pelo driver, mas são aceitas pelo **SQLConfigDatasource**. Incluindo essas configurações na cadeia de caracteres de conexão ODBC é a única maneira em que eles serão aceitas em tempo de execução. Uma configuração ignorada não será armazenada no registro quando **SQLConfigDatasource** cria a fonte de dados.  
  
 Na tabela a seguir, *A/N* significa qualquer cadeia de caracteres alfanumérica válida até o comprimento máximo permitido. *Max Len* (máximo) é o comprimento máximo permitido aceito pela configuração, incluindo o caractere terminador de cadeia de caracteres.  
  
|Configuração|max Len|Valor padrão|Valores válidos|Description|  
|-------------|-------------|-------------------|------------------|-----------------|  
|BufferSize|7|65535|1.000|Até 65535 bytes de tamanho do buffer de busca mínimo|  
|CatalogCap|2|1|0 ou 1|Se for 1, identificadores nonquoted será convertido em maiusculas no catálogo de funções.|  
|ConnectString|128|""|A/N|Cadeia de conexão. Método necessário de especificar o nome do servidor com o driver Msorcl10.dll.|  
|Description|256|""|A/N|Descrição.|  
|DSN|33|""|A/N|Nome da fonte de dados.|  
|GuessTheColDef|4|0|A/N|Retorna um valor diferente de zero para colunas sem escala definidas pelo Oracle.|  
|NumberFloat|2|""|0 ou 1|Se for 0, FLOAT colunas são tratadas como SQL_FLOAT. Se for 1, FLOAT colunas são tratadas como SQL_DOUBLE.|  
|PWD|30|""|A/N|Senha.|  
|RDOSupport|2|""|0 ou 1|Permite RDO chamar procedimentos do Oracle.|  
|Remarks|2|0|0 ou 1|Inclua comentários em funções de catálogo.|  
|RowLimit|4|""|0 a 99|Número máximo de linhas retornadas por uma instrução SELECT. Uma cadeia de caracteres de comprimento zero indica que nenhum limite é aplicado.|  
|Servidor|128|""|A/N|Nome do servidor Oracle.|  
|SynonymColumns|2|1|0 ou 1|Inclua SYNONYMs em SQLColumns.|  
|SystemTable|2|""|0 ou 1|Se for 0, as tabelas do sistema não serão exibidas. Se for 1, as tabelas do sistema serão exibidas.|  
|TranslationDLL|33|""|A/N|Nome do. dll de conversão.|  
|TranslationName|33|""|A/N|Nome de tradução.|  
|TranslationOption|33|""|A/N|Opção de conversão.|  
|TxnCap|2|""|A/N|Compatível com a transação. Se for 0, o driver informa que não dá suporte a transações. Se for 1, o driver informa que ele seja capaz de realizar transações.|  
|UID|30|""|A/N|Nome de usuário.|
