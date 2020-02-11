---
title: Regras de conversão de tipo de dados Dwloader
description: Este tópico descreve os formatos de dados de entrada e as conversões implícitas de tipo de dados que o carregador de linha de comando dwloader dá suporte ao carregar dados em Parallel data warehouse (PDW). "
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: fe5d8790b5adb8477c994d265f458cdb1ceda61a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401186"
---
# <a name="data-type-conversion-rules-for-dwloader---parallel-data-warehouse"></a>Regras de conversão de tipo de dados para data warehouse dwloader paralelos
Este tópico descreve os formatos de dados de entrada e as conversões implícitas de tipo de dados que o [carregador de linha de comando dwloader](dwloader.md) dá suporte ao carregar dados no PDW. As conversões de dados implícitas ocorrem quando os dados de entrada não correspondem ao tipo de dados na tabela de destino SQL Server PDW. Use essas informações ao criar seu processo de carregamento para garantir que os dados serão carregados com êxito no SQL Server PDW.  
   
  
## <a name="InsertBinaryTypes"></a>Inserindo literais em tipos binários  
A tabela a seguir define os tipos literais, o formato e as regras de conversão aceitos para carregar um valor literal em uma coluna SQL Server PDW do tipo **Binary** (*n*) ou **varbinary**(*n*).  
  
|Tipo de dados de entrada|Exemplos de dados de entrada|Conversão para tipo de dados binary ou varbinary|  
|-------------------|-----------------------|-----------------------------------------------|  
|Literal binário|0x *hexidecimal_string*<br /><br />Exemplo: 12Ef ou 0x12Ef|O prefixo 0x é opcional.<br /><br />O comprimento da fonte de dados não pode exceder o número de bytes especificados para o tipo de dados.<br /><br />Se o comprimento da fonte de dados for menor que o tamanho do tipo de dados **Binary** , os dados serão preenchidos à direita com zeros para alcançar o tamanho do tipo de dados.|  
  
