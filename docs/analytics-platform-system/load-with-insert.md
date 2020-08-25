---
title: Carregar dados com INSERT
description: Usando a instrução T-SQL INSERT para carregar dados em uma tabela distribuída ou replicada do PDW (data warehouse paralelo).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: c28d15febb08855b914e4cd6ed04a97850ffe02c
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88766855"
---
# <a name="load-data-with-insert-into-parallel-data-warehouse"></a>Carregar dados com inserção em data warehouse paralelo

Você pode usar a instrução de inserção TSQL para carregar dados em uma tabela distribuída ou replicada SQL Server em paralelo data warehouse (PDW). Para obter mais informações sobre INSERT, consulte [Insert](../t-sql/statements/insert-transact-sql.md). Para tabelas replicadas e todas as colunas de não distribuição em uma tabela distribuída, o PDW usa SQL Server para converter implicitamente os valores de dados especificados na instrução para o tipo de dados da coluna de destino. Para obter mais informações sobre regras de conversão de dados de SQL Server, consulte [conversão de tipo de dados para SQL](../t-sql/data-types/data-type-conversion-database-engine.md). No entanto, para colunas de distribuição, o PDW dá suporte apenas a um subconjunto de conversões implícitas às quais SQL Server dá suporte. Portanto, quando você usa a instrução INSERT para carregar dados em uma coluna de distribuição, os dados de origem devem ser especificados em um dos formatos definidos nas tabelas a seguir.  
  
  
## <a name="insert-literals-into-binary-types"></a><a name="InsertingLiteralsBinary"></a>Inserir literais em tipos binários  
A tabela a seguir define os tipos de literal aceitos, o formato e as regras de conversão para inserir um valor literal em uma coluna de distribuição do tipo **Binary** (*n*) ou **varbinary**(*n*).  
  
|Tipo literal|Formatar|Regras de conversão|  
|----------------|----------|--------------------|  
|Literal binário|0x*hexidecimal_string*<br /><br />Exemplo: 0x12Ef|Os literais binários devem ser prefixados com 0x.<br /><br />O comprimento da fonte de dados não pode exceder o número de bytes especificados para o tipo de dados.<br /><br />Se o comprimento da fonte de dados for menor que o tamanho do tipo de dados **Binary** , os dados serão preenchidos à direita com zeros para alcançar o tamanho do tipo de dados.|  
  
## <a name="insert-literals-into-date-and-time-types"></a><a name="InsertingLiteralsDateTime"></a>Inserir literais em tipos de data e hora  
Os literais de data e hora são representados usando valores de caracteres em formatos específicos, entre aspas simples. As tabelas a seguir definem os tipos de literal permitidos, o formato e as regras de conversão para inserir um literal de data ou hora em uma SQL Server PDW coluna de distribuição do tipo **DateTime**, **smalldatetime**, **Date**, **time**, **DateTimeOffset**ou **datetime2**.  
  
### <a name="datetime-data-type"></a>tipo de dados DateTime  
A tabela a seguir define os formatos e as regras aceitas para inserir valores literais em uma coluna de distribuição do tipo **DateTime**. Qualquer cadeia de caracteres vazia (' ') é convertida para o valor padrão ' 1900-01-01 12:00:00.000 '. Cadeias de caracteres que contêm apenas espaços em branco (' ') geram um erro.  
  
