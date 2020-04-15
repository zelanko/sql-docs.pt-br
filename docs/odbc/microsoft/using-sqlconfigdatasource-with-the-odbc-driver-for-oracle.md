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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 718e444d63e0d4cf3821c0c03eb851732ed5b4e4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292766"
---
# <a name="using-sqlconfigdatasource-with-the-odbc-driver-for-oracle"></a>Usar SQLConfigDatasource com o driver ODBC para Oracle
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 A tabela a seguir lista as configurações válidas **do SQLConfigDatasource** para o Microsoft ODBC Driver for Oracle, a versão 1.0 (Msorcl10.dll) e o Microsoft ODBC Driver for Oracle, versão 2.0 (Msorcl32.dll).  
  
> [!NOTE]  
>  O driver Msorcl10.dll (versão 1.0) suporta todas as configurações, exceto **server**. O driver Msorcl32.dll (versão 2.0 ou superior) suporta todas as configurações.  
  
 Algumas configurações são ignoradas pelo driver, mas são aceitas pelo **SQLConfigDatasource**. Incluir essas configurações na seqüência de conexões ODBC é a única maneira de serem aceitas em tempo de execução. Uma configuração ignorada não será armazenada no registro quando o **SQLConfigDatasource** criar a fonte de dados.  
  
 Na tabela a seguir, *A/N* significa qualquer string alfanumérica válida até o comprimento máximo permitido. *Max Len* (comprimento máximo) é o comprimento máximo permitido da seqüência de strings aceito pela configuração, incluindo o caractere exterminador de cordas.  
  
|Configuração|Max Len|Valor padrão|Valores válidos|Descrição|  
|-------------|-------------|-------------------|------------------|-----------------|  
|BufferSize|7|65535|1000|Tamanho mínimo de buffer de busca até 65535 bytes|  
|CatálogoCap|2|1|0 ou 1|Se 1, os identificadores não citados serão convertidos em maiúsculas nas funções do catálogo.|  
|ConnectString|128|""|A/N|Cadeia de conexão. Método necessário para especificar o nome do servidor com o driver Msorcl10.dll.|  
|Descrição|256|""|A/N|Descrição.|  
|DSN|33|""|A/N|Nome da fonte dos dados.|  
|GuessTheColDef|4|0|A/N|Retorna um valor não-zero para colunas sem escala definida pelo Oracle.|  
|Flutuação numérica|2|""|0 ou 1|Se 0, as colunas FLOAT são tratadas como SQL_FLOAT. Se 1, as colunas FLOAT são tratadas como SQL_DOUBLE.|  
|PWD|30|""|A/N|Senha.|  
|Suporte rdo|2|""|0 ou 1|Permite que o RDO ligue para procedimentos Oracle.|  
|Comentários|2|0|0 ou 1|Inclua OBSERVAÇÕES em funções de catálogo.|  
|Rowlimit|4|""|0 a 99|Número máximo de linhas retornadas por uma declaração SELECT. Uma seqüência de comprimento zero indica que nenhum limite é aplicado.|  
|Servidor|128|""|A/N|Nome do servidor Oracle.|  
|Colunas de Sinônimos|2|1|0 ou 1|Inclua SYNONYMs em Colunas SQL.|  
|Tabela de sistemas|2|""|0 ou 1|Se 0, as tabelas do sistema não serão exibidas. Se 1, as tabelas do sistema serão exibidas.|  
|TraduçãoDLL|33|""|A/N|Nome de tradução .dll.|  
|Nome da tradução|33|""|A/N|Nome da tradução.|  
|Translationoption|33|""|A/N|Opção de tradução.|  
|TxnCap|2|""|A/N|Transação capaz. Se 0, o driver informa que não suporta transações. Se 1, o motorista informa que é capaz de realizar transações.|  
|UID|30|""|A/N|Nome de usuário.|