## <a name="InsertDateTimeTypes"></a>Inserindo literais em tipos de data e hora  
Os literais de data e hora são representados usando literais de cadeia de caracteres em formatos específicos, entre aspas simples. As tabelas a seguir definem os tipos literais permitidos, o formato e as regras de conversão para carregar um literal de data ou hora em uma coluna do tipo **DateTime**, **smalldatetime**, **Date**, **time**, **DateTimeOffset**ou **datetime2**. As tabelas definem o formato padrão para o tipo de dados fornecido. Outros formatos que podem ser especificados são definidos na seção [formatos de data e hora](#DateFormats). Os literais de data e hora não podem incluir espaços à esquerda ou à direita. os valores **Date**, **smalldatetime**e NULL não podem ser carregados no modo de largura fixa.  
  
### <a name="datetime-data-type"></a>Tipo de dados datetime  
A tabela a seguir define o formato padrão e as regras para carregar valores literais em uma coluna do tipo **DateTime**. Uma cadeia de caracteres vazia (' ') é convertida para o valor padrão ' 1900-01-01 12:00:00.000 '. Cadeias de caracteres que contêm apenas espaços em branco (' ') geram um erro.  
  
|Tipo de dados de entrada|Exemplos de dados de entrada|Conversão para tipo de dados DateTime|  
|-------------------|-----------------------|------------------------------------|  
|Literal de cadeia de caracteres no formato **DateTime**|' AAAA-MM-DD hh: mm: SS [. FFF] '<br /><br />Exemplo: ' 2007-05-08 12:35:29.123 '|Os dígitos fracionários ausentes são definidos como 0 quando o valor é inserido. Por exemplo, o literal ' 2007-05-08 12:35 ' é inserido como ' 2007-05-08 12:35:00.000 '.|  
|Literal de cadeia de caracteres no formato **smalldatetime**|' AAAA-MM-DD hh: mm '<br /><br />Exemplo: ' 2007-05-08 12:35 '|Segundos e dígitos fracionários restantes são definidos como 0 quando o valor é inserido.|  
|Literal de cadeia de caracteres no formato de **Data**|' AAAA-MM-DD '<br /><br />Exemplo: ' 2007-05-08 '|Os valores de hora (hora, minutos, segundos e frações) são definidos como 12:00:00.000 quando o valor é inserido.|  
|Literal de cadeia de caracteres no formato **datetime2**|' AAAA-MM-DD hh: mm: SS. fffffff '<br /><br />Exemplo: ' 2007-05-08 12:35:29.1234567 '|Os dados de origem não podem exceder três dígitos fracionários. Por exemplo, o literal ' 2007-05-08 12:35:29.123 ' será inserido, mas o valor ' 2007-05-8 12:35:29.1234567 ' gerará um erro.|  
  
### <a name="smalldatetime-data-type"></a>Tipo de dados smalldatetime  
A tabela a seguir define o formato padrão e as regras para carregar valores literais em uma coluna do tipo **smalldatetime**. Uma cadeia de caracteres vazia (' ') é convertida para o valor padrão ' 1900-01-01 12:00 '. Cadeias de caracteres que contêm apenas espaços em branco (' ') geram um erro.  
  
|Tipo de dados de entrada|Exemplos de dados de entrada|Conversão para tipo de dados smalldatetime|  
|-------------------|-----------------------|-----------------------------------------|  
|Literal de cadeia de caracteres no formato **smalldatetime**|' AAAA-MM-DD hh: mm ' ou ' AAAA-MM-DD hh: mm: SS '<br /><br />Exemplo: ' 2007-05-08 12:00 ' ou ' 2007-05-08 12:00:15 '|Os dados de origem devem ter valores para ano, mês, data, hora e minuto. Segundos são opcionais e, se presentes, devem ser definidos com o valor 00. Qualquer outro valor gera um erro.<br /><br />Segundos são opcionais. Ao carregar em uma coluna smalldatetime, dwloader arredondará segundos e segundos fracionários. Por exemplo, 1999-01-05 20:10:35.123 será carregado como 01-05 20:11.|  
|Literal de cadeia de caracteres no formato de **Data**|' AAAA-MM-DD '<br /><br />Exemplo: ' 2007-05-08 '|Os valores de hora (hora, minutos, segundos e frações) são definidos como 0 quando o valor é inserido.|  
  
### <a name="date-data-type"></a>Tipo de dados de data  
A tabela a seguir define o formato padrão e as regras para carregar valores literais em uma coluna do tipo **Date**. Uma cadeia de caracteres vazia (' ') é convertida para o valor padrão ' 1900-01-01 '. Cadeias de caracteres que contêm apenas espaços em branco (' ') geram um erro.  
  
|Tipo de dados de entrada|Exemplos de dados de entrada|Conversão para tipo de dados de data|  
|-------------------|-----------------------|--------------------------------|  
|Literal de cadeia de caracteres no formato de **Data**|' AAAA-MM-DD '<br /><br />Exemplo: ' 2007-05-08 '||  
  
### <a name="time-data-type"></a>Tipo de dados time  
A tabela a seguir define o formato padrão e as regras para carregar valores literais em uma coluna do tipo **time**. Uma cadeia de caracteres vazia (' ') é convertida para o valor padrão ' 00:00:00.0000 '. Cadeias de caracteres que contêm apenas espaços em branco (' ') geram um erro.  
  
|Tipo de dados de entrada|Exemplos de dados de entrada|Conversão para tipo de dados de hora|  
|-------------------|-----------------------|--------------------------------|  
|Literal de cadeia de caracteres no formato de **hora**|' hh: mm: SS. fffffff '<br /><br />Exemplo: ' 12:35:29.1234567 '|Se a fonte de dados tiver uma precisão menor ou igual (número de dígitos fracionários) do que a precisão do tipo de dados de **tempo** , os dados serão preenchidos à direita com zeros. Por exemplo, um valor literal ' 12:35:29.123 ' é inserido como ' 12:35:29.1230000 '.|  
  
### <a name="datetimeoffset-data-type"></a>Tipo de dados DateTimeOffset  
A tabela a seguir define o formato padrão e as regras para carregar valores literais em uma coluna do tipo **DateTimeOffset** (*n*). O formato padrão é ' AAAA-MM-DD hh: mm: SS. fffffff {+ |-} hh: mm '. Uma cadeia de caracteres vazia (' ') é convertida para o valor padrão ' 1900-01-01 12:00:00.0000000 + 00:00 '. Cadeias de caracteres que contêm apenas espaços em branco (' ') geram um erro. O número de dígitos fracionários depende da definição de coluna. Por exemplo, uma coluna definida como **DateTimeOffset** (2) terá dois dígitos fracionários.  
  
|Tipo de dados de entrada|Exemplos de dados de entrada|Conversão para o tipo de dados DateTimeOffset|  
|-------------------|-----------------------|------------------------------------------|  
|Literal de cadeia de caracteres no formato **DateTime**|' AAAA-MM-DD hh: mm: SS [. FFF] '<br /><br />Exemplo: ' 2007-05-08 12:35:29.123 '|Dígitos fracionários e valores de deslocamento ausentes são definidos como 0 quando o valor é inserido. Por exemplo, o literal ' 2007-05-08 12:35:29.123 ' é inserido como ' 2007-05-08 12:35:29.1230000 + 00:00 '.|  
|Literal de cadeia de caracteres no formato **smalldatetime**|' AAAA-MM-DD hh: mm '<br /><br />Exemplo: ' 2007-05-08 12:35 '|Segundos, os dígitos fracionários restantes e os valores de deslocamento são definidos como 0 quando o valor é inserido.|  
|Literal de cadeia de caracteres no formato de **Data**|' AAAA-MM-DD '<br /><br />Exemplo: ' 2007-05-08 '|Os valores de hora (hora, minutos, segundos e frações) são definidos como 0 quando o valor é inserido. Por exemplo, o literal ' 2007-05-08 ' é inserido como ' 2007-05-08 00:00:00.0000000 + 00:00 '.|  
|Literal de cadeia de caracteres no formato **datetime2**|' AAAA-MM-DD hh: mm: SS. fffffff '<br /><br />Exemplo: ' 2007-05-08 12:35:29.1234567 '|Os dados de origem não podem exceder o número especificado de segundos fracionários na coluna DateTimeOffset. Se a fonte de dados tiver um número menor ou igual de segundos fracionários, os dados serão preenchidos à direita com zeros. Por exemplo, se o tipo de dados for DateTimeOffset (5), o valor literal ' 2007-05-08 12:35:29.123 + 12:15 ' será inserido como ' 12:35:29.12300 + 12:15 '.|  
|Literal de cadeia de caracteres no formato **DateTimeOffset**|' AAAA-MM-DD hh: mm: SS. fffffff {+&#124;-} hh: mm '<br /><br />Exemplo: ' 2007-05-08 12:35:29.1234567 + 12:15 '|Os dados de origem não podem exceder o número especificado de segundos fracionários na coluna DateTimeOffset. Se a fonte de dados tiver um número menor ou igual de segundos fracionários, os dados serão preenchidos à direita com zeros. Por exemplo, se o tipo de dados for DateTimeOffset (5), o valor literal ' 2007-05-08 12:35:29.123 + 12:15 ' será inserido como ' 12:35:29.12300 + 12:15 '.|  
  
### <a name="datetime2-data-type"></a>Tipo de dados datetime2  
A tabela a seguir define o formato padrão e as regras para carregar valores literais em uma coluna do tipo **datetime2** (*n*). O formato padrão é ' AAAA-MM-DD hh: mm: SS. fffffff '. Uma cadeia de caracteres vazia (' ') é convertida para o valor padrão ' 1900-01-01 12:00:00 '. Cadeias de caracteres que contêm apenas espaços em branco (' ') geram um erro. O número de dígitos fracionários depende da definição de coluna. Por exemplo, uma coluna definida como **datetime2** (2) terá dois dígitos fracionários.  
  
|Tipo de dados de entrada|Exemplos de dados de entrada|Conversão para tipo de dados datetime2|  
|-------------------|-----------------------|-------------------------------------|  
|Literal de cadeia de caracteres no formato **DateTime**|' AAAA-MM-DD hh: mm: SS [. FFF] '<br /><br />Exemplo: ' 2007-05-08 12:35:29.123 '|Os segundos fracionários são opcionais e são definidos como 0 quando o valor é inserido.|  
|Literal de cadeia de caracteres no formato **smalldatetime**|' AAAA-MM-DD hh: mm '<br /><br />Exemplo: ' 2007-05-08 12 '|Os segundos opcionais e os dígitos fracionários restantes são definidos como 0 quando o valor é inserido.|  
|Literal de cadeia de caracteres no formato de **Data**|' AAAA-MM-DD '<br /><br />Exemplo: ' 2007-05-08 '|Os valores de hora (hora, minutos, segundos e frações) são definidos como 0 quando o valor é inserido. Por exemplo, o literal ' 2007-05-08 ' é inserido como ' 2007-05-08 12:00:00.0000000 '.|  
|Literal de cadeia de caracteres no formato **datetime2**|' AAAA-MM-DD hh: mm: SS: fffffff '<br /><br />Exemplo: ' 2007-05-08 12:35:29.1234567 '|Se a fonte de dados contiver componentes de dados e de tempo menores ou iguais ao valor especificado em **datetime2**(*n*), os dados serão inseridos; caso contrário, um erro será gerado.|  
  
### <a name="DateFormats"></a>Formatos DateTime  
O Dwloader dá suporte aos seguintes formatos de dados para os dados de entrada que estão sendo carregados no SQL Server PDW. Mais detalhes são listados após a tabela.  
  
|DATETIME|smalldatetime|date|datetime2|datetimeoffset|  
|------------|-----------------|--------|-------------|------------------|  
|[M[M]]M-[d]d-[yy]yy HH:mm:ss[.fff]|[M[M]]M-[d]d-[aa]aa HH:mm[:00]|[M[M]]M-[d]d-[aa]aa|[M[M]]M-[d]d-[aa]aa HH:mm:ss[.fffffff]|[M[M]]M-[d]d-[aa]aa HH:mm:ss[.fffffff] zzz|  
|[M[M]]M-[d]d-[aa]aa hh:mm:ss[.fff][tt]|[M[M]]M-[d]d-[aa]aa hh:mm[:00][tt]||[M[M]]M-[d]d-[aa]aa hh:mm:ss[.fffffff][tt]|[M[M]]M-[d]d-[aa]aa hh:mm:ss[.fffffff][tt] zzz|  
|[M[M]]M-[yy]yy-[d]d HH:mm:ss[.fff]|[M[M]]M-[yy]yy-[d]d HH:mm[:00]|[M[M]]M-[yy]yy-[d]d|[M[M]]M-[yy]yy-[d]d HH:mm:ss[.fffffff]|[M[M]]M-[aa]aa-[d]d HH:mm:ss[.fffffff] zzz|  
|[M[M]]M-[aa]aa-[d]d hh:mm:ss[.fff][tt]|[M[M]]M-[aa]aa-[d]d hh:mm[:00][tt]||[M[M]]M-[aa]aa-[d]d hh:mm:ss[.fffffff][tt]|[M[M]]M-[aa]aa-[d]d hh:mm:ss[.fffffff][tt] zzz|  
|[yy]yy-[M[M]]M-[d]d HH:mm:ss[.fff]|[yy]yy-[M[M]]M-[d]d HH:mm[:00]|[yy]yy-[M[M]]M-[d]d|[yy]yy-[M[M]]M-[d]d HH:mm:ss[.fffffff]|[aa]aa-[M[M]]M-[d]d HH:mm:ss[.fffffff] zzz|  
|[aa]aa-[M[M]]M-[d]d hh:mm:ss[.fff][tt]|[aa]aa-[M[M]]M-[d]d hh:mm[:00][tt]||[aa]aa-[M[M]]M-[d]d hh:mm:ss[.fffffff][tt]|[aa]aa-[M[M]]M-[d]d hh:mm:ss[.fffffff][tt] zzz|  
|[yy]yy-[d]d-[M[M]]M HH:mm:ss[.fff]|[aa]aa-[d]d-[M[M]]M HH:mm[:00]|[yy]yy-[d]d-[M[M]]M|[aa]aa-[d]d-[M[M]]M HH:mm:ss[.fffffff]|[aa]aa-[d]d-[M[M]]M HH:mm:ss[.fffffff] zzz|  
|[aa]aa-[d]d-[M[M]]M hh:mm:ss[.fff][tt]|[aa]aa-[d]d-[M[M]]M hh:mm[:00][tt]||[aa]aa-[d]d-[M[M]]M hh:mm:ss[.fffffff][tt]|[aa]aa-[d]d-[M[M]]M hh:mm:ss[.fffffff][tt] zzz|  
|[d]d-[M[M]]M-[aa]aa HH:mm:ss[.fff]|[d]d-[M[M]]M-[aa]aa HH:mm[:00]|[d]d-[M[M]]M-[aa]aa|[d]d-[M[M]]M-[aa]aa HH:mm:ss[.fffffff]|[d]d-[M[M]]M-[aa]aa HH:mm:ss[.fffffff] zzz|  
|[d]d-[M[M]]M-[aa]aa hh:mm:ss[.fff][tt]|[d]d-[M[M]]M-[aa]aa hh:mm[:00][tt]||[d]d-[M[M]]M-[aa]aa hh:mm:ss[.fffffff][tt]|[d]d-[M[M]]M-[aa]aa hh:mm:ss[.fffffff][tt] zzz|  
|[d]d-[yy]yy-[M[M]]M HH:mm:ss[.fff]|[d]d-[aa]aa-[M[M]]M HH:mm[:00]|[d]d-[yy]yy-[M[M]]M|[d]d-[yy]yy-[M[M]]M HH:mm:ss[.fffffff]|[d]d-[aa]aa-[M[M]]M HH:mm:ss[.fffffff] zzz|  
|[d]d-[aa]aa-[M[M]]M hh:mm:ss[.fff][tt]|[d]d-[aa]aa-[M[M]]M hh:mm[:00][tt]||[d]d-[aa]aa-[M[M]]M hh:mm:ss[.fffffff][tt]|[d]d-[aa]aa-[M[M]]M hh:mm:ss[.fffffff][tt] zzz|  
  
Detalhes:  
  
-   Para separar os valores de mês, dia e ano, você pode usar '-', '/' ou '. '. Para simplificar, a tabela use apenas o separador ‘-’.  
  
-   Para especificar o mês como texto, use três ou mais caracteres. Meses com 1 ou 2 caracteres serão interpretados como um número.  
  
-   Para separar valores de tempo, use o símbolo ': '.  
  
-   As letras entre colchetes são opcionais.  
  
-   As letras 'tt' designam [AM|PM|am|pm]. AM é o padrão. Quando 'tt' for especificado, o valor de hora (hh) precisará estar no intervalo de 0 a 12.  
  
-   As letras 'zzz' designam a diferença do fuso horário atual do sistema no formato {+|-}HH:ss].  
  