|Tipo literal|Formatar|Regras de conversão|  
|----------------|----------|--------------------|  
|Literal de cadeia de caracteres no formato **DateTime**|' AAAA-MM-DD hh: mm: SS [. nnn] '<br /><br />Exemplo: ' 2007-05-08 12:35:29.123 '|Os dígitos fracionários ausentes são definidos como 0 quando o valor é inserido. Por exemplo, o literal ' 2007-05-08 12:35 ' é inserido como ' 2007-05-08 12:35:00.000 '.|  
|Literal de cadeia de caracteres no formato **smalldatetime**|' AAAA-MM-DD hh: mm '<br /><br />Exemplo: ' 2007-05-08 12:35 '|Segundos e dígitos fracionários restantes são definidos como 0 quando o valor é inserido.|  
|Literal de cadeia de caracteres no formato de **Data**|' AAAA-MM-DD '<br /><br />Exemplo: ' 2007-05-08 '|Os valores de hora (hora, minutos, segundos e frações) são definidos como 12:00:00.000 quando o valor é inserido.|  
|Literal de cadeia de caracteres no formato **datetime2**|' AAAA-MM-DD hh: mm: SS. nnnnnnn '<br /><br />Exemplo: ' 2007-05-08 12:35:29.1234567 '|Os dados de origem não podem exceder três dígitos fracionários. Por exemplo, o literal ' 2007-05-08 12:35:29.123 ' será inserido, mas o valor ' 2007-05-08 12:35:29.1234567 ' gerará um erro.|  
  
### <a name="smalldatetime-data-type"></a>tipo de dados smalldatetime  
A tabela a seguir define os formatos e as regras aceitas para inserir valores literais em uma coluna de distribuição do tipo **smalldatetime**. Qualquer cadeia de caracteres vazia (' ') é convertida para o valor padrão ' 1900-01-01 12:00 '. Cadeias de caracteres que contêm apenas espaços em branco (' ') geram um erro.  
  
|Tipo literal|Formatar|Regras de conversão|  
|----------------|----------|--------------------|  
|Literal de cadeia de caracteres no formato **smalldatetime**|' AAAA-MM-DD hh: mm ' ou ' AAAA-MM-DD hh: mm: 00 '<br /><br />Exemplo: ' 2007-05-08 12:00 ' ou ' 2007-05-08 12:00:00 '|Os dados de origem devem ter valores para ano, mês, data, hora e minuto. Segundos são opcionais e, se presentes, devem ser definidos com o valor 00. Qualquer outro valor gera um erro.|  
|Literal de cadeia de caracteres no formato de **Data**|' AAAA-MM-DD '<br /><br />Exemplo: ' 2007-05-08 '|Os valores de hora (hora, minutos, segundos e frações) são definidos como 0 quando o valor é inserido.|  
  
### <a name="date-data-type"></a>tipo de dados de data  
A tabela a seguir define os formatos e as regras aceitas para inserir valores literais em uma coluna de distribuição do tipo **Date**. Qualquer cadeia de caracteres vazia (' ') é convertida para o valor padrão ' 1900-01-01 '. Cadeias de caracteres que contêm apenas espaços em branco (' ') geram um erro.  
  
|Tipo literal|Formatar|Regras de conversão|  
|----------------|----------|--------------------|  
|Literal de cadeia de caracteres no formato de **Data**|' AAAA-MM-DD '<br /><br />Exemplo: ' 2007-05-08 '|Esse é o único formato aceito.|  
  
### <a name="time-data-type"></a>tipo de dados time  
A tabela a seguir define os formatos e as regras aceitas para inserir valores literais em uma coluna de distribuição do tipo **time**. Qualquer cadeia de caracteres vazia (' ') é convertida para o valor padrão ' 00:00:00.0000 '. Cadeias de caracteres que contêm apenas espaços em branco (' ') geram um erro.  
  
|Tipo literal|Formatar|Regras de conversão|  
|----------------|----------|--------------------|  
|Literal de cadeia de caracteres no formato de **hora**|' hh: mm: SS. nnnnnnn '<br /><br />Exemplo: ' 12:35:29.1234567 '|Se a fonte de dados tiver uma precisão menor ou igual (número de dígitos fracionários) do que a precisão do tipo de dados de **tempo** , os dados serão preenchidos à direita com zeros. Por exemplo, um valor literal ' 12:35:29.123 ' é inserido como ' 12:35:29.1230000 '.<br /><br />Um valor que tem uma precisão maior do que o tipo de dados de destino é rejeitado.|  
  
