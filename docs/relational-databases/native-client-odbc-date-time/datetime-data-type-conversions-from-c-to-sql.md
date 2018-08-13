---
title: Conversões do C para SQL | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- conversions [ODBC], C to SQL
ms.assetid: 7ac098db-9147-4883-8da9-a58ab24a0d31
caps.latest.revision: 35
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: f983a9ae2d98b5e93b08b65938b6627e1ea83c6c
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39542546"
---
# <a name="datetime-data-type-conversions-from-c-to-sql"></a>Conversões do tipo de dados datetime do C para SQL
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Este tópico lista os problemas a considerar ao converter tipos C a tipos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de data/hora.  
  
 As conversões descritas na tabela a seguir se aplicam a conversões feitas no cliente. Em casos em que o cliente especifica a precisão de segundo fracionário para um parâmetro que é diferente do que definido no servidor, a conversão do cliente pode ter êxito, mas o servidor retornará um erro quando **SQLExecute** ou  **SQLExecuteDirect** é chamado. Em particular, o ODBC trata qualquer truncamento de frações de segundo como um erro, enquanto o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] comportamento é arredondar; por exemplo, o arredondamento ocorre quando você vai **datetime2(6)** para **datetime2(2)**. Os valores da coluna datetime são arredondados para 1/300º de um segundo e as colunas smalldatetime têm os segundos definidos como zero pelo servidor.  
  
|||||||||  
|-|-|-|-|-|-|-|-|  
||SQL_TYPE_DATE|SQL_TYPE_TIME|SQL_SS_TIME2|SQL_TYPE_TIMESTAMP|SQL_SS_TIMSTAMPOFFSET|SQL_CHAR|SQL_WCHAR|  
|SQL_C_DATE|1|-|-|1,6|1,5,6|1,13|1,13|  
|SQL_C_TIME|-|1|1|1,7|1,5,7|1,13|1,13|  
|SQL_C_SS_TIME2|-|1,3|1,10|1,7|1,5,7|1,13|1,13|  
|SQL_C_BINARY(SQL_SS_TIME2_STRUCT)|N/A|N/A|1,10,11|N/A|N/A|N/A|N/A|  
|SQL_C_TYPE_TIMESTAMP|1,2|1,3,4|1,4,10|1,10|1,5,10|1,13|1,13|  
|SQL_C_SS_TIMESTAMPOFFSET|1,2,8|1,3,4,8|1,4,8,10|1,8,10|1,10|1,13|1,13|  
|SQL_C_BINARY(SQL_SS_TIMESTAMPOFFSET_STRUCT)|N/A|N/A|N/A|N/A|1,10,11|N/A|N/A|  
|SQL_C_CHAR/SQL_WCHAR (date)|9|9|9|9,6|9,5,6|N/A|N/A|  
|SQL_C_CHAR/SQL_WCHAR (time2)|9|9,3|9,10|9,7,10|9,5,7,10|N/A|N/A|  
|SQL_C_CHAR/SQL_WCHAR (datetime)|9,2|9,3,4|9,4,10|9,10|9,5,10|N/A|N/A|  
|SQL_C_CHAR/SQL_WCHAR (datetimeoffset)|9,2,8|9,3,4,8|9,4,8,10|9,8,10|9,10|N/A|N/A|  
|SQL_C_BINARY(SQL_DATE_STRUCT)|1,11|N/A|N/A|N/A|N/A|N/A|N/A|  
|SQL_C_BINARY(SQL_TIME_STRUCT)|N/A|N/A|N/A|N/A|N/A|N/A|N/A|  
|SQL_C_BINARY(SQL_TIMESTAMP_STRUCT)|N/A|N/A|N/A|N/A|N/A|N/A|N/A|  
  
## <a name="key-to-symbols"></a>Legenda dos símbolos  
  
-   **-**: Nenhuma conversão é suportada. Será gerado um registro de diagnóstico com SQLSTATE 07006 e a mensagem "Violação do atributo de tipo de dados restrito".  
  
-   **1**: se os dados fornecidos não forem válidos, um registro de diagnóstico é gerado com SQLSTATE 22007 e a mensagem "formato de datetime inválido".  
  
-   **2**: campos de hora devem ser zero ou um registro de diagnóstico será gerado com SQLSTATE 22008 e a mensagem "Truncamento fracionário".  
  
-   **3**: frações de segundo devem ser zero ou um registro de diagnóstico será gerado com SQLSTATE 22008 e a mensagem "Truncamento fracionário".  
  
