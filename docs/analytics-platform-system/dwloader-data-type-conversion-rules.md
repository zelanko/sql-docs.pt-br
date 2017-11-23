---
title: "Regras de dwloader conversão de tipo de dados"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "Este tópico descreve os formatos de dados de entrada e conversões de tipo de dados implícitos que dwloader carregador de linha de comando dá suporte a quando ele carrega dados no PDW."
ms.date: 10/20/2016
ms.topic: article
ms.assetid: 79c48520-b08b-4b15-a943-a551cc90a2c4
caps.latest.revision: "30"
ms.openlocfilehash: 2ac1325b3765bafbe34dc61f65f7641431afdfa0
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="data-type-conversion-rules-for-dwloader"></a>Regras de dwloader conversão de tipo de dados
Este tópico descreve os formatos de dados de entrada e conversões de tipo de dados implícitos que [dwloader carregador de linha de comando](dwloader.md) suporta quando ele carrega dados no PDW. As conversões de dados implícitas ocorrem quando os dados de entrada não corresponde ao tipo de dados na tabela de destino SQL Server PDW. Use essas informações quando criar o processo de carregamento para garantir que seus dados seja carregado com êxito no SQL Server PDW.  
   
  
## <a name="InsertBinaryTypes"></a>Inserindo literais de tipos binários  
A tabela a seguir define os tipos de literal aceitos, o formato e a regras de conversão para carregar um valor literal em uma coluna do SQL Server PDW do tipo **binário** (*n*) ou  **varbinary**(*n*).  
  
|Tipo de dados de entrada|Exemplos de dados de entrada|Conversão para binary ou varbinary tipo de dados|  
|-------------------|-----------------------|-----------------------------------------------|  
|Literal binário|[0x] *hexidecimal_string*<br /><br />Exemplo: 12Ef ou 0x12Ef|O prefixo 0x é opcional.<br /><br />O tamanho de fonte de dados não pode exceder o número de bytes especificado para o tipo de dados.<br /><br />Se o tamanho de fonte de dados for menor que o tamanho do **binário** tipo de dados, os dados são preenchidos para a direita com zeros para alcançar o tamanho do tipo de dados.|  
  