### <a name="datetimeoffset-data-type"></a>tipo de dados DateTimeOffset  
A tabela a seguir define os formatos e regras aceitos para inserir valores literais em uma coluna de distribuição do tipo **DateTimeOffset** (*n*). O formato padrão é ' AAAA-MM-DD hh: mm: SS. nnnnnnn {+ |-} hh: mm '. Uma cadeia de caracteres vazia (' ') é convertida para o valor padrão ' 1900-01-01 12:00:00.0000000 + 00:00 '. Cadeias de caracteres que contêm apenas espaços em branco (' ') geram um erro. O número de dígitos fracionários depende da definição de coluna. Por exemplo, uma coluna definida como **DateTimeOffset** (2) terá dois dígitos fracionários.  
  
|Tipo literal|Formatar|Regras de conversão|  
|----------------|----------|--------------------|  
|Literal de cadeia de caracteres no formato **DateTime**|' AAAA-MM-DD hh: mm: SS [. nnn] '<br /><br />Exemplo: ' 2007-05-08 12:35:29.123 '|Dígitos fracionários e valores de deslocamento ausentes são definidos como 0 quando o valor é inserido. Por exemplo, o literal ' 2007-05-08 12:35:29.123 ' é inserido como ' 2007-05-08 12:35:29.1230000 + 00:00 '.|  
|Literal de cadeia de caracteres no formato **smalldatetime**|' AAAA-MM-DD hh: mm '<br /><br />Exemplo: ' 2007-05-08 12:35 '|Segundos, os dígitos fracionários restantes e os valores de deslocamento são definidos como 0 quando o valor é inserido.|  
|Literal de cadeia de caracteres no formato de **Data**|' AAAA-MM-DD '<br /><br />Exemplo: ' 2007-05-08 '|Os valores de hora (hora, minutos, segundos e frações) são definidos como 0 quando o valor é inserido. Por exemplo, o literal ' 2007-05-08 ' é inserido como ' 2007-05-08 00:00:00.0000000 + 00:00 '.|  
|Literal de cadeia de caracteres no formato **datetime2**|' AAAA-MM-DD hh: mm: SS. nnnnnnn '<br /><br />Exemplo: ' 2007-05-08 12:35:29.1234567 '|Os dados de origem não podem exceder o número especificado de segundos fracionários na coluna DateTimeOffset. Se a fonte de dados tiver um número menor ou igual de segundos fracionários, os dados serão preenchidos à direita com zeros. Por exemplo, se o tipo de dados for DateTimeOffset (5), o valor literal ' 2007-05-08 12:35:29.123 + 12:15 ' será inserido como ' 12:35:29.12300 + 12:15 '.|  
|Literal de cadeia de caracteres no formato **DateTimeOffset**|' AAAA-MM-DD hh: mm: SS. nnnnnnn {+&#124;-} hh: mm '<br /><br />Exemplo: ' 2007-05-08 12:35:29.1234567 + 12:15 '|Os dados de origem não podem exceder o número especificado de segundos fracionários na coluna DateTimeOffset. Se a fonte de dados tiver um número menor ou igual de segundos fracionários, os dados serão preenchidos à direita com zeros. Por exemplo, se o tipo de dados for DateTimeOffset (5), o valor literal ' 2007-05-08 12:35:29.123 + 12:15 ' será inserido como ' 12:35:29.12300 + 12:15 '.|  
  
### <a name="datetime2-data-type"></a>tipo de dados datetime2  
A tabela a seguir define os formatos e regras aceitos para inserir valores literais em uma coluna de distribuição do tipo **datetime2** (*n*). O formato padrão é ' AAAA-MM-DD hh: mm: SS. nnnnnnn '. Uma cadeia de caracteres vazia (' ') é convertida para o valor padrão ' 1900-01-01 12:00:00 '. Cadeias de caracteres que contêm apenas espaços em branco (' ') geram um erro. O número de dígitos fracionários depende da definição de coluna. Por exemplo, uma coluna definida como **datetime2** (2) terá dois dígitos fracionários.  
  
