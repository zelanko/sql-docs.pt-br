---
description: Alterações de cópia em massa para tipos de data e hora aprimorados (OLE DB e ODBC)
title: Cópia em massa, tipos aprimorados OLE DB
ms.custom: ''
ms.date: 12/18/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC, bulk copy operations
ms.assetid: c29e0f5e-9b3c-42b3-9856-755f4510832f
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 208cc75e186c0c1de32ed10d263359ffdbb7e039
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88423878"
---
# <a name="bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc"></a>Alterações de cópia em massa para tipos de data e hora aprimorados (OLE DB e ODBC)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Este tópico descreve os aprimoramentos de data/hora para oferecer suporte à funcionalidade de cópia em massa. As informações deste tópico são válidas para OLE DB e ODBC no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="format-files"></a>Arquivos de formato  
 Ao criar arquivos de formato interativamente, a tabela a seguir descreve a entrada usada para especificar os tipos de data/hora e os nomes de tipo de dados do arquivo de host correspondentes.  
  
|tipo de armazenamento de arquivo|Tipo de dados do arquivo host|Resposta à solicitação: "Insira o tipo de armazenamento de arquivo do campo <nome_do_campo> [\<default>]:"|  
|-----------------------|-------------------------|-----------------------------------------------------------------------------------------------------|  
|Datetime|SQLDATETIME|d|  
|Smalldatetime|SQLDATETIM4|D|  
|Data|SQLDATE|de|  
|Hora|SQLTIME|te|  
|Datetime2|SQLDATETIME2|d2|  
|Datetimeoffset|SQLDATETIMEOFFSET|do|  
||||

 O XSD do arquivo de formato XML terá as adições a seguir:  
  
```xml
<xs:complexType name="SQLDATETIME2">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
<xs:complexType name="SQLDATETIMEOFFSET">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
<xs:complexType name="SQLDATE">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
<xs:complexType name="SQLTIME">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
```  
  
## <a name="character-data-files"></a>Arquivos de dados de caracteres  
 Em arquivos de dados de caractere, os valores de data e hora são representados conforme descrito na seção "formatos de dados: cadeias de caracteres e literais" do [suporte de tipo de dados para melhorias de data e hora ODBC](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md) para ODBC ou de [tipo de dados suporte para OLE DB melhorias de data e hora](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md) para OLE DB.  
  
 No Fles de dados nativos, os valores de data e hora para os quatro novos tipos são representados como suas representações de TDS com uma escala de 7 (porque esse é o máximo com suporte do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e os arquivos de dados BCP não armazenam a escala dessas colunas). Não há nenhuma alteração no armazenamento dos tipos **datetime** e **smalldatetime** existentes nem em suas representações do protocolo TDS.  
  
 Os tamanhos de armazenamento para os diferentes tipos de armazenamento do OLE DB são estes:  
  
|tipo de armazenamento de arquivo|Tamanho de armazenamento em bytes|  
|-----------------------|---------------------------|  
|DATETIME|8|  
|smalldatetime|4|  
|date|3|  
|time|6|  
|datetime2|9|  
|datetimeoffset|11|  
|||

 Os tamanhos para o ODBC são mostrados a seguir. Observe que não é necessário armazenar a precisão nem nos arquivos de formato nem nos de dados, porque o BCP.exe sempre recuperará a precisão do servidor.  
  
|tipo de armazenamento de arquivo|Tamanho de armazenamento em bytes|Formato de armazenamento|  
|-----------------------|---------------------------|--------------------|  
|datetime (d)|8|TDS|  
|smalldatetime (D)|4|TDS|  
|date (de)|3|TDS|  
|time (te)|6|TDS|  
|datetime2 (d2)|9|TDS|  
|datetimeoffset (do)|11|TDS|  
||||

## <a name="bcp-types-in-sqlnclih"></a>Tipos BCP em sqlncli.h  
 Os tipos a seguir são definidos em sqlncli.h para ser usados com as extensões de API BCP para ODBC. Esses tipos são passados com o parâmetro *eUserDataType* do método IBCPSession::BCPColFmt no OLE DB.  
  
|tipo de armazenamento de arquivo|Tipo de dados do arquivo host|Digite sqlncli. h para uso com IBCPSession:: BCPColFmt|Valor|  
|-----------------------|-------------------------|-----------------------------------------------------------|-----------|  
|Datetime|SQLDATETIME|BCP_TYPE_SQLDATETIME|0x3d|  
|Smalldatetime|SQLDATETIM4|BCP_TYPE_SQLDATETIME4|0x3a|  
|Data|SQLDATE|BCP_TYPE_SQLDATE|0x28|  
|Hora|SQLTIME|BCP_TYPE_SQLTIME|0x29|  
|Datetime2|SQLDATETIME2|BCP_TYPE_SQLDATETIME2|0x2a|  
|Datetimeoffset|SQLDATETIMEOFFSET|BCP_TYPE_SQLDATETIMEOFFSET|0x2b|  
|||||