## <a name="InsertDateTimeTypes"></a>Inserindo literais de tipos de data e hora  
Literais de data e hora são representados usando literais de cadeia de caracteres em formatos específicos, incluídos entre aspas. As tabelas a seguir definem o literal de tipos permitidos, formato e regras de conversão para carregar uma data ou hora literal em uma coluna do tipo **datetime**, **smalldatetime**, **data**, **tempo**, **datetimeoffset**, ou **datetime2**. As tabelas definem o formato padrão para o tipo de dados específico. Outros formatos que podem ser especificados são definidos na seção [formatos de data/hora](#DateFormats). Literais de data e hora não podem incluir espaços à esquerda ou à direita. **data**, **smalldatetime**, e valores nulos não podem ser carregados no modo de largura fixa.  
  
### <a name="datetime-data-type"></a>Tipo de dados datetime  
A tabela a seguir define o formato padrão e as regras para carregar valores literais em uma coluna do tipo **datetime**. Uma cadeia de caracteres vazia (") é convertida para o valor padrão ' 12:00:00.000 1900-01-01'. Cadeias de caracteres que contém somente espaços em branco (' ') gera um erro.  
  
|Tipo de dados de entrada|Exemplos de dados de entrada|Conversão em tipo de dados datetime|  
|-------------------|-----------------------|------------------------------------|  
|Cadeia de caracteres literal no **datetime** formato|'AAAA-MM-dd hh [. fff]'<br /><br />Exemplo: ' 2007-05-08 12:35:29.123'|Dígitos fracionários são definidos como 0 quando o valor é inserido. Por exemplo, o literal ' 2007-05-08 12:35 ° será inserido como ' 2007-05-08 12:35:00.000'.|  
|Cadeia de caracteres literal no **smalldatetime** formato|'AAAA-MM-dd hh: mm'<br /><br />Exemplo: ' 2007-05-08 12:35 '|Segundos e fracionários restantes são definidos como 0 quando o valor é inserido.|  
|Cadeia de caracteres literal no **data** formato|'AAAA-MM-dd'<br /><br />Exemplo: ' 2007-05-08'|Valores de tempo (horas, minutos, segundos e frações) são definidos como 12:00:00.000 quando o valor é inserido.|  
|Cadeia de caracteres literal no **datetime2** formato|'AAAA-MM-dd: ss. FFFFFFF'<br /><br />Exemplo: ' 2007-05-08 12:35:29.1234567'|Os dados de origem não podem exceder três dígitos fracionários. Por exemplo, o literal ' 2007-05-08 12:35:29.123' será inserido, mas o valor ' 2007-05-8 12:35:29.1234567' gera um erro.|  
  
### <a name="smalldatetime-data-type"></a>Tipo de dados smalldatetime  
A tabela a seguir define o formato padrão e as regras para carregar valores literais em uma coluna do tipo **smalldatetime**. Uma cadeia de caracteres vazia (") é convertida para o valor padrão ' 1900-01-01 12:00 '. Cadeias de caracteres que contém somente espaços em branco (' ') gera um erro.  
  
|Tipo de dados de entrada|Exemplos de dados de entrada|Conversão em tipo de dados smalldatetime|  
|-------------------|-----------------------|-----------------------------------------|  
|Cadeia de caracteres literal no **smalldatetime** formato|'AAAA-MM-dd hh: mm' ou 'AAAA-MM-dd HH'<br /><br />Exemplo: ' 2007-05-08-12:00 ' ou ' 2007-05-08-12:00:15 '|Os dados de origem devem ter valores de ano, mês, data, hora e minuto. Segundos são opcionais e, se presente, devem ser definidos como o valor 00. Qualquer outro valor gera um erro.<br /><br />Segundos são opcionais. Ao carregar em uma coluna smalldatetime, dwloader será arredondar segundos e segundos fracionários. Por exemplo, 1999-01-05 20:10:35.123 será carregado como 01-05 20:11.|  
|Cadeia de caracteres literal no **data** formato|'AAAA-MM-dd'<br /><br />Exemplo: ' 2007-05-08'|Valores de tempo (horas, minutos, segundos e frações) são definidos como 0 quando o valor é inserido.|  
  
### <a name="date-data-type"></a>Tipo de dados de data  
A tabela a seguir define o formato padrão e as regras para carregar valores literais em uma coluna do tipo **data**. Uma cadeia de caracteres vazia (") é convertida para o valor padrão ' 1900-01-01'. Cadeias de caracteres que contém somente espaços em branco (' ') gera um erro.  
  
|Tipo de dados de entrada|Exemplos de dados de entrada|Conversão em tipo de dados de data|  
|-------------------|-----------------------|--------------------------------|  
|Cadeia de caracteres literal no **data** formato|'AAAA-MM-dd'<br /><br />Exemplo: ' 2007-05-08'||  
  
### <a name="time-data-type"></a>Tipo de dados de tempo  
A tabela a seguir define o formato padrão e as regras para carregar valores literais em uma coluna do tipo **tempo**. Uma cadeia de caracteres vazia (") é convertida para o valor padrão '00:00:00.0000'. Cadeias de caracteres que contém somente espaços em branco (' ') gera um erro.  
  
|Tipo de dados de entrada|Exemplos de dados de entrada|Conversão em tipo de dados de tempo|  
|-------------------|-----------------------|--------------------------------|  
|Cadeia de caracteres literal no **tempo** formato|': ss. FFFFFFF'<br /><br />Exemplo: '12:35:29.1234567'|Se a fonte de dados tem uma precisão menor ou igual (número de dígitos fracionários) que a precisão de **tempo** tipo de dados, os dados são preenchidos para a direita com zeros. Por exemplo, um valor literal '12:35:29.123' será inserido como '12:35:29.1230000'.|  
  
### <a name="datetimeoffset-data-type"></a>Tipo de dados DateTimeOffset  
A tabela a seguir define o formato padrão e as regras para carregar valores literais em uma coluna do tipo **datetimeoffset** (*n*). O formato padrão é ' AAAA-MM-dd: ss. FFFFFFF {+ |-} hh: mm '. Uma cadeia de caracteres vazia (") é convertida para o valor padrão ' 1900-01-01 12:00:00.0000000 + 00:00 '. Cadeias de caracteres que contém somente espaços em branco (' ') gera um erro. O número de dígitos fracionários depende da definição de coluna. Por exemplo, uma coluna definida como **datetimeoffset** (2) terá dois dígitos fracionários.  
  
|Tipo de dados de entrada|Exemplos de dados de entrada|Conversão em tipo de dados datetimeoffset|  
|-------------------|-----------------------|------------------------------------------|  
|Cadeia de caracteres literal no **datetime** formato|'AAAA-MM-dd hh [. fff]'<br /><br />Exemplo: ' 2007-05-08 12:35:29.123'|Dígitos de fração ausentes e os valores de deslocamento são definidos como 0 quando o valor é inserido. Por exemplo, o literal ' 2007-05-08 12:35:29.123' será inserido como ' 2007-05-08 12:35:29.1230000 + 00:00 '.|  
|Cadeia de caracteres literal no **smalldatetime** formato|'AAAA-MM-dd hh: mm'<br /><br />Exemplo: ' 2007-05-08 12:35 '|Segundos fracionários restantes e os valores de deslocamento são definidos como 0 quando o valor é inserido.|  
|Cadeia de caracteres literal no **data** formato|'AAAA-MM-dd'<br /><br />Exemplo: ' 2007-05-08'|Valores de tempo (horas, minutos, segundos e frações) são definidos como 0 quando o valor é inserido. Por exemplo, o literal ' 2007-05-08' será inserido como ' 2007-05-08 00:00:00.0000000 + 00:00 '.|  
|Cadeia de caracteres literal no **datetime2** formato|'AAAA-MM-dd: ss. FFFFFFF'<br /><br />Exemplo: ' 2007-05-08 12:35:29.1234567'|Os dados de origem não podem exceder o número especificado de segundos fracionários na coluna datetimeoffset. Se a fonte de dados tem um número igual ou menor de frações de segundo, os dados são preenchidos para a direita com zeros. Por exemplo, se o tipo de dados datetimeoffset (5), o valor literal ' 2007-05-08 12:35:29.123 + 12:15 ' será inserido como ' 12:35:29.12300 + 12:15 '.|  
|Cadeia de caracteres literal no **datetimeoffset** formato|' AAAA-MM-dd: ss. FFFFFFF {+ &#124;;-} hh: mm '<br /><br />Exemplo: ' 2007-05-08 12:35:29.1234567 + 12:15 '|Os dados de origem não podem exceder o número especificado de segundos fracionários na coluna datetimeoffset. Se a fonte de dados tem um número igual ou menor de frações de segundo, os dados são preenchidos para a direita com zeros. Por exemplo, se o tipo de dados datetimeoffset (5), o valor literal ' 2007-05-08 12:35:29.123 + 12:15 ' será inserido como ' 12:35:29.12300 + 12:15 '.|  
  
### <a name="datetime2-data-type"></a>Tipo de dados datetime2  
A tabela a seguir define o formato padrão e as regras para carregar valores literais em uma coluna do tipo **datetime2** (*n*). O formato padrão é 'AAAA-MM-dd: ss. FFFFFFF'. Uma cadeia de caracteres vazia (") é convertida para o valor padrão ' 1900-01-01 12:00:00 '. Cadeias de caracteres que contém somente espaços em branco (' ') gera um erro. O número de dígitos fracionários depende da definição de coluna. Por exemplo, uma coluna definida como **datetime2** (2) terá dois dígitos fracionários.  
  
|Tipo de dados de entrada|Exemplos de dados de entrada|Conversão em tipo de dados datetime2|  
|-------------------|-----------------------|-------------------------------------|  
|Cadeia de caracteres literal no **datetime** formato|'AAAA-MM-dd hh [. fff]'<br /><br />Exemplo: ' 2007-05-08 12:35:29.123'|Frações de segundo são opcionais e são definidos como 0 quando o valor é inserido.|  
|Cadeia de caracteres literal no **smalldatetime** formato|'AAAA-MM-dd hh: mm'<br /><br />Exemplo: ' 2007-05-08 12'|Segundos opcionais e fracionários restantes são definidos como 0 quando o valor é inserido.|  
|Cadeia de caracteres literal no **data** formato|'AAAA-MM-dd'<br /><br />Exemplo: ' 2007-05-08'|Valores de tempo (horas, minutos, segundos e frações) são definidos como 0 quando o valor é inserido. Por exemplo, o literal ' 2007-05-08' será inserido como ' 2007-05-08 12:00:00.0000000'.|  
|Cadeia de caracteres literal no **datetime2** formato|'AAAA-MM-dd hh:mm:ss:fffffff'<br /><br />Exemplo: ' 2007-05-08 12:35:29.1234567'|Se a fonte de dados contém os componentes de data e hora que são menor ou igual ao valor especificado em **datetime2**(*n*), os dados são inseridos; caso contrário, será gerado um erro.|  
  
### <a name="DateFormats"></a>Formatos de data e hora  
Dwloader suporta os seguintes formatos de dados para os dados de entrada que está sendo carregado no SQL Server PDW. Mais detalhes estão listados após a tabela.  
  
|datetime|smalldatetime|date|datetime2|datetimeoffset|  
|------------|-----------------|--------|-------------|------------------|  
|[M [M]] M-[d] d-[AA] AA hh [. fff]|[M [M]] M-[d] d-[AA] AA hh: mm [: 00]|[M [M]] M-[d] d-[AA] AA|[M [M]] M-[d] d-[AA] AA hh [. FFFFFFF]|[M [M]] M-[d] d-[AA] AA hh [. FFFFFFF] zzz|  
|[M [M]] M-[d] d-[AA] AA hh [. fff] [tt]|[M [M]] M-[d] d-[AA] AA hh: mm [: 00] [tt]||[M [M]] M-[d] d-[AA] AA hh [. FFFFFFF] [tt]|[M [M]] M-[d] d-[AA] AA hh [. FFFFFFF] [tt] zzz|  
|[M [M]] M-[AA] AA-[d] d hh [. fff]|[M [M]] M-[AA] AA-[d] d hh: mm [: 00]|[M [M]] M-[AA] AA-[d] d|[M [M]] M-[AA] AA-[d] d hh [. FFFFFFF]|[M [M]] M-[AA] AA-[d] d zzz hh [. FFFFFFF]|  
|[M [M]] M-[AA] AA-[d] d hh [. fff] [tt]|[M [M]] M-[AA] AA-[d] d hh: mm [: 00] [tt]||[M [M]] M-[AA] AA-[d] d hh [. FFFFFFF] [tt]|[M [M]] M-[AA] AA-[d] d hh [. FFFFFFF] [tt] zzz|  
|[AA] AA-[[M] M] M-[d] d hh [. fff]|[AA] AA-[[M] M] M-[d] d hh: mm [: 00]|[AA] AA-[[M] M] M-[d] d|[AA] AA-[[M] M] M-[d] d hh [. FFFFFFF]|[AA] AA-[[M] M] M-[d] d hh [. FFFFFFF] zzz|  
|[AA] AA-[[M] M] M-[d] d hh [. fff] [tt]|[AA] AA-[[M] M] M-[d] d hh: mm [: 00] [tt]||[AA] AA-[[M] M] M-[d] d hh [. FFFFFFF] [tt]|[AA] AA-[[M] M] M-[d] d hh [. FFFFFFF] [tt] zzz|  
|[AA] AA-[d] d-[[M] M] M hh [. fff]|[AA] AA-[d] d-[[M] M] M hh: mm [: 00]|[AA] AA - d [d]-[[M] M] M|[AA] AA-[d] d-[[M] M] M hh [. FFFFFFF]|[AA] AA-[d] d-[[M] M] M hh [. FFFFFFF] zzz|  
|[AA] AA-[d] d-[[M] M] M hh [. fff] [tt]|[AA] AA-[d] d-[[M] M] M hh: mm [: 00] [tt]||[AA] AA-[d] d-[[M] M] M hh [. FFFFFFF] [tt]|[AA] AA-[d] d-[[M] M] M hh [. FFFFFFF] [tt] zzz|  
|[d] d-[[M] M] M-[AA] AA hh [. fff]|[d] d-[[M] M] M-[AA] AA hh: mm [: 00]|[d] d-[[M] M] M-[AA] AA|[d] d-[[M] M] M-[AA] AA hh [. FFFFFFF]|[d] d-[[M] M] M-[AA] AA hh [. FFFFFFF] zzz|  
|[d] d-[[M] M] M-[AA] AA hh [. fff] [tt]|[d] d-[[M] M] M-[AA] AA hh: mm [: 00] [tt]||[d] d-[[M] M] M-[AA] AA hh [. FFFFFFF] [tt]|[d] d-[[M] M] M-[AA] AA hh [. FFFFFFF] [tt] zzz|  
|d [d]-[AA] AA-[[M] M] M hh [. fff]|d [d]-[AA] AA-[[M] M] M hh: mm [: 00]|d [d]-[AA] AA-[[M] M] M|d [d]-[AA] AA-[[M] M] M hh [. FFFFFFF]|[d] d-[AA] AA-[[M] M] M hh [. FFFFFFF] zzz|  
|[d] d-[AA] AA-[[M] M] M hh [. fff] [tt]|[d] d-[AA] AA-[[M] M] M hh: mm [: 00] [tt]||[d] d-[AA] AA-[[M] M] M hh [. FFFFFFF] [tt]|[d] d-[AA] AA-[[M] M] M hh [. FFFFFFF] [tt] zzz|  
  
Detalhes:  
  
-   Para separar os valores do mês, dia e ano, você pode usar '-', '/' ou '. '. Para simplificar, a tabela usa apenas o separador '-'.  
  
-   Para especificar o mês como texto use três ou mais caracteres. Meses com 1 ou 2 caracteres serão interpretadas como um número.  
  
-   Para separar os valores de tempo, use o ': ' símbolo.  
  
-   Letras entre colchetes são opcionais.  
  
-   As letras 'tt' designam [AM | PM | am | pm]. AM é o padrão. Quando 'tt' for especificado, o valor de hora (hh) deve ser no intervalo de 0 a 12.  
  
-   As letras 'zzz' designam o deslocamento de fuso horário para a zona de tempo atual do sistema no formato {+ |-} HH:ss].  
  
## <a name="InsertNumerictypes"></a>Inserindo literais de tipos numéricos  
As tabelas a seguir definem as regras de formato e a conversão do padrão de carregamento de um valor literal em uma coluna do SQL Server PDW que usa um tipo numérico.  
  
### <a name="bit-data-type"></a>Tipo de dados bit  
A tabela a seguir define o formato padrão e as regras para carregar valores literais em uma coluna do tipo **bit**. Uma cadeia de caracteres vazia (") ou uma cadeia de caracteres que contém somente espaços em branco (' ') é convertido em 0.  
  
|Tipo de dados de entrada|Exemplos de dados de entrada|Conversão em tipo de dados bit|  
|-------------------|-----------------------|-------------------------------|  
|Cadeia de caracteres literal no **inteiro** formato|'ffffffffff'<br /><br />Exemplo: '1' ou '321'|Um valor inteiro formatado como um literal de cadeia de caracteres não pode conter um valor negativo. Por exemplo, o valor '-123' gera um erro.<br /><br />Um valor maior que 1 é convertido em 1. Por exemplo, o valor '123' é convertido em 1.|  
|Literal de cadeia de caracteres|'TRUE' ou 'FALSE'<br /><br />Exemplo: 'true'|O valor 'TRUE' é convertido em 1. o valor 'FALSE' é convertido em 0.|  
|Literal de inteiro|fffffffn<br /><br />Exemplo: 1 ou 321|Um valor menor que 0 ou maior que 1 é convertido em 1. Por exemplo, os valores 123 e-123 são convertidos em 1.|  
|Literal decimal|fffnn.fffn<br /><br />Exemplo: 1234.5678|Um valor menor que 0 ou maior que 1 é convertido em 1. Por exemplo, os valores 123,45 e-123.45 são convertidos em 1.|  
  
### <a name="decimal-data-type"></a>Tipo de dados decimal  
A tabela a seguir define as regras para carregar valores literais em uma coluna do tipo **decimal** (*p, s*). Regras de conversão de dados são as mesmas para SQL Server. Para obter mais informações, consulte [conversão de tipo de dados (mecanismo de banco de dados)](http://go.microsoft.com/fwlink/?LinkId=202128) no MSDN.  
  
|Tipo de dados de entrada|Exemplos de dados de entrada|  
|-------------------|-----------------------|  
|Literal de inteiro|321312313123|  
|Literal decimal|123344.34455|  
  
### <a name="float-and-real-data-types"></a>Tipos de dados float e real  
A tabela a seguir define as regras para carregar valores literais em uma coluna do tipo **float** ou **real**. Regras de conversão de dados são as mesmas para SQL Server. Para obter mais informações, consulte [conversão de tipo de dados (mecanismo de banco de dados)](../t-sql/data-types/data-type-conversion-database-engine.md) no MSDN.  
  
|Tipo de dados de entrada|Exemplos de dados de entrada|  
|-------------------|-----------------------|  
|Literal de inteiro|321312313123|  
|Literal decimal|123344.34455|  
|Literal de ponto flutuante|3.12323E + 14|  
  
### <a name="int-bigint-tinyint-smallint-data-types"></a>int, bigint, smallint tipos de dados tinyint  
A tabela a seguir define as regras para carregar valores literais em uma coluna do tipo **int**, **bigint**, **tinyint**, ou **smallint**. A fonte de dados não pode exceder o intervalo permitido para o tipo de dados específico. Por exemplo, o intervalo de **tinyint** é de 0 a 255 e o intervalo para **int** é de -2.147.483.648 a 2.147.483.647.  
  
|Tipo de dados de entrada|Exemplos de dados de entrada|Conversão em tipos de dados inteiro|  
|-------------------|-----------------------|------------------------------------|  
|Literal de inteiro|321312313123||  
|Literal decimal|123344.34455|Os valores à direita do separador decimal são truncados.|  
  
### <a name="money-and-smallmoney-data-types"></a>Tipos de dados Money e smallmoney  
Valores literais dinheiro são representados como uma cadeia de caracteres de números com um ponto decimal opcional e um símbolo monetário opcional como prefixo. A fonte de dados não pode exceder o intervalo permitido para o tipo de dados específico. Por exemplo, o intervalo de **smallmoney** é de -214.748,3648 214.748,3647 e o intervalo de **money** é -922.337.203.685.477,5808 e 922.337.203.685.477,5807. A tabela a seguir define as regras para carregar valores literais em uma coluna do tipo **money** ou **smallmoney**.  
  
|Tipo de dados de entrada|Exemplos de dados de entrada|Conversão para o dinheiro ou smallmoney tipo de dados|  
|-------------------|-----------------------|-----------------------------------------------|  
|Literal de inteiro|321312|Dígitos após o ponto decimal são definidos como 0 quando o valor é inserido. Por exemplo, o literal 12345 é inserido como 12345.0000|  
|Literal decimal|123344.34455|Se o número de dígitos após o ponto decimal exceder 4, o valor é arredondado para o valor mais próximo. Por exemplo, o valor 123344.34455 é inserido como 123344.3446.|  
|Money literal|$123456.7890|O símbolo de moeda não é inserido com o valor.<br /><br />Se o número de dígitos após o ponto decimal exceder 4, o valor é arredondado para o valor mais próximo.|  
  
## <a name="InsertStringTypes"></a>Inserindo literais de cadeia de caracteres de tipos  
As tabelas a seguir definem as regras de formato e a conversão do padrão de carregamento de um valor literal em uma coluna do SQL Server PDW que usa um tipo de cadeia de caracteres.  
  
### <a name="char-varchar-nchar-and-nvarchar-data-types"></a>Tipos de dados char, varchar, nchar e nvarchar  
A tabela a seguir define o formato padrão e as regras para carregar valores literais em uma coluna do tipo **char**, **varchar**, **nchar** e **nvarchar** . O tamanho de fonte de dados não pode exceder o tamanho especificado para o tipo de dados. Se o tamanho de fonte de dados for menor que o tamanho do **char** ou **nchar** tipo de dados, os dados são preenchidos para a direita com espaços em branco para alcançar o tamanho do tipo de dados.  
  
|Tipo de dados de entrada|Exemplos de dados de entrada|Conversão em tipos de dados de caractere|  
|---------------|-------------------|----------------------------------|  
|Literal de cadeia de caracteres|Formato: 'cadeia de caracteres'<br /><br />Exemplo: 'abc'| NA |  
|Literal de cadeia Unicode|Formato: Cadeia de caracteres N'character'<br /><br />Exemplo: N'abc'| NA |  
|Literal de inteiro|Formato: ffffffffffn<br /><br />Exemplo: 321312313123| NA |  
|Literal decimal|Formato: ffffff.fffffff<br /><br />Exemplo: 12344.34455| NA |  
|Money literal|Formato: $ffffff.fffnn<br /><br />Exemplo: US $123456.99|O símbolo monetário opcional não é inserido com o valor. Para inserir o símbolo de moeda, insira o valor como uma cadeia de caracteres literal. Isso corresponderá o formato do carregador, que trata cada literal como uma cadeia de caracteres literal.<br /><br />Vírgulas não são permitidas.<br /><br />Se o número de dígitos após o ponto decimal exceder 2, o valor é arredondado para o valor mais próximo. Por exemplo, o valor 123.946789 é inserido como 123.95.<br /><br />Somente o estilo padrão 0 (sem vírgulas e 2 dígitos após o ponto decimal) é permitido ao usar a função CONVERT para inserir os literais de dinheiro.|  
  
### <a name="general-remarks"></a>Comentários gerais  
**dwloader** realiza as conversões implícitas mesmo que o SMP SQL Server executa, mas não suporta todas as conversões implícitas que ofereça suporte a SMP SQL Server.  
 
<!-- MISSING LINKS 
## See Also  
[Grant Permissions to Load Data &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-load-data-sql-server-pdw.md)  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  

-->
  
