---
title: Tradução automática de Dados de Caracteres | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC], autotranslating character data
- data types [ODBC], autotranslating character data
- ACPs
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- AutoTranslate feature
- ANSI code pages
- character data autotranslation [ODBC]
- autotranslating character data
- SQL Server Native Client ODBC driver, data types
- ODBC data types, autotranslating character data
ms.assetid: 86a8adda-c5ad-477f-870f-cb370c39ee13
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2a8672f748af8d643fa39038be030efa5d434dc8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297876"
---
# <a name="autotranslation-of-character-data"></a>Tradução automática de dados de caracteres
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Os dados de caracteres, como variáveis de caracteres [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ANSI declaradas com SQL_C_CHAR ou dados armazenados usando os tipos **de dados char,** **varchar**ou **texto,** podem representar apenas um número limitado de caracteres. Os dados de caractere armazenados que usam um byte por caractere podem representar apenas 256 caracteres. Os valores armazenados em variáveis SQL_C_CHAR são interpretados usando a ACP (página de código ANSI) do computador cliente. Os valores armazenados usando **char,** **varchar**ou tipos de dados de **texto** no servidor são avaliados usando o ACP do servidor.  
  
 Se tanto o servidor quanto o cliente tiverem o mesmo ACP, então eles não terão problemas em interpretar os valores armazenados em SQL_C_CHAR, **char,** **varchar**ou objetos **de texto.** Se o servidor e o cliente tiverem ACPs diferentes, então SQL_C_CHAR dados do cliente podem ser interpretados como um caractere diferente no servidor se ele for usado em **colunas de char,** **varchar**ou **texto,** variáveis ou parâmetros. Por exemplo, um byte de caractere contendo o valor 0xA5 é interpretado como o caractere Ñ em um computador usando a página de código 437 e é interpretado como o sinal de iene (¥) em um computador executando a página 1252.  
  
 Dados de Unicode são armazenados usando dois bytes por caractere. Todos os caracteres estendidos são abordados pela especificação de Unicode. Dessa forma, todos os caracteres Unicode são interpretados da mesma maneira por todos os computadores.  
  
 O recurso AutoTranslate [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do driver ODBC do Cliente Nativo tenta minimizar os problemas na movimentação de dados de caracteres entre um cliente e um servidor que têm páginas de código diferentes. O AutoTranslate pode ser configurado na seqüência de conexão do [SQLDriverConnect,](../../relational-databases/native-client-odbc-api/sqldriverconnect.md)na seqüência [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de configuração do [SQLConfigDataSource,](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)ou ao configurar fontes de dados para o driver ODBC do Cliente Nativo usando o Administrador ODBC.  
  
 Quando o AutoTranslate é definido como "não", nenhuma conversão é feita em dados movidos entre SQL_C_CHAR variáveis no cliente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e **char,** **varchar**ou colunas de **texto,** variáveis ou parâmetros em um banco de dados. Os padrões de bit poderão ser interpretados de forma diferente nos computadores cliente e servidor se os dados contiverem caracteres estendidos e os dois computadores tiverem páginas de código diferentes. Os dados serão interpretados da mesma maneira se ambos os computadores tiverem a mesma página de código.  
  
 Quando o AutoTranslate é definido [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como "sim", o driver Cliente Nativo ODBC usa o Unicode para converter dados movidos entre SQL_C_CHAR [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] variáveis no cliente e **char,** **varchar**ou colunas de **texto,** variáveis ou parâmetros em um banco de dados:  
  
-   Quando os dados são enviados de uma variável SQL_C_CHAR no cliente para um **char** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , **varchar,** ou coluna de **texto,** variável ou parâmetro em um banco de dados, o driver ODBC primeiro converte de SQL_C_CHAR para Unicode usando o ACP do cliente, depois de Unicode de volta ao caractere usando o ACP do servidor.  
  
-   Quando os dados são enviados de um **char**, **varchar** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ou coluna de **texto,** variável ou parâmetro em um banco de dados para uma variável SQL_C_CHAR no cliente, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver Cliente Nativo ODBC primeiro converte de caractere para Unicode usando o ACP do servidor, depois de Unicode de volta para SQL_C_CHAR usando o ACP do cliente.  
  
 Como todas essas conversões são [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] feitas pelo driver ODBC do Cliente Nativo executando no cliente, o ACP do servidor deve ser uma das páginas de código instaladas no computador cliente.  
  
 Fazer as conversões de caractere por Unicode assegura a conversão adequada de todos os caracteres que existem nas duas páginas de código. Se um caractere existir em uma página de código, mas não em outra, entretanto, o caractere não poderá ser representado na página de código de destino. Por exemplo, a página de código 1252 tem o símbolo de marca registrada (®), enquanto a página de código 437 não tem.  
  
 A configuração AutoTranslate não tem nenhum efeito sobre essas conversões:  
  
-   Movendo dados entre variáveis de SQL_C_CHAR de caracteres e **nchar**unicode, **nvarchar** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou colunas de **texto,** variáveis ou parâmetros em bancos de dados.  
  
-   Movendo dados entre unicode SQL_C_WCHAR variáveis do cliente e **char**de caracteres, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **varchar,** ou colunas de **texto,** variáveis ou parâmetros em bancos de dados.  
  
 Os dados devem sempre ser convertidos quando movidos de caractere para Unicode.  
  
## <a name="see-also"></a>Consulte Também  
 [Resultados de processamento &#40;&#41;Da ODBC](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)   
 [Suporte a ordenações e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md)  
  
  