|Tipo literal|Formatar|Regras de conversão|  
|----------------|----------|--------------------|  
|Literal de cadeia de caracteres no formato **DateTime**|' AAAA-MM-DD hh: mm: SS [. nnn] '<br /><br />Exemplo: ' 2007-05-08 12:35:29.123 '|Os segundos fracionários são opcionais e são definidos como 0 quando o valor é inserido.<br /><br />Um valor que tem mais dígitos fracionários do que o tipo de dados de destino é rejeitado.|  
|Literal de cadeia de caracteres no formato **smalldatetime**|' AAAA-MM-DD hh: mm '<br /><br />Exemplo: ' 2007-05-08 12 '|Os segundos opcionais e os dígitos fracionários restantes são definidos como 0 quando o valor é inserido.|  
|Literal de cadeia de caracteres no formato de **Data**|' AAAA-MM-DD '<br /><br />Exemplo: ' 2007-05-08 '|Os valores de hora (hora, minutos, segundos e frações) são definidos como 0 quando o valor é inserido. Por exemplo, o literal ' 2007-05-08 ' é inserido como ' 2007-05-08 12:00:00.0000000 '.|  
|Literal de cadeia de caracteres no formato **datetime2**|' AAAA-MM-DD hh: mm: SS: nnnnnnn '<br /><br />Exemplo: ' 2007-05-08 12:35:29.1234567 '|Se a fonte de dados contiver componentes de dados e de tempo menores ou iguais ao valor especificado em **datetime2**(*n*), os dados serão inseridos; caso contrário, um erro será gerado.|  
  
## <a name="insert-literals-into-numeric-types"></a><a name="InsertLiteralsNumeric"></a>Inserir literais em tipos numéricos  
As tabelas a seguir definem os formatos aceitos e as regras de conversão para inserir um valor literal em uma SQL Server PDW coluna de distribuição que usa um tipo numérico.  
  
### <a name="bit-data-type"></a>tipo de dados bit  
A tabela a seguir define os formatos e as regras aceitas para inserir valores literais em uma coluna de distribuição do tipo **bit**. Uma cadeia de caracteres vazia (' ') ou uma cadeia de caracteres que contém somente espaços em branco (' ') é convertida em 0.  
  
|Tipo literal|format|Regras de conversão|  
|----------------|----------|--------------------|  
|Literal de cadeia de caracteres no formato **inteiro**|'nnnnnnnnnn'<br /><br />Exemplo: ' 1 ' ou ' 321 '|Um valor inteiro formatado como um literal de cadeia de caracteres não pode conter um valor negativo. Por exemplo, o valor '-123 ' gera um erro.<br /><br />Um valor maior que 1 é convertido em 1. Por exemplo, o valor ' 123 ' é convertido em 1.|  
|Cadeia de caracteres literal|' TRUE ' ou ' FALSE '<br /><br />Exemplo: ' true '|O valor ' TRUE ' é convertido em 1; o valor ' FALSE ' é convertido em 0.|  
|Literal inteiro|nnnnnnnn<br /><br />Exemplo: 1 ou 321|Um valor maior que 1 ou menor que 0 é convertido em 1. Por exemplo, os valores 123 e-123 são convertidos em 1.|  
|Literal decimal|NNNNN. nnnn<br /><br />Exemplo: 1234,5678|Um valor maior que 1 ou menor que 0 é convertido em 1. Por exemplo, os valores 123,45 e-123,45 são convertidos em 1.|  
  
### <a name="decimal-data-type"></a>tipo de dados decimal  
A tabela a seguir define os formatos e as regras aceitas para inserir valores literais em uma coluna de distribuição do tipo **decimal** (*p, s*). As regras de conversão de dados são as mesmas para SQL Server. Para obter mais informações, consulte [conversão de tipo de dados](../t-sql/data-types/data-type-conversion-database-engine.md) no msdn.  
  
