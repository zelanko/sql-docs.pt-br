---
title: Usando SQLConfigDatasource com o Driver ODBC para Oracle | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], ODBC driver for Oracle
ms.assetid: e535d1ef-aff9-4ae7-a3ed-ef4ca2584289
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9edd9ae15e66a39abd84a8a6d8e50a83ed4a39ba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63259342"
---
# <a name="using-sqlconfigdatasource-with-the-odbc-driver-for-oracle"></a>Usar SQLConfigDatasource com o driver ODBC para Oracle
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 A seguinte tabela lista válida **SQLConfigDatasource** configurações para o Microsoft ODBC Driver para o Oracle, versão 1.0 (Msorcl10.dll) e o Microsoft ODBC Driver para o Oracle, versão 2.0 (msorcl32. dll).  
  
> [!NOTE]  
>  O driver Msorcl10.dll (versão 1.0) dá suporte a todas as configurações, exceto **Server**. O driver msorcl32. dll (versão 2.0 e superior) dá suporte a todas as configurações.  
  
 Algumas configurações são ignoradas pelo driver, mas são aceitos pelo **SQLConfigDatasource**. Incluir essas configurações na cadeia de caracteres de conexão ODBC é a única maneira que serão aceitas no tempo de execução. Uma configuração ignorada não será armazenada no registro quando **SQLConfigDatasource** cria a fonte de dados.  
  
 Na tabela a seguir *A/N* significa qualquer cadeia de caracteres alfanumérica válida até o comprimento máximo permitido. *max Len* (comprimento máximo) é o comprimento máximo permitido aceito pela configuração, incluindo o caractere terminador da cadeia de caracteres.  
  
|Configuração|máx Len|Valor padrão|Valores válidos|Descrição|  
|-------------|-------------|-------------------|------------------|-----------------|  
|BufferSize|7|65535|1\.000|Até 65535 bytes de tamanho do buffer de busca mínimo|  
|CatalogCap|2|1|0 ou 1|Se for 1, identificadores nonquoted será convertido em letras maiusculas no catálogo de funções.|  
|ConnectString|128|""|A/N|Cadeia de conexão. Método necessário de especificar o nome do servidor com o driver Msorcl10.dll.|  
|Descrição|256|""|A/N|Descrição.|  
|DSN|33|""|A/N|Nome da fonte de dados.|  
|GuessTheColDef|4|0|A/N|Retorna um valor diferente de zero para colunas sem escala definido pelo Oracle.|  
|NumberFloat|2|""|0 ou 1|Se for 0, FLOAT colunas são tratadas como SQL_FLOAT. Se for 1, FLOAT colunas são tratadas como SQL_DOUBLE.|  
|PWD|30|""|A/N|Senha.|  
|RDOSupport|2|""|0 ou 1|Permite RDO chamar procedimentos do Oracle.|  
|Comentários|2|0|0 ou 1|Inclua comentários em funções de catálogo.|  
|RowLimit|4|""|0 a 99|Número máximo de linhas retornadas por uma instrução SELECT. Uma cadeia de caracteres de comprimento zero indica que nenhum limite é aplicado.|  
|Servidor|128|""|A/N|Nome do servidor Oracle.|  
|SynonymColumns|2|1|0 ou 1|Inclua sinônimos em SQLColumns.|  
|SystemTable|2|""|0 ou 1|Se for 0, as tabelas do sistema não serão exibidas. Se for 1, tabelas do sistema serão exibidas.|  
|TranslationDLL|33|""|A/N|Nome. dll de conversão.|  
|TranslationName|33|""|A/N|Nome de tradução.|  
|TranslationOption|33|""|A/N|Opção de conversão.|  
|TxnCap|2|""|A/N|Compatível com a transação. Se for 0, o driver informa que ele não oferece suporte a transações. Se for 1, o driver informa que é capaz de realizar transações.|  
|UID|30|""|A/N|Nome de usuário.|
