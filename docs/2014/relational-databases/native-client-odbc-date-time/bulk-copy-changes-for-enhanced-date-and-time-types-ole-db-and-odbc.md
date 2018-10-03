---
title: Em massa copia alterações para aprimorados tipos de data e hora (OLE DB e ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC, bulk copy operations
- bulk copy [ODBC], changes for date/time improvements
ms.assetid: c29e0f5e-9b3c-42b3-9856-755f4510832f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 23e4d815e7f351bcc0c0220e32ad13051a23d97b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48120026"
---
# <a name="bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc"></a>Alterações de cópia em massa para tipos de data e hora aprimorados (OLE DB e ODBC)
  Este tópico descreve os aprimoramentos de data/hora para oferecer suporte à funcionalidade de cópia em massa. As informações deste tópico são válidas para OLE DB e ODBC no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="format-files"></a>Arquivos de formato  
 Ao criar arquivos de formato interativamente, a tabela a seguir descreve a entrada usada para especificar os tipos de data/hora e os nomes de tipo de dados do arquivo de host correspondentes.  
  
|tipo de armazenamento de arquivo|Tipo de dados do arquivo host|Resposta ao aviso: "Insira o tipo de armazenamento de arquivos do campo <field_name> [\<default>]:"|  
|-----------------------|-------------------------|-----------------------------------------------------------------------------------------------------|  
|DATETIME|SQLDATETIME|d|  
|Smalldatetime|SQLDATETIM4|D|  
|data|SQLDATE|de|  
|Hora|SQLTIME|te|  
|Datetime2|SQLDATETIME2|d2|  
|Datetimeoffset|SQLDATETIMEOFFSET|do|  
  
 O XSD do arquivo de formato XML terá as adições a seguir:  
  
```  
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
 Em arquivos de dados de caractere, valores de data e hora são representados conforme descrito na seção "Formatos de dados: cadeias de caracteres e literais" de [suporte de tipo de dados para ODBC aprimoramentos de data e hora](data-type-support-for-odbc-date-and-time-improvements.md) para ODBC ou de [suporte ao tipo de dados para OLE DB aprimoramentos de data e hora](../native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md) para OLE DB.  
  
 Em arquivos de dados nativos, os valores de data e hora para os quatro novos tipos são representados como suas representações de TDS com uma escala de 7 (porque esse é o máximo com suporte pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e arquivos de dados bcp não armazenam a escala dessas colunas). Não há nenhuma alteração no armazenamento do existente `datetime` e `smalldatetime` seus dados tabulares ou tipo de fluxo de representações de (TDS).  
  
 Os tamanhos de armazenamento para os diferentes tipos de armazenamento do OLE DB são estes:  
  
|tipo de armazenamento de arquivo|Tamanho de armazenamento em bytes|  
|-----------------------|---------------------------|  
|DATETIME|8|  
|smalldatetime|4|  
|Data|3|  
|time|6|  
|datetime2|9|  
|datetimeoffset|11|  
  
 Os tamanhos para o ODBC são mostrados a seguir. Observe que não é necessário armazenar a precisão nem nos arquivos de formato nem nos de dados, porque o BCP.exe sempre recuperará a precisão do servidor.  
  
|tipo de armazenamento de arquivo|Tamanho de armazenamento em bytes|Formato de armazenamento|  
|-----------------------|---------------------------|--------------------|  
|datetime (d)|8|TDS|  
|smalldatetime (D)|4|TDS|  
|date (de)|3|TDS|  
|time (te)|6|TDS|  
|datetime2 (d2)|9|TDS|  
|datetimeoffset (do)|11|TDS|  
  
## <a name="bcp-types-in-sqlnclih"></a>Tipos BCP em sqlncli.h  
 Os tipos a seguir são definidos em sqlncli.h para ser usados com as extensões de API BCP para ODBC. Esses tipos são passados com a *eUserDataType* parâmetro do ibcpsession:: BCPColFmt no OLE DB.  
  
|tipo de armazenamento de arquivo|Tipo de dados do arquivo host|Digite SQLNCLI. h para uso com ibcpsession:: BCPColFmt|Valor|  
|-----------------------|-------------------------|-----------------------------------------------------------|-----------|  
|DATETIME|SQLDATETIME|BCP_TYPE_SQLDATETIME|0x3d|  
|Smalldatetime|SQLDATETIM4|BCP_TYPE_SQLDATETIME4|0x3a|  
|data|SQLDATE|BCP_TYPE_SQLDATE|0x28|  
|Hora|SQLTIME|BCP_TYPE_SQLTIME|0x29|  
|Datetime2|SQLDATETIME2|BCP_TYPE_SQLDATETIME2|0x2a|  
|Datetimeoffset|SQLDATETIMEOFFSET|BCP_TYPE_SQLDATETIMEOFFSET|0x2b|  
  
## <a name="bcp-data-type-conversions"></a>Conversões de tipo de dados BCP  
 As tabelas a seguir fornecem informações de conversão.  
  
 **Observação do OLE DB** As conversões a seguir são executadas por IBCPSession. IRowsetFastLoad usa conversões OLE DB conforme definido em [conversões executadas do cliente para o servidor](../native-client-ole-db-date-time/conversions-performed-from-client-to-server.md). Observe que os valores datetime são arredondados para 1/300 de um segundo e os valores smalldatetime têm os segundos definidos como zero depois de concluídas as conversões de cliente descritas a seguir. O arredondamento de datetime se propaga para horas e minutos, mas não para a data.  
  
|Para --><br /><br /> De|Data|time|smalldatetime|DATETIME|datetime2|datetimeoffset|char|wchar|  
|------------------------|----------|----------|-------------------|--------------|---------------|--------------------|----------|-----------|  
|data|1|-|1,6|1,6|1,6|1,5,6|1,3|1,3|  
|Hora|N/A|1,10|1,7,10|1,7,10|1,7,10|1,5,7,10|1,3|1,3|  
|Smalldatetime|1,2|1,4,10|1|1|1,10|1,5,10|1,11|1,11|  
|DATETIME|1,2|1,4,10|1,12|1|1,10|1,5,10|1,11|1,11|  
|Datetime2|1,2|1,4,10|1,10 (ODBC)1,12 (OLE DB)|1,10|1,10|1,5,10|1,3|1,3|  
|Datetimeoffset|1,2,8|1,4,8,10|1,8,10|1,8,10|1,8,10|1,10|1,3|1,3|  
|Char/wchar (date)|9|-|9,6 (ODBC)9,6,12 (OLE DB)|9,6 (ODBC)9,6,12 (OLE DB)|9,6|9,5,6|N/A|N/A|  
|Char/wchar (time)|-|9,10|9,7,10 (ODBC)9,7,10,12 (OLE DB)|9,7,10 (ODBC)9,7,10, 12 (OLE DB)|9,7,10|9,5,7,10|N/A|N/A|  
|Char/wchar (datetime)|9,2|9,4,10|9,10 (ODBC)9,10,12 (OLE DB)|9,10 (ODBC)9,10,12 (OLE DB)|9,10|9,5,10|N/A|N/A|  
|Char/wchar (datetimeoffset)|9,2,8|9,4,8,10|9,8,10 (ODBC)9,8,10,12 (OLE DB)|9,8,10 (ODBC)9,8,10,12 (OLE DB)|9,8,10|9,10|N/A|N/A|  
  
#### <a name="key-to-symbols"></a>Legenda dos símbolos  
  
|Símbolo|Significado|  
|------------|-------------|  
|-|Não há suporte a nenhuma conversão.<br /><br /> Será gerado um registro de diagnóstico de ODBC com SQLSTATE 07006 e a mensagem "Violação do atributo de tipo de dados restrito".|  
|1|Se os dados fornecidos não forem válidos, um registro de diagnóstico de ODBC será gerado com SQLSTATE 22007 e a mensagem "Formato de datetime inválido". Para valores datetimeoffset, a parte time deve estar dentro do intervalo após a conversão em UTC, mesmo que nenhuma conversão em UTC seja solicitada. O motivo disso é que o TDS e o servidor sempre normalizam a hora em valores datetimeoffset para UTC. Por isso, o cliente deve verificar se os componentes time estão dentro do intervalo com suporte após a conversão em UTC.|  
|2|O componente time é ignorado.|  
|3|Para ODBC, se ocorrer o truncamento com a perda de dados, será gerado um registro de diagnóstico com SQLSTATE 22001 e a mensagem 'Dados de cadeia de caracteres truncados à direita'. O número de dígitos de segundos fracionais (a escala) é determinado pelo tamanho da coluna de destino de acordo com a tabela a seguir. Para tamanhos de coluna maiores do que o intervalo na tabela, é sugerida uma escala de 7. Essa conversão deve permitir até nove dígitos de segundos fracionários, o máximo permitido pelo ODBC.<br /><br /> **Tipo:** DBTIME2<br /><br /> **Escala implícita 0** 8<br /><br /> **Escala 1..7 implícita** 10,16<br /><br /> <br /><br /> **Tipo:** DBTIMESTAMP<br /><br /> **Escala implícita 0:** 19<br /><br /> **Escala 1..7 implícita:** 21..27<br /><br /> <br /><br /> **Tipo:** DBTIMESTAMPOFFSET<br /><br /> **Escala implícita 0:** 26<br /><br /> **Escala 1..7 implícita:** 28..34<br /><br /> Para OLE DB, se ocorrer o truncamento com a perda de dados, será postado um erro. Para datetime2, o número de dígitos de segundos fracionários (a escala) é determinado pelo tamanho da coluna de destino de acordo com a tabela a seguir. Para tamanhos de coluna maiores do que o intervalo na tabela, é sugerida uma escala de 9. Essa conversão deve permitir até nove dígitos de frações de segundo, o máximo permitido pelo OLE DB.<br /><br /> **Tipo:** DBTIME2<br /><br /> **Escala implícita 0** 8<br /><br /> **Escala implícita 1..9** 1..9<br /><br /> <br /><br /> **Tipo:** DBTIMESTAMP<br /><br /> **Escala implícita 0:** 19<br /><br /> **Escala implícita 1..9:** 21..29<br /><br /> <br /><br /> **Tipo:** DBTIMESTAMPOFFSET<br /><br /> **Escala implícita 0:** 26<br /><br /> **Escala implícita 1..9:** 28..36|  
|4|O componente de data é ignorado.|  
|5|O timezone é definido como UTC (por exemplo, 00:00).|  
|6|A hora é definida como zero.|  
|7|O componente date é definido como 1900-01-01.|  
|8|O deslocamento de timezone é ignorado.|  
|9|A cadeia de caracteres é analisada e convertida em um valor date, datetime, datetimeoffset ou time, dependendo do primeiro caractere de pontuação encontrado e da presença dos componentes restantes. A cadeia de caracteres é convertida no tipo de destino, seguindo as regras na tabela ao final deste tópico para o tipo de origem descoberto por esse processo. Se não for possível analisar sem erro os dados fornecidos ou se qualquer parte do componente estive fora do intervalo permitido ou ainda se não houver nenhuma conversão do tipo literal para o tipo de destino, será postado um erro (OLE DB) ou gerado um registro de diagnóstico de ODBC com SQLSTATE 22018 e a mensagem "Valor de caractere inválido para a especificação de difusão". Para os parâmetros datetime e smalldatetime, se o ano estiver fora do intervalo com suporte nesses tipos, será postado um erro (OLE DB) ou gerado um registro de diagnóstico de ODBC com SQLSATE 22007 e a mensagem "Formato de datetime inválido".<br /><br /> Para datetimeoffset, o valor deve estar dentro do intervalo após a conversão em UTC, mesmo que nenhuma conversão em UTC seja solicitada. O motivo disso é que o TDS e o servidor sempre normalizam a hora em valores datetimeoffset para UTC, por isso o cliente deve verificar se os componentes time estão dentro do intervalo com suporte após a conversão em UTC. Se o valor não estiver dentro do intervalo UTC com suporte, será postado um erro (OLE DB) ou gerado um registro de diagnóstico de ODBC com SQLSTATE 22007 e a mensagem "Formato de datetime inválido".|  
|10|Se ocorrer o truncamento com a perda de dados em uma conversão de cliente para servidor, será postado um erro (OLE DB) ou gerado um registro de diagnóstico de ODBC com SQLSTATE 22008 e a mensagem "Estouro no campo de data e hora". Esse erro também ocorrerá se o valor estiver fora do intervalo que pode ser representado pelo intervalo UTC usado pelo servidor. Se ocorrer o truncamento de segundos ou de segundos fracionários em uma conversão de cliente para servidor, somente um aviso será emitido.|  
|11|Se ocorrer o truncamento com a perda de dados, será gerado um registro de diagnóstico.<br /><br /> Em uma conversão de servidor para cliente, isso é uma advertência (ODBC SQLSTATE S1000).<br /><br /> Em uma conversão de cliente para servidor, isso é um erro (ODBC SQLSTATE 22001).|  
|12|Os segundos são definidos como zero e os segundos fracionários são descartados. Nenhum erro de truncamento é possível.|  
|N/A|O [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] existente e o comportamento anterior é mantido.|  
  
## <a name="see-also"></a>Consulte também  
 [Aprimoramentos de data e hora &#40;ODBC&#41;](date-and-time-improvements-odbc.md)   
 [Melhorias de data e hora &#40;OLE DB&#41;](../native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