|Tipo literal|Formatar|  
|----------------|----------|  
|Literal de cadeia de caracteres no formato **inteiro**|'nnnnnnnnnnnn'<br /><br />Exemplo: ' 321312313123 '|  
|Literal de cadeia de caracteres no formato **decimal**|' nnnnnn. NNNNN '<br /><br />Exemplo: ' 123344,34455 '|  
|Literal inteiro|nnnnnnnnnnnn<br /><br />Exemplo: 321312313123|  
|Literal decimal|nnnnnn. NNNNN<br /><br />Exemplo: ' 123344,34455 '|  
  
### <a name="float-and-real-data-types"></a>tipos de dados float e real  
A tabela a seguir define os formatos e as regras aceitas para inserir valores literais em uma coluna de distribuição do tipo **float** ou **real**. As regras de conversão de dados são as mesmas para SQL Server. Para obter mais informações, consulte [conversão de tipo de dados](../t-sql/data-types/data-type-conversion-database-engine.md) no msdn.  
  
|Tipo literal|Formatar|  
|----------------|----------|  
|Literal de cadeia de caracteres no formato **inteiro**|'nnnnnnnnnnnn'<br /><br />Exemplo: ' 321312313123 '|  
|Literal de cadeia de caracteres no formato **decimal**|' nnnnnn. NNNNN '<br /><br />Exemplo: ' 123344,34455 '|  
|Literal de cadeia de caracteres no formato de **ponto flutuante**|' n. nnnnnE + NN '<br /><br />Exemplo: ' 3.12323 E + 14 '|  
|Literal inteiro|nnnnnnnnnnnn<br /><br />Exemplo: 321312313123|  
|Literal decimal|nnnnnn. NNNNN<br /><br />Exemplo: 123344,34455|  
|Literal de ponto flutuante|n. nnnnnE + nn<br /><br />Exemplo: 3.12323 E + 14|  
  
### <a name="int-bigint-tinyint-smallint-data-types"></a>tipos de dados int, bigint, tinyint, smallint  
A tabela a seguir define os formatos e as regras aceitas para inserir valores literais em uma coluna de distribuição do tipo **int**, **bigint**, **tinyint**ou **smallint**. A fonte de dados não pode exceder o intervalo permitido para o tipo de dados fornecido. Por exemplo, o intervalo de **tinyint** é de 0 a 255 e o intervalo para **int** é-2.147.483.648 a 2.147.483.647.  
  
|Tipo de literal|Formatar|Regras de conversão|  
|------------|------|----------------|
|Literal de cadeia de caracteres no formato **inteiro**|'nnnnnnnnnnnnnn'<br /><br />Exemplo: ' 321312313123 '| Nenhum |  
|Literal inteiro|nnnnnnnnnnnnnn<br /><br />Exemplo: 321312313123| Nenhum|  
|Literal decimal|nnnnnn. NNNNN<br /><br />Exemplo: 123344,34455|Os valores à direita do ponto decimal são truncados.|  
  
### <a name="money-and-smallmoney-data-types"></a>tipos de dados Money e smallmoney  
Os valores literais de Money são representados como números com um ponto decimal opcional e um símbolo de moeda como um prefixo. A fonte de dados não pode exceder o intervalo permitido para o tipo de dados fornecido. Por exemplo, o intervalo para **smallmoney** é de-214748,3648 a 214748,3647 e o intervalo para **money** é-922337203685477,5808 a 922337203685477,5807. A tabela a seguir define os formatos e as regras aceitas para inserir valores literais em uma coluna de distribuição do tipo **Money** ou **smallmoney**.  
  
