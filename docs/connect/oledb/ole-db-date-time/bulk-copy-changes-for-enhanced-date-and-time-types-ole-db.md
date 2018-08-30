---
title: Alterações de cópia em massa para tipos avançados de data e hora (OLE DB) | Microsoft Docs
description: Alterações de cópia em massa para tipos avançados de data e hora (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, bulk copy operations
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 16ab7dd1f4a083c51108ef86ff9c9428df1649da
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43029555"
---
# <a name="bulk-copy-changes-for-enhanced-date-and-time-types-ole-db"></a>Alterações de cópia em massa para tipos avançados de data e hora (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Este artigo descreve os aprimoramentos de data/hora para dar suporte à funcionalidade de cópia em massa no Driver do OLE DB para SQL Server.  
  
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
 Em arquivos de dados de caractere, valores de data e hora são representados conforme descrito na seção "Formatos de dados: cadeias de caracteres e literais" de [suporte de tipo de dados para OLE DB aprimoramentos de data e hora](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md) para OLE DB.  
  
 Em arquivos de dados nativos, os valores de data e os valores temporais para os quatro novos tipos são mostrados como suas representações TDS com uma escala de 7 (porque esse é o máximo com suporte no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e os arquivos de dados bcp não armazenam a escala dessas colunas). Não há nenhuma alteração no armazenamento dos tipos **datetime** e **smalldatetime** existentes nem em suas representações do protocolo TDS.  
  
 Os tamanhos de armazenamento para os diferentes tipos de armazenamento do OLE DB são estes:  
  
|tipo de armazenamento de arquivo|Tamanho de armazenamento em bytes|  
|-----------------------|---------------------------|  
|DATETIME|8|  
|smalldatetime|4|  
|Data|3|  
|time|6|  
|datetime2|9|  
|datetimeoffset|11|  
 
  
## <a name="bcp-types-in-msoledbsqlh"></a>Tipos BCP em msoledbsql.h  
 Os seguintes tipos são definidos em msoledbsql.h. Esses tipos são passados com a *eUserDataType* parâmetro do ibcpsession:: BCPColFmt no OLE DB.  
  
|tipo de armazenamento de arquivo|Tipo de dados do arquivo host|Digite msoledbsql.h para uso com ibcpsession:: BCPColFmt|Valor|  
|-----------------------|-------------------------|-----------------------------------------------------------|-----------|  
|DATETIME|SQLDATETIME|BCP_TYPE_SQLDATETIME|0x3d|  
|Smalldatetime|SQLDATETIM4|BCP_TYPE_SQLDATETIM4|0x3a|  
|data|SQLDATE|BCP_TYPE_SQLDATE|0x28|  
|Hora|SQLTIME|BCP_TYPE_SQLTIME|0x29|  
|Datetime2|SQLDATETIME2|BCP_TYPE_SQLDATETIME2|0x2a|  
|Datetimeoffset|SQLDATETIMEOFFSET|BCP_TYPE_SQLDATETIMEOFFSET|0x2b|  
  
## <a name="bcp-data-type-conversions"></a>Conversões de tipo de dados BCP  
 As tabelas a seguir fornecem informações de conversão.  
  
 **Observação do OLE DB** As conversões a seguir são executadas por IBCPSession. IRowsetFastLoad usa conversões OLE DB conforme definido em [conversões executadas do cliente para o servidor](../../oledb/ole-db-date-time/conversions-performed-from-client-to-server.md). Observe que os valores datetime são arredondados para 1/300 de um segundo e os valores smalldatetime têm os segundos definidos como zero depois de concluídas as conversões de cliente descritas a seguir. O arredondamento de datetime se propaga para horas e minutos, mas não para a data.  
  
|Para --><br /><br /> De|Data|time|smalldatetime|DATETIME|datetime2|datetimeoffset|char|wchar|  
|------------------------|----------|----------|-------------------|--------------|---------------|--------------------|----------|-----------|  
|data|1|-|1, 6|1, 6|1, 6|1, 5, 6|1, 3|1, 3|  
|Hora|N/A|1, 10|1, 7, 10|1, 7, 10|1, 7, 10|1, 5, 7, 10|1, 3|1, 3|  
|Smalldatetime|1, 2|1, 4, 10|1|1|1, 10|1, 5, 10|1, 11|1, 11|  
|DATETIME|1, 2|1, 4, 10|1, 12|1|1, 10|1, 5, 10|1, 11|1, 11|  
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
|3|Se ocorrer truncamento com perda de dados, será postado um erro. Para datetime2, o número de dígitos de segundos fracionários (a escala) é determinado pelo tamanho da coluna de destino de acordo com a tabela a seguir. Para tamanhos de coluna maiores do que o intervalo na tabela, é sugerida uma escala de 9. Essa conversão deve permitir até nove dígitos de frações de segundo, o máximo permitido pelo OLE DB.<br /><br /> **Tipo:** DBTIME2<br /><br /> **Escala implícita 0** 8<br /><br /> **Escala implícita 1..9** 1..9<br /><br /> <br /><br /> **Tipo:** DBTIMESTAMP<br /><br /> **Escala implícita 0:** 19<br /><br /> **Escala implícita 1..9:** 21..29<br /><br /> <br /><br /> **Tipo:** DBTIMESTAMPOFFSET<br /><br /> **Escala implícita 0:** 26<br /><br /> **Escala implícita 1..9:** 28..36|  
|4|O componente de data é ignorado.|  
|5|O timezone é definido como UTC (por exemplo, 00:00).|  
|6|A hora é definida como zero.|  
|7|O componente date é definido como 1900-01-01.|  
|8|O deslocamento de timezone é ignorado.|  
|9|A cadeia de caracteres é analisada e convertida em um valor date, datetime, datetimeoffset ou time, dependendo do primeiro caractere de pontuação encontrado e da presença dos componentes restantes. A cadeia de caracteres é então convertida no tipo de destino, seguindo as regras da tabela ao final deste artigo para o tipo de origem descoberto por esse processo. Se os dados fornecidos não podem ser analisados sem erro, ou se qualquer parte do componente estiver fora do intervalo permitido, ou se não houver nenhuma conversão do tipo de literal para o tipo de destino, será postado um erro. Para os parâmetros datetime e smalldatetime, se o ano estiver fora do intervalo de que dar suporte a esses tipos, será postado um erro.<br /><br /> Para datetimeoffset, o valor deve estar dentro do intervalo após a conversão em UTC, mesmo que nenhuma conversão em UTC seja solicitada. O motivo disso é que o TDS e o servidor sempre normalizam a hora em valores datetimeoffset para UTC, por isso o cliente deve verificar se os componentes time estão dentro do intervalo com suporte após a conversão em UTC. Se o valor não está dentro do intervalo UTC com suporte, um erro será lançado.|  
|10|Para conversões de servidor cliente, se ocorrer truncamento com perda de dados será postado um erro. Esse erro também ocorrerá se o valor estiver fora do intervalo que pode ser representado pelo intervalo UTC usado pelo servidor. Se ocorrer o truncamento de segundos ou de segundos fracionários em uma conversão de cliente para servidor, somente um aviso será emitido.|  
|11|Para conversões de servidor cliente, se ocorrer truncamento com perda de dados será postado um erro.|
|12|Os segundos são definidos como zero e os segundos fracionários são descartados. Nenhum erro de truncamento é possível.|  
|N/A|O [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] existente e o comportamento anterior é mantido.|  
  
## <a name="see-also"></a>Consulte Também     
 [Melhorias de data e hora &#40;OLE DB&#41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
