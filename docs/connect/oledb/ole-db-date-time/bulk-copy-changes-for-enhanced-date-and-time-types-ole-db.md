---
title: Em massa copia alterações para aprimorados tipos de data e hora (OLE DB) | Microsoft Docs
description: Alterações de cópia em massa para aprimorados tipos de data e hora (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, bulk copy operations
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 45d2688be6c45f299d6f3e8d6868f40874c89354
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="bulk-copy-changes-for-enhanced-date-and-time-types-ole-db"></a>Alterações de cópia em massa para aprimorados tipos de data e hora (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Este artigo descreve os aprimoramentos de data/hora para dar suporte à funcionalidade de cópia em massa no Driver do OLE DB para SQL Server.  
  
## <a name="format-files"></a>Arquivos de formato  
 Ao criar arquivos de formato interativamente, a tabela a seguir descreve a entrada usada para especificar os tipos de data/hora e os nomes de tipo de dados do arquivo de host correspondentes.  
  
|tipo de armazenamento de arquivo|Tipo de dados do arquivo host|Resposta à solicitação: "digite o tipo de armazenamento de arquivo do campo < nome_do_campo > [\<padrão >]:"|  
|-----------------------|-------------------------|-----------------------------------------------------------------------------------------------------|  
|Datetime|SQLDATETIME|d|  
|Smalldatetime|SQLDATETIM4|D|  
|Data|SQLDATE|de|  
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
 Em arquivos de dados de caractere, valores de data e hora são representados como descrito na seção "Formatos de dados: cadeias e literais" de [suporte de tipo de dados para aprimoramentos de hora e data do OLE DB](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md) para OLE DB.  
  
 Nos arquivos de dados nativos, os valores de data e hora para os quatro novos tipos são representados como suas representações de TDS com uma escala de 7 (porque esse é o máximo suportado pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e arquivos de dados bcp não armazenam a escala dessas colunas). Não há nenhuma alteração no armazenamento do existente **datetime** e **smalldatetime** representações (TDS) de fluxo de tipo ou seus dados tabulares.  
  
 Os tamanhos de armazenamento para os diferentes tipos de armazenamento do OLE DB são estes:  
  
|tipo de armazenamento de arquivo|Tamanho de armazenamento em bytes|  
|-----------------------|---------------------------|  
|datetime|8|  
|smalldatetime|4|  
|date|3|  
|time|6|  
|datetime2|9|  
|datetimeoffset|11|  
 
  
## <a name="bcp-types-in-msoledbsqlh"></a>Tipos BCP em msoledbsql.h  
 Os seguintes tipos são definidos no msoledbsql.h. Esses tipos são passados com o *eUserDataType* parâmetro ibcpsession:: BCPColFmt no OLE DB.  
  
|tipo de armazenamento de arquivo|Tipo de dados do arquivo host|Digite msoledbsql.h para uso com ibcpsession:: BCPColFmt|Value|  
|-----------------------|-------------------------|-----------------------------------------------------------|-----------|  
|Datetime|SQLDATETIME|BCP_TYPE_SQLDATETIME|0x3d|  
|Smalldatetime|SQLDATETIM4|BCP_TYPE_SQLDATETIM4|0x3a|  
|Data|SQLDATE|BCP_TYPE_SQLDATE|0x28|  
|Hora|SQLTIME|BCP_TYPE_SQLTIME|0x29|  
|Datetime2|SQLDATETIME2|BCP_TYPE_SQLDATETIME2|0x2a|  
|Datetimeoffset|SQLDATETIMEOFFSET|BCP_TYPE_SQLDATETIMEOFFSET|0x2b|  
  
## <a name="bcp-data-type-conversions"></a>Conversões de tipo de dados BCP  
 As tabelas a seguir fornecem informações de conversão.  
  
 **Observação do OLE DB** as conversões a seguir são executadas por IBCPSession. IRowsetFastLoad usa conversões OLE DB conforme definido em [conversões executadas do cliente para servidor](../../oledb/ole-db-date-time/conversions-performed-from-client-to-server.md). Observe que os valores datetime são arredondados para 1/300 de um segundo e os valores smalldatetime têm os segundos definidos como zero depois de concluídas as conversões de cliente descritas a seguir. O arredondamento de datetime se propaga para horas e minutos, mas não para a data.  
  
|Para --><br /><br /> De|date|time|smalldatetime|datetime|datetime2|datetimeoffset|char|wchar|  
|------------------------|----------|----------|-------------------|--------------|---------------|--------------------|----------|-----------|  
|Data|1|-|1, 6|1, 6|1, 6|1, 5, 6|1, 3|1, 3|  
|Hora|N/A|1, 10|1, 7, 10|1, 7, 10|1, 7, 10|1, 5, 7, 10|1, 3|1, 3|  
|Smalldatetime|1, 2|1, 4, 10|1|1|1, 10|1, 5, 10|1, 11|1, 11|  
|Datetime|1, 2|1, 4, 10|1, 12|1|1, 10|1, 5, 10|1, 11|1, 11|  
|Datetime2|1, 2|1, 4, 10|1, 12|1, 10|1, 10|1, 5, 10|1, 3|1, 3|  
|Datetimeoffset|1, 2, 8|1, 4, 8, 10|1, 8, 10|1, 8, 10|1, 8, 10|1, 10|1, 3|1, 3|  
|Char/wchar (date)|9|-|9, 6, 12|9, 6, 12|9, 6|9, 5, 6|N/A|N/A|  
|Char/wchar (time)|-|9, 10|9, 7, 10, 12|9, 7, 10, 12|9, 7, 10|9, 5, 7, 10|N/A|N/A|  
|Char/wchar (datetime)|9, 2|9, 4, 10|9, 10, 12|9, 10, 12|9, 10|9, 5, 10|N/A|N/A|  
|Char/wchar (datetimeoffset)|9, 2, 8|9, 4, 8, 10|9, 8, 10, 12|9, 8, 10, 12|9, 8, 10|9, 10|N/A|N/A|  
  
#### <a name="key-to-symbols"></a>Legenda dos símbolos  
  
|Símbolo|Significado|  
|------------|-------------|  
|-|Não há suporte a nenhuma conversão.<br />|  
|1|Se os dados fornecidos não são válidos, um erro será lançado. Para valores datetimeoffset, a parte time deve estar dentro do intervalo após a conversão em UTC, mesmo que nenhuma conversão em UTC seja solicitada. O motivo disso é que o TDS e o servidor sempre normalizam a hora em valores datetimeoffset para UTC. Por isso, o cliente deve verificar se os componentes time estão dentro do intervalo com suporte após a conversão em UTC.|  
|2|O componente time é ignorado.|  
|3|Se ocorrer o truncamento com perda de dados, um erro será lançado. Para datetime2, o número de dígitos de segundos fracionários (a escala) é determinado pelo tamanho da coluna de destino de acordo com a tabela a seguir. Para tamanhos de coluna maiores do que o intervalo na tabela, é sugerida uma escala de 9. Essa conversão deve permitir até nove dígitos de frações de segundo, o máximo permitido pelo OLE DB.<br /><br /> **Tipo:** DBTIME2<br /><br /> **Implícito na escala de 0** 8<br /><br /> **Implícito na escala 1..9** 1..9<br /><br /> <br /><br /> **Tipo:** DBTIMESTAMP<br /><br /> **Implícito na escala de 0:** 19<br /><br /> **Implícito na escala 1..9:** 21..29<br /><br /> <br /><br /> **Tipo:** DBTIMESTAMPOFFSET<br /><br /> **Implícito na escala de 0:** 26<br /><br /> **Implícito na escala 1..9:** 28..36|  
|4|O componente de data é ignorado.|  
|5|O timezone é definido como UTC (por exemplo, 00:00).|  
|6|A hora é definida como zero.|  
|7|O componente date é definido como 1900-01-01.|  
|8|O deslocamento de timezone é ignorado.|  
|9|A cadeia de caracteres é analisada e convertida em um valor date, datetime, datetimeoffset ou time, dependendo do primeiro caractere de pontuação encontrado e da presença dos componentes restantes. A cadeia de caracteres é convertida para o tipo de destino, seguindo as regras na tabela no final deste artigo para o tipo de origem descoberto por esse processo. Se os dados fornecidos não podem ser analisados sem erro, ou se qualquer parte do componente está fora do intervalo permitido, ou se não houver nenhuma conversão de tipo de literal para o tipo de destino, será postado um erro. Para os parâmetros datetime e smalldatetime, se o ano estiver fora do intervalo de que oferecer suporte a esses tipos, um erro será lançado.<br /><br /> Para datetimeoffset, o valor deve estar dentro do intervalo após a conversão em UTC, mesmo que nenhuma conversão em UTC seja solicitada. O motivo disso é que o TDS e o servidor sempre normalizam a hora em valores datetimeoffset para UTC, por isso o cliente deve verificar se os componentes time estão dentro do intervalo com suporte após a conversão em UTC. Se o valor não está dentro do intervalo UTC com suporte, um erro será lançado.|  
|10|Para conversões de servidor cliente, se ocorrer truncamento com perda de dados será postado um erro. Esse erro também ocorrerá se o valor estiver fora do intervalo que pode ser representado pelo intervalo UTC usado pelo servidor. Se ocorrer o truncamento de segundos ou de segundos fracionários em uma conversão de cliente para servidor, somente um aviso será emitido.|  
|11|Para conversões de servidor cliente, se ocorrer truncamento com perda de dados será postado um erro.|
|12|Os segundos são definidos como zero e os segundos fracionários são descartados. Nenhum erro de truncamento é possível.|  
|N/A|O [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] existente e o comportamento anterior é mantido.|  
  
## <a name="see-also"></a>Consulte também     
 [Data e hora melhorias & #40; OLE DB & #41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