## <a name="InsertNumerictypes"></a>Inserindo literais em tipos numéricos  
As tabelas a seguir definem o formato padrão e as regras de conversão para carregar um valor literal em uma SQL Server PDW coluna que usa um tipo numérico.  
  
### <a name="bit-data-type"></a>Tipo de dados bit  
A tabela a seguir define o formato padrão e as regras para carregar valores literais em uma coluna do tipo **bit**. Uma cadeia de caracteres vazia (' ') ou uma cadeia de caracteres que contém somente espaços em branco (' ') é convertida em 0.  
  
|Tipo de dados de entrada|Exemplos de dados de entrada|Conversão para tipo de dados bit|  
|-------------------|-----------------------|-------------------------------|  
|Literal de cadeia de caracteres no formato **inteiro**|'ffffffffff'<br /><br />Exemplo: ' 1 ' ou ' 321 '|Um valor inteiro formatado como um literal de cadeia de caracteres não pode conter um valor negativo. Por exemplo, o valor '-123 ' gera um erro.<br /><br />Um valor maior que 1 é convertido em 1. Por exemplo, o valor ' 123 ' é convertido em 1.|  
|Literal de cadeia de caracteres|' TRUE ' ou ' FALSE '<br /><br />Exemplo: ' true '|O valor ' TRUE ' é convertido em 1; o valor ' FALSE ' é convertido em 0.|  
|Literal inteiro|fffffffn<br /><br />Exemplo: 1 ou 321|Um valor maior que 1 ou menor que 0 é convertido em 1. Por exemplo, os valores 123 e-123 são convertidos em 1.|  
|Literal decimal|fffnn.fffn<br /><br />Exemplo: 1234,5678|Um valor maior que 1 ou menor que 0 é convertido em 1. Por exemplo, os valores 123,45 e-123,45 são convertidos em 1.|  
  
