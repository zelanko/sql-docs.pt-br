---
title: Carregar dados com INSERT - Parallel Data Warehouse | Microsoft Docs
description: Usando a instrução INSERT do T-SQL para carregar dados em um Parallel Data Warehouse (PDW) distribuído ou tabela replicada.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: b13daf2d32cc41d63deea6c612dde247d541e4d5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63128562"
---
# <a name="load-data-with-insert-into-parallel-data-warehouse"></a>Carregar dados com INSERT no Parallel Data Warehouse

Você pode usar a instrução de inserção de tsql para carregar dados em um SQL Server Parallel Data Warehouse (PDW) distribuído ou tabela replicada. Para obter mais informações sobre a inserção, consulte [inserir](../t-sql/statements/insert-transact-sql.md). Para tabelas replicadas e todas as colunas de distribuição não em uma tabela distribuída, o PDW usa o SQL Server para converter implicitamente os valores de dados especificados na instrução para o tipo de dados da coluna de destino. Para obter mais informações sobre regras de conversão de dados do SQL Server, consulte [dados de conversão de tipo para SQL](../t-sql/data-types/data-type-conversion-database-engine.md). No entanto, para colunas de distribuição, PDW dá suporte a apenas um subconjunto de conversões implícitas que dá suporte ao SQL Server. Portanto, quando você usa a instrução INSERT para carregar dados em uma coluna de distribuição, os dados de origem devem ser especificados em um dos formatos definidos nas tabelas a seguir.  
  
  
## <a name="InsertingLiteralsBinary"></a>Inserir literais em tipos binários  
A tabela a seguir define os tipos de literal aceitos, formato e regras de conversão para inserir um valor literal em uma coluna de distribuição do tipo **binário** (*n*) ou **varbinary** (*n*).  
  
|Tipo literal|Formatar|Regras de conversão|  
|----------------|----------|--------------------|  
|Literal binário|0x*hexidecimal_string*<br /><br />Exemplo: 0x12Ef|Literais binários devem ser prefixados com 0x.<br /><br />O tamanho da fonte de dados não pode exceder o número de bytes especificado para o tipo de dados.<br /><br />Se o tamanho da fonte de dados for menor que o tamanho do **binário** os dados de tipo de dados, serão preenchidos à direita com zeros para alcançar o tamanho do tipo de dados.|  
  
## <a name="InsertingLiteralsDateTime"></a>Inserir literais em tipos de data e hora  
Literais de data e hora são representadas usando valores de caractere em formatos específicos, incluídos entre aspas. As tabelas a seguir definem os tipos de literais permitidos, formato e regras de conversão para inserir uma data ou hora literal em uma coluna de distribuição do SQL Server PDW do tipo **datetime**, **smalldatetime**, **data**, **tempo**, **datetimeoffset**, ou **datetime2**.  
  
