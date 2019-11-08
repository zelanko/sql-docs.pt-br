---
title: Suporte de tipo de dados para melhorias de data e hora ODBC | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- date/time [ODBC], data type support
- ODBC, date/time improvements
ms.assetid: 8e0d9ba2-3ec1-4680-86e3-b2590ba8e2e9
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ed58bf3db95d9989bedf2826cdd722206bfb4d51
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73784002"
---
# <a name="data-type-support-for-odbc-date-and-time-improvements"></a>Suporte a tipos de dados para aprimoramentos de data e hora do ODBC
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Este tópico fornece informações sobre tipos de ODBC com suporte a tipos de dados de data e hora do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="data-type-mapping-in-parameters-and-resultsets"></a>Mapeamento de tipo de dados em parâmetros e conjuntos de resultados  
 Além dos tipos de dados ODBC (SQL_TYPE_TIMESTAMP e SQL_TIMESTAMP), dois novos tipos de dados foram adicionados ao ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client para expor os novos tipos de servidor:  
  
-   SQL_SS_TIME2  
  
-   SQL_SS_TIMESTAMPOFFSET  
  
 A tabela seguinte mostra o mapeamento completo de tipo do servidor. Observe que algumas células da tabela contêm duas entradas; nestes casos, a primeira é o valor ODBC 3.0 e a segunda é o valor ODBC 2.0.  
  
|Tipo de dados do SQL Server|Tipo de dados SQL|Value|  
|--------------------------|-------------------|-----------|  
|Datetime|SQL_TYPE_TIMESTAMP<br /><br /> SQL_TIMESTAMP|93 (sql.h)<br /><br /> 11 (sqlext.h)|  
|Smalldatetime|SQL_TYPE_TIMESTAMP<br /><br /> SQL_TIMESTAMP|93 (sql.h)<br /><br /> 11 (sqlext.h)|  
|Data|SQL_TYPE_DATE<br /><br /> SQL_DATE|91 (SQL. h)<br /><br /> 9 (sqlext. h)|  
|Hora|SQL_SS_TIME2|-154 (SQLNCLI. h)|  
|DatetimeOFFSET|SQL_SS_TIMESTAMPOFFSET|-155 (SQLNCLI.h)|  
|Datetime2|SQL_TYPE_TIMESTAMP<br /><br /> SQL_TIMESTAMP|93 (sql.h)<br /><br /> 11 (sqlext.h)|  
  
 A tabela seguinte lista as estruturas correspondentes e os tipos ODBC C. Como o ODBC não permite tipos C definidos pelo driver, SQL_C_BINARY é usado para time e datetimeoffset como estruturas binárias.  
  
|Tipo de dados SQL|Layout de memória|Tipo de dados C padrão|Valor (sqlext.h)|  
|-------------------|-------------------|-------------------------|------------------------|  
|SQL_TYPE_TIMESTAMP<br /><br /> SQL_TIMESTAMP|SQL_TIMESTAMP_STRUCT<br /><br /> TIMESTAMP_STRUCT|SQL_C_TYPE_TIMESTAMP<br /><br /> SQL_C_TIMESTAMP|SQL_TYPE_TIMESTAMP<br /><br /> SQL_TIMESTAMP|  
|SQL_TYPE_DATE<br /><br /> SQL_DATE|SQL_DATE_STRUCT<br /><br /> DATE_STRUCT|SQL_C_TYPE_DATE<br /><br /> SQL_C_DATE|SQL_TYPE_DATE<br /><br /> SQL_DATE|  
|SQL_SS_TIME2|SQL_SS_TIME2_STRUCT|SQL_C_SS_TIME2<br /><br /> SQL_C_BINARY (ODBC 3.5 e anterior)|0x4000 (sqlncli.h)<br /><br /> SQL_BINARY (-2)|  
|SQL_SS_TIMESTAMPOFFSET|SQL_SS_TIMESTAMPOFFSET_STRUCT|SQL_C_SS_TIMESTAMPOFFSET<br /><br /> SQL_C_BINARY (ODBC 3.5 e anterior)|0x4001 (sqlncli.h)<br /><br /> SQL_BINARY (-2)|  
  
 Quando a associação SQL_C_BINARY é especificada, a verificação do alinhamento será executada e um erro relatado para alinhamento incorreto. O SQLSTATE para esse erro será IM016, com a mensagem "Alinhamento de estrutura incorreto".  
  
## <a name="data-formats-strings-and-literals"></a>Formatos de dados: cadeias e literais  
 A tabela seguinte mostra os mapeamentos entre tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], tipos de dados ODBC e os literais da cadeia de caracteres ODBC.  
  