### <a name="decimal-data-type"></a>Tipo de dados decimal  
A tabela a seguir define as regras para carregar valores literais em uma coluna do tipo **decimal** (*p, s*). As regras de conversão de dados são as mesmas para SQL Server. Para obter mais informações, consulte [conversão de tipo de dados (mecanismo de banco de dados)](https://go.microsoft.com/fwlink/?LinkId=202128) no msdn.  
  
|Tipo de dados de entrada|Exemplos de dados de entrada|  
|-------------------|-----------------------|  
|Literal inteiro|321312313123|  
|Literal decimal|123344,34455|  
  
### <a name="float-and-real-data-types"></a>Tipos de dados float e real  
A tabela a seguir define as regras para carregar valores literais em uma coluna do tipo **float** ou **real**. As regras de conversão de dados são as mesmas para SQL Server. Para obter mais informações, consulte [conversão de tipo de dados (mecanismo de banco de dados)](../t-sql/data-types/data-type-conversion-database-engine.md) no msdn.  
  
|Tipo de dados de entrada|Exemplos de dados de entrada|  
|-------------------|-----------------------|  
|Literal inteiro|321312313123|  
|Literal decimal|123344,34455|  
|Literal de ponto flutuante|3.12323 e + 14|  
  
### <a name="int-bigint-tinyint-smallint-data-types"></a>Tipos de dados int, bigint, tinyint, smallint  
A tabela a seguir define as regras para carregar valores literais em uma coluna do tipo **int**, **bigint**, **tinyint**ou **smallint**. A fonte de dados não pode exceder o intervalo permitido para o tipo de dados fornecido. Por exemplo, o intervalo de **tinyint** é de 0 a 255 e o intervalo para **int** é-2.147.483.648 a 2.147.483.647.  
  
|Tipo de dados de entrada|Exemplos de dados de entrada|Conversão para tipos de dados inteiros|  
|-------------------|-----------------------|------------------------------------|  
|Literal inteiro|321312313123||  
|Literal decimal|123344,34455|Os valores à direita do ponto decimal são truncados.|  
  
### <a name="money-and-smallmoney-data-types"></a>Tipos de dados Money e smallmoney  
Os valores literais de Money são representados como uma cadeia de números com um ponto decimal opcional e um símbolo de moeda opcional como um prefixo. A fonte de dados não pode exceder o intervalo permitido para o tipo de dados fornecido. Por exemplo, o intervalo para **smallmoney** é de-214748,3648 a 214748,3647 e o intervalo para **money** é-922337203685477,5808 a 922337203685477,5807. A tabela a seguir define as regras para carregar valores literais em uma coluna do tipo **Money** ou **smallmoney**.  
  
|Tipo de dados de entrada|Exemplos de dados de entrada|Conversão para tipo de dados money ou smallmoney|  
|-------------------|-----------------------|-----------------------------------------------|  
|Literal inteiro|321312|Os dígitos ausentes após o ponto decimal são definidos como 0 quando o valor é inserido. Por exemplo, o literal 12345 é inserido como 12345, 0|  
|Literal decimal|123344,34455|Se o número de dígitos após o ponto decimal exceder 4, o valor será arredondado para o valor mais próximo. Por exemplo, o valor 123344,34455 é inserido como 123344,3446.|  
|Literal de dinheiro|$123456.7890|O símbolo de moeda não é inserido com o valor.<br /><br />Se o número de dígitos após o ponto decimal exceder 4, o valor será arredondado para o valor mais próximo.|  
  
## <a name="InsertStringTypes"></a>Inserindo literais em tipos de cadeia de caracteres  
As tabelas a seguir definem o formato padrão e as regras de conversão para carregar um valor literal em uma SQL Server PDW coluna que usa um tipo de cadeia de caracteres.  
  
### <a name="char-varchar-nchar-and-nvarchar-data-types"></a>Tipos de dados char, varchar, nchar e nvarchar  
A tabela a seguir define o formato padrão e as regras para carregar valores literais em uma coluna do tipo **Char**, **varchar**, **nchar** e **nvarchar**. O comprimento da fonte de dados não pode exceder o tamanho especificado para o tipo de dados. Se o comprimento da fonte de dados for menor que o tamanho do tipo de dados **Char** ou **nchar** , os dados serão preenchidos à direita com espaços em branco para alcançar o tamanho do tipo de dados.  
  
|Tipo de dados de entrada|Exemplos de dados de entrada|Conversão para tipos de dados de caractere|  
|---------------|-------------------|----------------------------------|  
|Literal de cadeia de caracteres|Formato: ' cadeia de caracteres '<br /><br />Exemplo: ' abc '| NA |  
|Literal de cadeia de caracteres Unicode|Formato: cadeia de caracteres N'character '<br /><br />Exemplo: N'abc '| NA |  
|Literal inteiro|Formato: ffffffffffn<br /><br />Exemplo: 321312313123| NA |  
|Literal decimal|Formato: FFFFFF. fffffff<br /><br />Exemplo: 12344,34455| NA |  
|Literal de dinheiro|Formato: $ffffff. fffnn<br /><br />Exemplo: $123456.99|O símbolo de moeda opcional não é inserido com o valor. Para inserir o símbolo de moeda, insira o valor como um literal de cadeia de caracteres. Isso corresponderá ao formato do carregador, que trata cada literal como um literal de cadeia de caracteres.<br /><br />Não são permitidas vírgulas.<br /><br />Se o número de dígitos após o ponto decimal exceder 2, o valor será arredondado para o valor mais próximo. Por exemplo, o valor 123,946789 é inserido como 123,95.<br /><br />Somente o estilo padrão 0 (sem vírgulas e 2 dígitos após o ponto decimal) é permitido ao usar a função CONVERT para inserir literais monetários.|  
  
### <a name="general-remarks"></a>Comentários gerais  
o **dwloader** executa as mesmas conversões implícitas que o SMP SQL Server executa, mas não dá suporte a todas as conversões implícitas às quais o SMP SQL Server dá suporte.  
 
<!-- MISSING LINKS 
## See Also  
[Grant Permissions to Load Data &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-load-data-sql-server-pdw.md)  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  

-->
  