|Tipo literal|Formatar|Regras de conversão|  
|----------------|----------|--------------------|  
|Literal de cadeia de caracteres no formato **inteiro**|nnnnnnnn<br /><br />Exemplo: ' 123433 '|Os dígitos ausentes após o ponto decimal são definidos como 0 quando o valor é inserido. Por exemplo, o literal ' 12345 ' é inserido como 12345, 0.|  
|Literal de cadeia de caracteres no formato **decimal**|' nnnnnn. NNNNN '<br /><br />Exemplo: ' 123344,34455 '|Se o número de dígitos após o ponto decimal exceder 4, o valor será arredondado para o valor mais próximo. Por exemplo, o valor ' 123344,34455 ' é inserido como 123344,3446.|  
|Literal de cadeia de caracteres no formato **Money**|' $nnnnnn. nnnn '<br /><br />Exemplo: ' $123456.7890 '|O símbolo de moeda opcional não é inserido com o valor.<br /><br />Se o número de dígitos após o ponto decimal exceder 4, o valor será arredondado para o valor mais próximo.|  
|Literal inteiro|nnnnnnnn<br /><br />Exemplo: 123433|Os dígitos ausentes após o ponto decimal são definidos como 0 quando o valor é inserido. Por exemplo, o literal 12345 é inserido como 12345, 0.|  
|Literal decimal|nnnnnn. NNNNN<br /><br />Exemplo: 123344,34455|Se o número de dígitos após o ponto decimal exceder 4, o valor será arredondado para o valor mais próximo. Por exemplo, o valor 123344,34455 é inserido como 123344,3446.|  
|Literal de dinheiro|$nnnnnn. nnnn<br /><br />Exemplo: $123456.7890|O símbolo de moeda opcional não é inserido com o valor.<br /><br />Se o número de dígitos após o ponto decimal exceder 4, o valor será arredondado para o valor mais próximo.|  
  
## <a name="inserting-literals-into-string-types"></a><a name="InsertLiteralsString"></a>Inserindo literais em tipos de cadeia de caracteres  
As tabelas a seguir definem os formatos aceitos e as regras de conversão para inserir um valor literal em uma SQL Server PDW coluna que usa um tipo de cadeia de caracteres.  
  
### <a name="char-varchar-nchar-and-nvarchar-data-types"></a>tipos de dados char, varchar, nchar e nvarchar  
A tabela a seguir define os formatos e as regras aceitas para inserir valores literais em uma coluna de distribuição do tipo **Char**, **varchar**, **nchar** e **nvarchar**. O comprimento da fonte de dados não pode exceder o tamanho especificado para o tipo de dados. Se o comprimento da fonte de dados for menor que o tamanho do tipo de dados **Char** ou **nchar** , os dados serão preenchidos à direita com espaços em branco para alcançar o tamanho do tipo de dados.  
  
|Tipo de literal|Formatar|Regras de conversão|  
|----------------|----------|--------------------|  
|Cadeia de caracteres literal|Formato: ' cadeia de caracteres '<br /><br />Exemplo: ' abc '| Nenhum|  
|Literal de cadeia de caracteres Unicode|Formato: cadeia de caracteres N'character '<br /><br />Exemplo: N'abc '|  Nenhum |  
|Literal inteiro|Formato: nnnnnnnnnnn<br /><br />Exemplo: 321312313123| Nenhum |  
|Literal decimal|Formato: nnnnnn. nnnnnnn<br /><br />Exemplo: 12344,34455| Nenhum |  
|Literal de dinheiro|Formato: $nnnnnn. NNNNN<br /><br />Exemplo: $123456.99|O símbolo de moeda não é inserido com o valor. Para inserir o símbolo de moeda, insira o valor como um literal de cadeia de caracteres. Isso corresponderá ao formato da ferramenta **dwloader** , que trata cada literal como um literal de cadeia de caracteres.<br /><br />Não são permitidas vírgulas.<br /><br />Se o número de dígitos após o ponto decimal exceder 2, o valor será arredondado para o valor mais próximo. Por exemplo, o valor 123,946789 é inserido como 123,95.<br /><br />Somente o estilo padrão 0 (sem vírgulas e 2 dígitos após o ponto decimal) é permitido ao usar a função CONVERT para inserir literais monetários.|  

  
## <a name="see-also"></a>Consulte Também  
 
[Dados distribuídos](/azure/synapse-analytics/sql-data-warehouse/massively-parallel-processing-mpp-architecture)  
[INSERT](../t-sql/statements/insert-transact-sql.md)  
  
<!-- MISSING LINKS
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Metadata query examples](metadata-query-examples.md) 
-->