|Tipo de dados do SQL Server|Tipo de dados ODBC|Formato de cadeia de caracteres para conversões do cliente|  
|--------------------------|--------------------|------------------------------------------|  
|Datetime|SQL_TYPE_TIMESTAMP<br /><br /> SQL_TIMESTAMP|'aaaa-mm-dd hh:mm:ss[.999]'<br /><br /> O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte a até três dígitos de fração de segundo para Datetime.|  
|Smalldatetime|SQL_TYPE_TIMESTAMP<br /><br /> SQL_TIMESTAMP|'aaaa-mm-dd hh:hh:ss'<br /><br /> Este tipo de dados tem precisão de um minuto. O componente de segundos será zero na saída, sendo arredondado pelo servidor na entrada.|  
|Data|SQL_TYPE_DATE<br /><br /> SQL_DATE|'aaaa-mm-dd'|  
|Hora|SQL_SS_TIME2|'hh:mm:ss[.9999999]'<br /><br /> Opcionalmente, podem ser especificadas frações de segundo usando até sete dígitos.|  
|Datetime2|SQL_TYPE_TIMESTAMP<br /><br /> SQL_TIMESTAMP|' aaaa-mm-dd hh: mm: SS [. 9999999] '<br /><br /> Opcionalmente, podem ser especificadas frações de segundo usando até sete dígitos.|  
|DatetimeOFFSET|SQL_SS_TIMESTAMPOFFSET|'aaaa-mm-dd hh:mm:ss[.9999999] +/- hh:mm'<br /><br /> Opcionalmente, podem ser especificadas frações de segundo usando até sete dígitos.|  
  
 Não há nenhuma alteração às sequências de escape de ODBC para literais de data/hora.  
  
 As frações de segundo nos resultados sempre usam um ponto (.), em vez de dois-pontos (:).  
  
 Valores da cadeia de caracteres retornados aos aplicativos têm sempre o mesmo comprimento para uma determinada coluna. Componentes de ano, mês, dia, hora, minuto e segundo são preenchidos com zeros à esquerda até sua largura máxima, e há um espaço entre date e time nos valores de datetime. Também há um espaço entre o deslocamento de time e timezone em um valor de datetimeoffset. Um deslocamento de timezone sempre é precedido por um sinal; quando o deslocamento é zero, este sinal é de mais (+). As frações de segundos são preenchidas com zeros à direita, se necessário, até a precisão definida para a coluna. Para colunas do tipo datetime, há três dígitos para frações de segundo. Para colunas do tipo smalldatetime, não há nenhum dígito de fração de segundo e os segundos sempre serão zero.  
  
 Uma cadeia de caracteres vazia não é um literal de data/hora válido e não representa um valor NULL. Uma tentativa de conversão de uma cadeia de caracteres vazia para um valor de data/hora resultará em erro SQLState 22018 e a mensagem "Valor de caractere inválido para a especificação de difusão".  
  
 As conversões de parâmetros de cadeia de caracteres esperarão caracteres no mesmo formato, com exceções de que o sinal de um fuso horário com zero horas e zero minutos podem ser mais ou menos, e zeros à direita são permitidos para frações de segundos com, no máximo, nove dígitos. Um componente de hora pode terminar com um ponto decimal e não ter dígitos de fração de segundo.  
  
 Atualmente, o driver permite espaço em branco adicional ao redor de caracteres de pontuação e o espaço entre deslocamento de time e timezone é opcional. Porém, isto pode ser alterado em uma versão futura; aplicativos não devem confiar no comportamento atual.  
  
## <a name="data-formats-data-structures"></a>Formatos de dados: estruturas de dados  
 Nas estruturas descritas a seguir, ODBC especifica as seguintes restrições, que são obtidas do calendário gregoriano:  
  
-   O intervalo de meses é de 1 a 12.  
  
-   O intervalo do campo de dias é de 1 ao número de dias do mês e deve ser coerente com os campos de ano e mês, levando em conta os anos bissextos.  
  
-   O intervalo de horas é de 0 a 23.  
  
-   O intervalo de minutos é de 0 a 59.  
  
-   O intervalo de segundos é 0 por 61,9(n). Isso permite até dois segundos intercalares para manter a sincronização com a hora sideral.  
  
     Observe que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não permite segundos intercalados. Dessa forma, valores de segundo maiores que 59 causarão um erro de servidor.  
  
 Foram modificadas as implementações das seguintes estruturas de ODBC existentes para dar suporte aos novos tipos de dados date e time do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Porém, as definições não foram alteradas.  
  
-   DATE_STRUCT  
  
-   TIME_STRUCT  
  
-   TIMESTAMP_STRUCT  
  
 Também há duas novas estruturas:  
  
-   SQL_SS_TIME2_STRUCT  
  
-   SQL_SS_TIMESTAMPOFFSET_STRUCT  
  
### <a name="sql_ss_time2_struct"></a>SQL_SS_TIME2_STRUCT  
 Esse struct é preenchido com até 12 bytes nos sistemas operacionais de 32 e 64 bits.  
  
```  
typedef struct tagSS_TIME2_STRUCT {  
   SQLUSMALLINT hour;  
   SQLUSMALLINT minute;  
   SQLUSMALLINT second;  
   SQLUINTEGER fraction;  
} SQL_SS_TIME2_STRUCT;  
```  
  
### <a name="sql_ss_timestampoffset_struct"></a>SQL_SS_TIMESTAMPOFFSET_STRUCT  
  
```  
typedef struct tagSS_TIMESTAMPOFFSET_STRUCT {  
   SQLSMALLINT year;  
   SQLUSMALLINT month;  
   SQLUSMALLINT day;  
   SQLUSMALLINT hour;  
   SQLUSMALLINT minute;  
   SQLUSMALLINT second;  
   SQLUINTEGER fraction;  
   SQLSMALLINT timezone_hour;  
   SQLSMALLINT timezone_minute;  
} SQL_SS_TIMESTAMPOFFSET_STRUCT;  
```  
  
 Se o **timezone_hour** for negativo, o **timezone_minute** deverá ser negativo ou zero. Se o **timezone_hour** for positivo, o **timezone_minute** deverá ser positivo ou zero. Se o **timezone_hour** for zero, o **timezone_minute** poderá ter qualquer valor no intervalo de-59 a + 59.  
  
## <a name="see-also"></a>Consulte também  
 [Aprimoramentos &#40;de data e hora do ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
  