## <a name="bcp-data-type-conversions"></a>Conversões de tipo de dados BCP  
 As tabelas a seguir fornecem informações de conversão.  
  
 **Observação do OLE DB** As conversões a seguir são executadas por IBCPSession. O IRowsetFastLoad usa conversões OLE DB conforme definido em [Conversões realizadas de Cliente para Servidor](../../relational-databases/native-client-ole-db-date-time/conversions-performed-from-client-to-server.md). Observe que os valores datetime são arredondados para 1/300 de um segundo e os valores smalldatetime têm os segundos definidos como zero depois de concluídas as conversões de cliente descritas a seguir. O arredondamento de datetime se propaga para horas e minutos, mas não para a data.  
  
|Para --><br /><br /> De|date|time|smalldatetime|DATETIME|datetime2|datetimeoffset|char|wchar|  
|------------------------|----------|----------|-------------------|--------------|---------------|--------------------|----------|-----------|  
|Data|1|-|1,6|1,6|1,6|1,5,6|1,3|1,3|  
|Hora|N/D|1,10|1,7,10|1,7,10|1,7,10|1,5,7,10|1,3|1,3|  
|Smalldatetime|1,2|1,4,10|1|1|1,10|1,5,10|1,11|1,11|  
|Datetime|1,2|1,4,10|1,12|1|1,10|1,5,10|1,11|1,11|  
|Datetime2|1,2|1,4,10|1,10 (ODBC)1,12 (OLE DB)|1,10|1,10|1,5,10|1,3|1,3|  
|Datetimeoffset|1,2,8|1,4,8,10|1,8,10|1,8,10|1,8,10|1,10|1,3|1,3|  
|Char/wchar (date)|9|-|9,6 (ODBC)9,6,12 (OLE DB)|9,6 (ODBC)9,6,12 (OLE DB)|9,6|9,5,6|N/D|N/D|  
|Char/wchar (time)|-|9,10|9,7,10 (ODBC)9,7,10,12 (OLE DB)|9,7,10 (ODBC)9,7,10, 12 (OLE DB)|9,7,10|9,5,7,10|N/D|N/D|  
|Char/wchar (datetime)|9,2|9,4,10|9,10 (ODBC)9,10,12 (OLE DB)|9,10 (ODBC)9,10,12 (OLE DB)|9,10|9,5,10|N/D|N/D|  
|Char/wchar (datetimeoffset)|9,2,8|9,4,8,10|9,8,10 (ODBC)9,8,10,12 (OLE DB)|9,8,10 (ODBC)9,8,10,12 (OLE DB)|9,8,10|9,10|N/D|N/D|  
||||||||||

#### <a name="key-to-symbols"></a>Legenda dos símbolos  
  