-   **4**: o componente de data será ignorado.  
  
-   **5**: o fuso horário é definido como a configuração de fuso horário do cliente.  
  
-   **6**: a hora é definida como zero.  
  
-   **7**: a data é definida como a data atual.  
  
-   **8**: a hora é convertida do fuso horário do cliente para UTC. Se ocorrer um erro durante esta conversão, um registro de diagnóstico será gerado com SQLSTATE 22008 e a mensagem "Estouro do campo datetime".  
  
-   **9**: a cadeia de caracteres é analisada e convertida em uma data, datetime, datetimeoffset ou valor de tempo, dependendo do primeiro caractere de pontuação encontrado e a presença dos componentes restantes. A cadeia de caracteres é então convertida no tipo de destino, seguindo as regras na tabela anterior para o tipo de origem descoberto por este processo. Se for detectado um erro ao analisar os dados, um registro de diagnóstico será gerado com SQLSTATE 22018 e a mensagem "Valor de caractere inválido para a especificação de difusão". Para os parâmetros datetime e smalldatetime, se o ano estiver fora do intervalo ao qual esses tipos dão suporte, um registro de diagnóstico será gerado com SQLSATE 22007 e a mensagem "Formato de datetime inválido".  
  
     Para datetimeoffset, o valor deve estar dentro do intervalo após a conversão em UTC, mesmo que nenhuma conversão em UTC seja solicitada. O motivo disso é que o TDS e o servidor sempre normalizam a hora em valores datetimeoffset para UTC, por isso o cliente deve verificar se os componentes time estão dentro do intervalo com suporte após a conversão em UTC. Se o valor não estiver no intervalo de UTC com suporte, um registro de diagnóstico será gerado com SQLSTATE 22007 e a mensagem "Formato de datetime inválido".  
  
-   **10**: se ocorrer truncamento com perda de dados, um registro de diagnóstico é gerado com SQLSTATE 22008 e a mensagem "formato de hora inválido". Esse erro também ocorrerá se o valor estiver fora do intervalo que pode ser representado pelo intervalo UTC usado pelo servidor.  
  
-   **11**: se o tamanho de bytes dos dados não é igual ao tamanho da estrutura exigida pelo tipo de SQL, um registro de diagnóstico é gerado com SQLSTATE 22003 e a mensagem "Valor numérico fora do intervalo".  
  
-   **12**: se o comprimento de bytes dos dados for 4 ou 8, os dados são enviados para o servidor no formato bruto smalldatetime ou datetime com TDS. Se o comprimento de bytes dos dados corresponder exatamente ao tamanho de SQL_TIMESTAMP_STRUCT, os dados serão convertidos no formato TDS para datetime2.  
  
-   **13**: se ocorrer truncamento com perda de dados, um registro de diagnóstico é gerado com SQLSTATE 22001 e a mensagem "Dados de cadeia de caracteres, truncados à direita".  
  
     O número de dígitos das frações de segundo (a escala) é determinado pelo tamanho da coluna de destino, de acordo com a seguinte tabela:  
  
    ||||  
    |-|-|-|  
    |Tipo|Escala implícita<br /><br /> 0|Escala implícita<br /><br /> 1..9|  
    |SQL_C_TYPE_TIMESTAMP|19|21..29|  
  
     Entretanto, para SQL_C_TYPE_TIMESTAMP, se as frações de segundo puderem ser representadas com três dígitos sem perda de dados e o tamanho da coluna for 23 ou maior, serão gerados exatamente três dígitos de frações de segundo. Esse comportamento assegura a compatibilidade com versões anteriores de aplicativos desenvolvidos usando drivers ODBC mais antigos.  
  
     Para tamanhos de coluna maiores do que o intervalo na tabela, é sugerida uma escala de 9. Essa conversão deve permitir até nove dígitos de frações de segundo, o máximo permitido pelo ODBC.  
  
     Um tamanho de coluna zero implica em tamanho ilimitado para tipos de caracteres de comprimento variável no ODBC (9 dígitos, a menos que a regra de 3 dígitos para SQL_C_TYPE_TIMESTAMP se aplique). A especificação de um tamanho de coluna zero com um tipo de caractere de comprimento fixo é um erro.  
  
-   **N/d**: existente [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e o comportamento anterior é mantido.  
  
## <a name="see-also"></a>Consulte também  
 [Aprimoramentos de data e hora &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
  