### <a name="datetime-data-type"></a>tipo de dados datetime  
A tabela a seguir define os formatos aceitos e regras para inserir valores literais em uma coluna de distribuição do tipo **datetime**. Qualquer cadeia de caracteres vazia (") é convertida para o valor padrão ' 1900-01-01 12:00:00.000'. Cadeias de caracteres que contém somente espaços em branco (' ') geram um erro.  
  
|Tipo literal|Formatar|Regras de conversão|  
|----------------|----------|--------------------|  
|Cadeia de caracteres literal no **datetime** formato|'AAAA-MM-DD HH: mm ss [. nnn]'<br /><br />Exemplo: '2007-05-08 12:35:29.123'|Ausente de dígitos fracionários são definidos como 0 quando o valor é inserido. Por exemplo, o literal ' 2007-05-08 12:35 ° será inserido como ' 2007-05-08 12:35:00.000'.|  
|Cadeia de caracteres literal no **smalldatetime** formato|'AAAA-MM-DD HH: mm'<br /><br />Exemplo: '2007-05-08 12:35'|Segundos e dígitos fracionários restantes são definidos como 0 quando o valor é inserido.|  
|Cadeia de caracteres literal no **data** formato|'AAAA-MM-DD'<br /><br />Exemplo: '2007-05-08'|Valores de tempo (horas, minutos, segundos e frações) são definidos como 12:00:00.000 quando o valor é inserido.|  
|Cadeia de caracteres literal no **datetime2** formato|'AAAA-MM-DD nnnnnnn'<br /><br />Exemplo: '2007-05-08 12:35:29.1234567'|Os dados de origem não podem exceder três dígitos fracionários. Por exemplo, o literal ' 2007-05-08 12:35:29.123' serão inseridos, mas o valor ' 12:35:29.1234567 2007-05-08' gera um erro.|  
  
### <a name="smalldatetime-data-type"></a>tipo de dados smalldatetime  
A tabela a seguir define os formatos aceitos e regras para inserir valores literais em uma coluna de distribuição do tipo **smalldatetime**. Qualquer cadeia de caracteres vazia (") é convertida para o valor padrão ' 1900-01-01 12:00". Cadeias de caracteres que contém somente espaços em branco (' ') geram um erro.  
  
|Tipo literal|Formatar|Regras de conversão|  
|----------------|----------|--------------------|  
|Cadeia de caracteres literal no **smalldatetime** formato|'AAAA-MM-DD HH: mm' ou 'AAAA-MM-DD hh:mm:00'<br /><br />Exemplo: ' 2007-05-08:00 a 12' ou ' 2007-05-08 12:00:00 '|Os dados de origem devem ter valores de ano, mês, data, hora e minuto. Segundos são opcionais e, se presente, devem ser definidos como o valor 00. Qualquer outro valor gera um erro.|  
|Cadeia de caracteres literal no **data** formato|'AAAA-MM-DD'<br /><br />Exemplo: '2007-05-08'|Valores de tempo (horas, minutos, segundos e frações) são definidos como 0 quando o valor é inserido.|  
  
### <a name="date-data-type"></a>Tipo de dados de data  
A tabela a seguir define os formatos aceitos e regras para inserir valores literais em uma coluna de distribuição do tipo **data**. Qualquer cadeia de caracteres vazia (") é convertida para o valor padrão ' 1900-01-01'. Cadeias de caracteres que contém somente espaços em branco (' ') geram um erro.  
  
|Tipo literal|Formatar|Regras de conversão|  
|----------------|----------|--------------------|  
|Cadeia de caracteres literal no **data** formato|'AAAA-MM-DD'<br /><br />Exemplo: '2007-05-08'|Isso é o único formato aceito.|  
  
### <a name="time-data-type"></a>tipo de dados de tempo  
A tabela a seguir define os formatos aceitos e regras para inserir valores literais em uma coluna de distribuição do tipo **tempo**. Qualquer cadeia de caracteres vazia (") é convertida para o valor padrão '00:00:00.0000'. Cadeias de caracteres que contém somente espaços em branco (' ') geram um erro.  
  
|Tipo literal|Formatar|Regras de conversão|  
|----------------|----------|--------------------|  
|Cadeia de caracteres literal no **tempo** formato|'hh:mm:ss.nnnnnnn'<br /><br />Exemplo: '12:35:29.1234567'|Se a fonte de dados tem uma precisão menor ou igual (número de dígitos fracionários) que a precisão de **tempo** os dados de tipo de dados, serão preenchidos à direita com zeros. Por exemplo, um valor literal '12:35:29.123' será inserido como '12:35:29.1230000'.<br /><br />Um valor que tem uma precisão maior do que o tipo de dados de destino será rejeitado.|  
  
### <a name="datetimeoffset-data-type"></a>tipo de dados DateTimeOffset  
A tabela a seguir define os formatos aceitos e regras para inserir valores literais em uma coluna de distribuição do tipo **datetimeoffset** (*n*). O formato padrão é ' AAAA-MM-DD nnnnnnn {+ |-} hh: mm '. Uma cadeia de caracteres vazia (") é convertida para o valor padrão ' 1900-01-01 12:00:00.0000000 + 00:00 '. Cadeias de caracteres que contém somente espaços em branco (' ') geram um erro. O número de dígitos fracionários depende da definição de coluna. Por exemplo, uma coluna definida como **datetimeoffset** (2) terá dois dígitos fracionários.  
  
|Tipo literal|Formatar|Regras de conversão|  
|----------------|----------|--------------------|  
|Cadeia de caracteres literal no **datetime** formato|'AAAA-MM-DD HH: mm ss [. nnn]'<br /><br />Exemplo: '2007-05-08 12:35:29.123'|Dígitos fracionários ausentes e valores de deslocamento é definido como 0 quando o valor é inserido. Por exemplo, o literal ' 2007-05-08 12:35:29.123' será inserido como ' 2007-05-08 12:35:29.1230000 + 00:00 '.|  
|Cadeia de caracteres literal no **smalldatetime** formato|'AAAA-MM-DD HH: mm'<br /><br />Exemplo: '2007-05-08 12:35'|Segundos, os dígitos fracionários restantes e valores de deslocamento é definido como 0 quando o valor é inserido.|  
|Cadeia de caracteres literal no **data** formato|'AAAA-MM-DD'<br /><br />Exemplo: '2007-05-08'|Valores de tempo (horas, minutos, segundos e frações) são definidos como 0 quando o valor é inserido. Por exemplo, o literal ' 2007-05-08' será inserido como ' 2007-05-08 00:00:00.0000000 + 00:00 '.|  
|Cadeia de caracteres literal no **datetime2** formato|'AAAA-MM-DD nnnnnnn'<br /><br />Exemplo: '2007-05-08 12:35:29.1234567'|Os dados de origem não podem exceder o número especificado de segundos fracionários na coluna de datetimeoffset. Se a fonte de dados tem um número igual ou menor de frações de segundo, os dados são preenchidos para a direita com zeros. Por exemplo, se o tipo de dados é datetimeoffset (5), o valor literal ' 2007-05-08 12:35:29.123 + 12:15 ' será inserido como ' 12:35:29.12300 + 12:15 '.|  
|Cadeia de caracteres literal no **datetimeoffset** formato|' AAAA-MM-DD nnnnnnn {+&#124;-} hh: mm '<br /><br />Exemplo: '2007-05-08 12:35:29.1234567 +12:15'|Os dados de origem não podem exceder o número especificado de segundos fracionários na coluna de datetimeoffset. Se a fonte de dados tem um número igual ou menor de frações de segundo, os dados são preenchidos para a direita com zeros. Por exemplo, se o tipo de dados é datetimeoffset (5), o valor literal ' 2007-05-08 12:35:29.123 + 12:15 ' será inserido como ' 12:35:29.12300 + 12:15 '.|  
  
### <a name="datetime2-data-type"></a>tipo de dados datetime2  
A tabela a seguir define os formatos aceitos e regras para inserir valores literais em uma coluna de distribuição do tipo **datetime2** (*n*). O formato padrão é 'AAAA-MM-DD nnnnnnn'. Uma cadeia de caracteres vazia (") é convertida para o valor padrão ' 1900-01-01 12:00:00". Cadeias de caracteres que contém somente espaços em branco (' ') geram um erro. O número de dígitos fracionários depende da definição de coluna. Por exemplo, uma coluna definida como **datetime2** (2) terá dois dígitos fracionários.  
  
|Tipo literal|Formatar|Regras de conversão|  
|----------------|----------|--------------------|  
|Cadeia de caracteres literal no **datetime** formato|'AAAA-MM-DD HH: mm ss [. nnn]'<br /><br />Exemplo: '2007-05-08 12:35:29.123'|Os segundos fracionários são opcionais e são definidos como 0 quando o valor é inserido.<br /><br />Um valor que tem mais dígitos fracionários que o tipo de dados de destino será rejeitado.|  
|Cadeia de caracteres literal no **smalldatetime** formato|'AAAA-MM-DD HH: mm'<br /><br />Exemplo: '2007-05-08 12'|Segundos opcionais e dígitos fracionários restantes são definidos como 0 quando o valor é inserido.|  
|Cadeia de caracteres literal no **data** formato|'AAAA-MM-DD'<br /><br />Exemplo: '2007-05-08'|Valores de tempo (horas, minutos, segundos e frações) são definidos como 0 quando o valor é inserido. Por exemplo, o literal ' 2007-05-08' será inserido como ' 2007-05-08 12:00:00.0000000'.|  
|Cadeia de caracteres literal no **datetime2** formato|'AAAA-MM-DD hh:mm:ss:nnnnnnn'<br /><br />Exemplo: '2007-05-08 12:35:29.1234567'|Se a fonte de dados contém os componentes de data e hora que são menor ou igual ao valor especificado na **datetime2**(*n*), os dados são inseridos; caso contrário, será gerado um erro.|  
  
## <a name="InsertLiteralsNumeric"></a>Inserir literais em tipos numéricos  
As tabelas a seguir definem os formatos aceitos e regras de conversão para inserir um valor literal em uma coluna de distribuição do SQL Server PDW que usa um tipo numérico.  
  
### <a name="bit-data-type"></a>tipo de dados bit  
A tabela a seguir define os formatos aceitos e regras para inserir valores literais em uma coluna de distribuição do tipo **bit**. Uma cadeia de caracteres vazia (") ou uma cadeia de caracteres que contém somente espaços em branco (' ') é convertido em 0.  
  
|Tipo literal|format|Regras de conversão|  
|----------------|----------|--------------------|  
|Cadeia de caracteres literal no **inteiro** formato|'nnnnnnnnnn'<br /><br />Exemplo: '1' ou '321'|Um valor inteiro formatado como uma cadeia de caracteres literal não pode conter um valor negativo. Por exemplo, o valor '-123' gera um erro.<br /><br />Um valor maior que 1 é convertido em 1. Por exemplo, o valor '123' é convertido em 1.|  
|Literal de cadeia de caracteres|'TRUE' ou 'FALSE'<br /><br />Exemplo: 'true'|O valor 'TRUE' é convertido em 1; o valor 'FALSE' é convertido em 0.|  
|Literal de inteiro|nnnnnnnn<br /><br />Exemplo: 1 ou 321|Um valor menor que 0 ou maior que 1 é convertido em 1. Por exemplo, os valores 123 e -123 são convertidos para 1.|  
|Literal decimal|nnnnn.nnnn<br /><br />Exemplo: 1234.5678|Um valor menor que 0 ou maior que 1 é convertido em 1. Por exemplo, os valores 123,45 e-123.45 são convertidos para 1.|  
  
### <a name="decimal-data-type"></a>tipo de dados decimal  
A tabela a seguir define os formatos aceitos e regras para inserir valores literais em uma coluna de distribuição do tipo **decimais** (*p, s*). As regras de conversão de dados são a mesma do SQL Server. Para obter mais informações, consulte [conversão de tipo de dados](../t-sql/data-types/data-type-conversion-database-engine.md) no MSDN.  
  
|Tipo literal|Formatar|  
|----------------|----------|  
|Cadeia de caracteres literal no **inteiro** formato|'nnnnnnnnnnnn'<br /><br />Exemplo: '321312313123'|  
|Cadeia de caracteres literal no **decimal** formato|'nnnnnn.nnnnn'<br /><br />Exemplo: '123344.34455'|  
|Literal de inteiro|nnnnnnnnnnnn<br /><br />Exemplo: 321312313123|  
|Literal decimal|nnnnnn.nnnnn<br /><br />Exemplo: '123344.34455'|  
  
### <a name="float-and-real-data-types"></a>tipos de dados float e real  
A tabela a seguir define os formatos aceitos e regras para inserir valores literais em uma coluna de distribuição do tipo **float** ou **real**. Regras de conversão de dados são a mesma do SQL Server. Para obter mais informações, consulte [conversão de tipo de dados](../t-sql/data-types/data-type-conversion-database-engine.md) no MSDN.  
  
|Tipo literal|Formatar|  
|----------------|----------|  
|Cadeia de caracteres literal no **inteiro** formato|'nnnnnnnnnnnn'<br /><br />Exemplo: '321312313123'|  
|Cadeia de caracteres literal no **decimal** formato|'nnnnnn.nnnnn'<br /><br />Exemplo: '123344.34455'|  
|Cadeia de caracteres literal no **de ponto flutuante** formato|'n.nnnnnE+nn'<br /><br />Exemplo: '3.12323E+14'|  
|Literal de inteiro|nnnnnnnnnnnn<br /><br />Exemplo: 321312313123|  
|Literal decimal|nnnnnn.nnnnn<br /><br />Exemplo: 123344.34455|  
|Literal de ponto flutuante|n.nnnnnE+nn<br /><br />Exemplo: 3.12323E + 14|  
  
### <a name="int-bigint-tinyint-smallint-data-types"></a>int, bigint, tinyint, smallint tipos de dados  
A tabela a seguir define os formatos aceitos e regras para inserir valores literais em uma coluna de distribuição do tipo **int**, **bigint**, **tinyint**, ou **smallint**. A fonte de dados não pode exceder o intervalo permitido para o tipo de dados fornecido. Por exemplo, o intervalo para **tinyint** é de 0 a 255 e o intervalo para **int** é de -2.147.483.648 a 2.147.483.647.  
  
|Tipo de literal|Formatar|Regras de conversão|  
|------------|------|----------------|
|Cadeia de caracteres literal no **inteiro** formato|'nnnnnnnnnnnnnn'<br /><br />Exemplo: '321312313123'| None |  
|Literal de inteiro|nnnnnnnnnnnnnn<br /><br />Exemplo: 321312313123| None|  
|Literal decimal|nnnnnn.nnnnn<br /><br />Exemplo: 123344.34455|Os valores para a direita da vírgula decimal são truncados.|  
  
### <a name="money-and-smallmoney-data-types"></a>tipos de dados Money e smallmoney  
Valores literais de dinheiro são representados como números com um ponto decimal opcional e o símbolo de moeda como um prefixo. A fonte de dados não pode exceder o intervalo permitido para o tipo de dados fornecido. Por exemplo, o intervalo para **smallmoney** é de -214.748,3648 a + 214.748,3647 e o intervalo para **money** é -922.337.203.685.477,5808 e 922.337.203.685.477,5807. A tabela a seguir define os formatos aceitos e regras para inserir valores literais em uma coluna de distribuição do tipo **dinheiro** ou **smallmoney**.  
  
|Tipo literal|Formatar|Regras de conversão|  
|----------------|----------|--------------------|  
|Cadeia de caracteres literal no **inteiro** formato|'nnnnnnnn'<br /><br />Exemplo: '123433'|Dígitos após o ponto decimal são definidos como 0 quando o valor é inserido. Por exemplo, o literal '12345' será inserido como 12345.0000.|  
|Cadeia de caracteres literal no **decimal** formato|'nnnnnn.nnnnn'<br /><br />Exemplo: '123344.34455'|Se o número de dígitos após o ponto decimal exceder 4, o valor é arredondado para o valor mais próximo. Por exemplo, o valor '123344.34455' será inserido como 123344.3446.|  
|Cadeia de caracteres literal no **dinheiro** formato|'$nnnnnn.nnnn'<br /><br />Exemplo: '$123456.7890'|O símbolo de moeda opcional não é inserido com o valor.<br /><br />Se o número de dígitos após o ponto decimal exceder 4, o valor é arredondado para o valor mais próximo.|  
|Literal de inteiro|nnnnnnnn<br /><br />Exemplo: 123433|Dígitos após o ponto decimal são definidos como 0 quando o valor é inserido. Por exemplo, o literal 12345 é inserido como 12345.0000.|  
|Literal decimal|nnnnnn.nnnnn<br /><br />Exemplo: 123344.34455|Se o número de dígitos após o ponto decimal exceder 4, o valor é arredondado para o valor mais próximo. Por exemplo, o valor 123344.34455 será inserido como 123344.3446.|  
|Literal de dinheiro|$nnnnnn.nnnn<br /><br />Exemplo: US $123456.7890|O símbolo de moeda opcional não é inserido com o valor.<br /><br />Se o número de dígitos após o ponto decimal exceder 4, o valor é arredondado para o valor mais próximo.|  
  
## <a name="InsertLiteralsString"></a>Inserindo literais em tipos de cadeia de caracteres  
As tabelas a seguir definem os formatos aceitos e regras de conversão para inserir um valor literal em uma coluna de PDW do SQL Server que usa um tipo de cadeia de caracteres.  
  
### <a name="char-varchar-nchar-and-nvarchar-data-types"></a>tipos de dados char, varchar, nchar e nvarchar  
A tabela a seguir define os formatos aceitos e regras para inserir valores literais em uma coluna de distribuição do tipo **char**, **varchar**, **nchar** e **nvarchar**. O tamanho da fonte de dados não pode exceder o tamanho especificado para o tipo de dados. Se o tamanho da fonte de dados for menor que o tamanho do **char** ou **nchar** os dados de tipo de dados, serão preenchidos à direita com espaços em branco para alcançar o tamanho do tipo de dados.  
  
|Tipo de literal|Formatar|Regras de conversão|  
|----------------|----------|--------------------|  
|Literal de cadeia de caracteres|Formato: 'cadeia de caracteres'<br /><br />Exemplo: 'abc'| None|  
|Literal de cadeia Unicode|Formato: Cadeia de caracteres N'character'<br /><br />Exemplo: N'abc'|  None |  
|Literal de inteiro|Formato: nnnnnnnnnnn<br /><br />Exemplo: 321312313123| None |  
|Literal decimal|Format: nnnnnn.nnnnnnn<br /><br />Exemplo: 12344.34455| None |  
|Literal de dinheiro|Formato: $nnnnnn.nnnnn<br /><br />Exemplo: US $123456.99|O símbolo de moeda não é inserido com o valor. Para inserir o símbolo de moeda, insira o valor como um literal de cadeia de caracteres. Isso irá corresponder ao formato do **dwloader** ferramenta, que trata toda literal como um literal de cadeia de caracteres.<br /><br />Vírgulas não são permitidas.<br /><br />Se o número de dígitos após o ponto decimal exceder 2, o valor é arredondado para o valor mais próximo. Por exemplo, o valor 123.946789 será inserido como 123.95.<br /><br />Somente o estilo padrão 0 (sem vírgulas e 2 dígitos após o ponto decimal) é permitido ao usar a função CONVERT para inserir os literais de dinheiro.|  

  
## <a name="see-also"></a>Consulte também  
 
[Dados distribuídos](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-distributed-data/)  
[INSERT](../t-sql/statements/insert-transact-sql.md)  
  
<!-- MISSING LINKS
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Metadata query examples](metadata-query-examples.md) 
-->
