---
title: Usando o SQLConfigDatasource com o driver ODBC para Oracle | Microsoft Docs
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
ms.openlocfilehash: fa5f1ecf9f3100480081e3744fc7d280a4da282b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68088032"
---
# <a name="using-sqlconfigdatasource-with-the-odbc-driver-for-oracle"></a>Usar SQLConfigDatasource com o driver ODBC para Oracle
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 A tabela a seguir lista as configurações de **SQLConfigDatasource** válidas para o Microsoft ODBC driver for Oracle, versão 1,0 (Msorcl10. dll) e o driver ODBC da Microsoft para Oracle, versão 2,0 (Msorcl32. dll).  
  
> [!NOTE]  
>  O driver Msorcl10. dll (versão 1,0) dá suporte a todas as configurações, exceto **servidor**. O driver Msorcl32. dll (versão 2,0 e superior) dá suporte a todas as configurações.  
  
 Algumas configurações são ignoradas pelo driver, mas são aceitas pelo **SQLConfigDatasource**. A inclusão dessas configurações na cadeia de conexão ODBC é a única maneira como elas serão aceitas em tempo de execução. Uma configuração ignorada não será armazenada no registro quando o **SQLConfigDatasource** criar a fonte de dados.  
  
 Na tabela a seguir, a */N* significa qualquer cadeia de caracteres alfanumérica válida até o comprimento máximo permitido. *Len máx* . (comprimento máximo) é o comprimento máximo permitido da cadeia de caracteres aceita pela configuração, incluindo o caractere de terminador de cadeia de caracteres.  
  
|Configuração|Len máx.|Valor padrão|Valores válidos|DESCRIÇÃO|  
|-------------|-------------|-------------------|------------------|-----------------|  
|BufferSize|7|65535|1000|Tamanho mínimo do buffer de busca de até 65535 bytes|  
|CatalogCap|2|1|0 ou 1|Se 1, os identificadores sem aspas serão convertidos em letras maiúsculas nas funções de catálogo.|  
|ConnectString|128|""|A/N|Cadeia de conexão. Método necessário para especificar o nome do servidor com o driver Msorcl10. dll.|  
|DESCRIÇÃO|256|""|A/N|Descrição.|  
|DSN|33|""|A/N|Nome da fonte de dados.|  
|GuessTheColDef|4|0|A/N|Retorna um valor diferente de zero para colunas sem a escala definida pela Oracle.|  
|NumberFloat|2|""|0 ou 1|Se 0, as colunas FLOAT serão tratadas como SQL_FLOAT. Se 1, as colunas FLOAT serão tratadas como SQL_DOUBLE.|  
|PWD|30|""|A/N|Senha.|  
|RDOSupport|2|""|0 ou 1|Permite que o RDO chame procedimentos Oracle.|  
|Comentários|2|0|0 ou 1|Incluir comentários em funções de catálogo.|  
|Limite de @|4|""|0 a 99|Número máximo de linhas retornadas por uma instrução SELECT. Uma cadeia de caracteres de comprimento zero indica que nenhum limite é aplicado.|  
|Servidor|128|""|A/N|Nome do servidor Oracle.|  
|SynonymColumns|2|1|0 ou 1|Incluir SINÔNIMOs em SQLColumns.|  
|Sistema de|2|""|0 ou 1|Se 0, as tabelas do sistema não serão exibidas. Se 1, as tabelas do sistema serão exibidas.|  
|TranslationDLL|33|""|A/N|Nome do translation. dll.|  
|Conversão de|33|""|A/N|Nome da tradução.|  
|TranslationOption|33|""|A/N|Opção de tradução.|  
|TxnCap|2|""|A/N|Com capacidade de transação. Se for 0, o driver relatará que ele não oferece suporte a transações. Se for 1, o driver relatará que ele é capaz de executar transações.|  
|UID|30|""|A/N|Nome de usuário.|