|Símbolo|Significado|  
|------------|-------------|  
|-|Não há suporte a nenhuma conversão.<br /><br /> Será gerado um registro de diagnóstico de ODBC com SQLSTATE 07006 e a mensagem "Violação do atributo de tipo de dados restrito".|  
|1|Se os dados fornecidos não forem válidos, um registro de diagnóstico de ODBC será gerado com SQLSTATE 22007 e a mensagem "Formato de datetime inválido". Para valores datetimeoffset, a parte time deve estar dentro do intervalo após a conversão em UTC, mesmo que nenhuma conversão em UTC seja solicitada. O motivo disso é que o TDS e o servidor sempre normalizam a hora em valores datetimeoffset para UTC. Por isso, o cliente deve verificar se os componentes time estão dentro do intervalo com suporte após a conversão em UTC.|  
|2|O componente time é ignorado.|  
|3|Para ODBC, se ocorrer truncamento com perda de dados, um registro de diagnóstico será gerado com SQLSTATE 22001 e dados de cadeia de caracteres de mensagem, truncados à direita ' o número de dígitos de segundos fracionários (a escala) é determinado do tamanho da coluna de destino de acordo com a tabela a seguir. Para tamanhos de coluna maiores do que o intervalo na tabela, é sugerida uma escala de 7. Essa conversão deve permitir até nove dígitos de segundos fracionários, o máximo permitido pelo ODBC.<br /><br /> **Tipo:** DBTIME2<br /><br /> **Escala implícita 0** 8<br /><br /> **Escala implícita 1.. 7** 10, 16<br /><br /> <br /><br /> **Tipo:** DBTIMESTAMP<br /><br /> **Escala implícita 0:** 19<br /><br /> **Escala implícita 1.. 7:** 21.. 27<br /><br /> <br /><br /> **Tipo:** DBTIMESTAMPOFFSET<br /><br /> **Escala implícita 0:** 26<br /><br /> **Escala implícita 1.. 7:** 28.. 34<br /><br /> Para OLE DB, se ocorrer o truncamento com a perda de dados, será postado um erro. Para datetime2, o número de dígitos de segundos fracionários (a escala) é determinado pelo tamanho da coluna de destino de acordo com a tabela a seguir. Para tamanhos de coluna maiores do que o intervalo na tabela, é sugerida uma escala de 9. Essa conversão deve permitir até nove dígitos de frações de segundo, o máximo permitido pelo OLE DB.<br /><br /> **Tipo:** DBTIME2<br /><br /> **Escala implícita 0** 8<br /><br /> **Escala implícita 1..9** 1..9<br /><br /> <br /><br /> **Tipo:** DBTIMESTAMP<br /><br /> **Escala implícita 0:** 19<br /><br /> **Escala implícita 1..9:** 21..29<br /><br /> <br /><br /> **Tipo:** DBTIMESTAMPOFFSET<br /><br /> **Escala implícita 0:** 26<br /><br /> **Escala implícita 1..9:** 28..36|  
|4|O componente de data é ignorado.|  
|5|O timezone é definido como UTC (por exemplo, 00:00).|  
|6|A hora é definida como zero.|  
|7|O componente date é definido como 1900-01-01.|  
|8|O deslocamento de timezone é ignorado.|  
|9|A cadeia de caracteres é analisada e convertida em um valor date, datetime, datetimeoffset ou time, dependendo do primeiro caractere de pontuação encontrado e da presença dos componentes restantes. A cadeia de caracteres é convertida no tipo de destino, seguindo as regras na tabela ao final deste tópico para o tipo de origem descoberto por esse processo. Se não for possível analisar sem erro os dados fornecidos ou se qualquer parte do componente estive fora do intervalo permitido ou ainda se não houver nenhuma conversão do tipo literal para o tipo de destino, será postado um erro (OLE DB) ou gerado um registro de diagnóstico de ODBC com SQLSTATE 22018 e a mensagem "Valor de caractere inválido para a especificação de difusão". Para os parâmetros datetime e smalldatetime, se o ano estiver fora do intervalo com suporte nesses tipos, será postado um erro (OLE DB) ou gerado um registro de diagnóstico de ODBC com SQLSATE 22007 e a mensagem "Formato de datetime inválido".<br /><br /> Para datetimeoffset, o valor deve estar dentro do intervalo após a conversão em UTC, mesmo que nenhuma conversão em UTC seja solicitada. O motivo disso é que o TDS e o servidor sempre normalizam a hora em valores datetimeoffset para UTC, por isso o cliente deve verificar se os componentes time estão dentro do intervalo com suporte após a conversão em UTC. Se o valor não estiver dentro do intervalo UTC com suporte, será postado um erro (OLE DB) ou gerado um registro de diagnóstico de ODBC com SQLSTATE 22007 e a mensagem "Formato de datetime inválido".|  
|10|Se ocorrer o truncamento com a perda de dados em uma conversão de cliente para servidor, será postado um erro (OLE DB) ou gerado um registro de diagnóstico de ODBC com SQLSTATE 22008 e a mensagem "Estouro no campo de data e hora". Esse erro também ocorrerá se o valor estiver fora do intervalo que pode ser representado pelo intervalo UTC usado pelo servidor. Se ocorrer o truncamento de segundos ou de segundos fracionários em uma conversão de cliente para servidor, somente um aviso será emitido.|  
|11|Se ocorrer o truncamento com a perda de dados, será gerado um registro de diagnóstico.<br /><br /> Em uma conversão de servidor para cliente, isso é uma advertência (ODBC SQLSTATE S1000).<br /><br /> Em uma conversão de cliente para servidor, isso é um erro (ODBC SQLSTATE 22001).|  
|12|Os segundos são definidos como zero e os segundos fracionários são descartados. Nenhum erro de truncamento é possível.|  
|N/D|O [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] existente e o comportamento anterior é mantido.|  
|||

## <a name="see-also"></a>Consulte Também  
 [Melhorias de data e hora &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)   
 [Melhorias de data e hora &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)  
