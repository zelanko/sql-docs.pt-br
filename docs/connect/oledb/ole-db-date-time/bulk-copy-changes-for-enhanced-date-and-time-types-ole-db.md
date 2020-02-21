---
title: Alterações de cópia em massa para tipos avançados de data e hora (OLE DB) | Microsoft Docs
description: Alterações de cópia em massa para tipos avançados de data e hora (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB, bulk copy operations
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 417bf44993ffc850da03d090e36c29cae472c104
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "68015827"
---
# <a name="bulk-copy-changes-for-enhanced-date-and-time-types-ole-db"></a>Alterações de cópia em massa para tipos avançados de data e hora (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Este artigo descreve as melhorias de data/hora para oferecer suporte à funcionalidade de cópia em massa no Driver do OLE DB para SQL Server.  
  
## <a name="format-files"></a>Arquivos de formato  
 Ao criar arquivos de formato interativamente, a tabela a seguir descreve a entrada usada para especificar os tipos de data/hora e os nomes de tipo de dados do arquivo de host correspondentes.  
  
|tipo de armazenamento de arquivo|Tipo de dados do arquivo host|Resposta à solicitação: "Insira o tipo de armazenamento de arquivo do campo <nome_do_campo> [\<padrão>]:"|  
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
 Em arquivos de dados de caractere, valores de data e hora são representados conforme descrito na seção "Formatos de dados: cadeias de caracteres e literais" em [Suporte a tipo de dados para aprimoramentos de data e hora do OLE DB](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md) para OLE DB.  
  
 Em arquivos de dados nativos, os valores de data e os valores temporais para os quatro novos tipos são mostrados como suas representações TDS com uma escala de 7 (porque esse é o máximo com suporte no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e os arquivos de dados bcp não armazenam a escala dessas colunas). Não há nenhuma alteração no armazenamento dos tipos **datetime** e **smalldatetime** existentes nem em suas representações do protocolo TDS.  
  
 Os tamanhos de armazenamento para os diferentes tipos de armazenamento do OLE DB são estes:  
  
|tipo de armazenamento de arquivo|Tamanho de armazenamento em bytes|  
|-----------------------|---------------------------|  
|DATETIME|8|  
|smalldatetime|4|  
|date|3|  
|time|6|  
|datetime2|9|  
|datetimeoffset|11|  
 
  
## <a name="bcp-types-in-msoledbsqlh"></a>Tipos BCP em msoledbsql.h  
 Os tipos a seguir estão definidos em msoledbsql.h. Esses tipos são passados com o parâmetro *eUserDataType* do método IBCPSession::BCPColFmt no OLE DB.  
  
|tipo de armazenamento de arquivo|Tipo de dados do arquivo host|Digite msoledbsql.h para uso com o método IBCPSession:: BCPColFmt|Valor|  
|-----------------------|-------------------------|-----------------------------------------------------------|-----------|  
|Datetime|SQLDATETIME|BCP_TYPE_SQLDATETIME|0x3d|  
|Smalldatetime|SQLDATETIM4|BCP_TYPE_SQLDATETIM4|0x3a|  
|Data|SQLDATE|BCP_TYPE_SQLDATE|0x28|  
|Hora|SQLTIME|BCP_TYPE_SQLTIME|0x29|  
|Datetime2|SQLDATETIME2|BCP_TYPE_SQLDATETIME2|0x2a|  
|Datetimeoffset|SQLDATETIMEOFFSET|BCP_TYPE_SQLDATETIMEOFFSET|0x2b|  
  
## <a name="bcp-data-type-conversions"></a>Conversões de tipo de dados BCP  
 As tabelas a seguir fornecem informações de conversão.  
  
 **Observação do OLE DB** As conversões a seguir são executadas por IBCPSession. O IRowsetFastLoad usa conversões OLE DB conforme definido em [Conversões realizadas de Cliente para Servidor](../../oledb/ole-db-date-time/conversions-performed-from-client-to-server.md). Observe que os valores datetime são arredondados para 1/300 de um segundo e os valores smalldatetime têm os segundos definidos como zero depois de concluídas as conversões de cliente descritas a seguir. O arredondamento de datetime se propaga para horas e minutos, mas não para a data.  
  
|Para --><br /><br /> De|date|time|smalldatetime|DATETIME|datetime2|datetimeoffset|char|wchar|  
|------------------------|----------|----------|-------------------|--------------|---------------|--------------------|----------|-----------|  
|Data|1|-|1, 6|1, 6|1, 6|1, 5, 6|1, 3|1, 3|  
|Hora|N/D|1, 10|1, 7, 10|1, 7, 10|1, 7, 10|1, 5, 7, 10|1, 3|1, 3|  
|Smalldatetime|1, 2|1, 4, 10|1|1|1, 10|1, 5, 10|1, 11|1, 11|  
|Datetime|1, 2|1, 4, 10|1, 12|1|1, 10|1, 5, 10|1, 11|1, 11|  
|Datetime2|1, 2|1, 4, 10|1, 12|1, 10|1, 10|1, 5, 10|1, 3|1, 3|  
|Datetimeoffset|1, 2, 8|1, 4, 8, 10|1, 8, 10|1, 8, 10|1, 8, 10|1, 10|1, 3|1, 3|  
|Char/wchar (date)|9|-|9, 6, 12|9, 6, 12|9, 6|9, 5, 6|N/D|N/D|  
|Char/wchar (time)|-|9, 10|9, 7, 10, 12|9, 7, 10, 12|9, 7, 10|9, 5, 7, 10|N/D|N/D|  
|Char/wchar (datetime)|9, 2|9, 4, 10|9, 10, 12|9, 10, 12|9, 10|9, 5, 10|N/D|N/D|  
|Char/wchar (datetimeoffset)|9, 2, 8|9, 4, 8, 10|9, 8, 10, 12|9, 8, 10, 12|9, 8, 10|9, 10|N/D|N/D|  
  
#### <a name="key-to-symbols"></a>Legenda dos símbolos  
  
|Símbolo|Significado|  
|------------|-------------|  
|-|Não há suporte a nenhuma conversão.<br />|  
|1|Se os dados fornecidos não forem válidos, um erro será postado. Para valores datetimeoffset, a parte time deve estar dentro do intervalo após a conversão em UTC, mesmo que nenhuma conversão em UTC seja solicitada. O motivo disso é que o TDS e o servidor sempre normalizam a hora em valores datetimeoffset para UTC. Por isso, o cliente deve verificar se os componentes time estão dentro do intervalo com suporte após a conversão em UTC.|  
|2|O componente time é ignorado.|  
|3|Se ocorrer truncamento com perda de dados, será postado um erro. Para datetime2, o número de dígitos de segundos fracionários (a escala) é determinado pelo tamanho da coluna de destino de acordo com a tabela a seguir. Para tamanhos de coluna maiores do que o intervalo na tabela, é sugerida uma escala de 9. Essa conversão deve permitir até nove dígitos de frações de segundo, o máximo permitido pelo OLE DB.<br /><br /> **Tipo:** DBTIME2<br /><br /> **Escala implícita 0** 8<br /><br /> **Escala implícita 1..9** 1..9<br /><br /> <br /><br /> **Tipo:** DBTIMESTAMP<br /><br /> **Escala implícita 0:** 19<br /><br /> **Escala implícita 1..9:** 21..29<br /><br /> <br /><br /> **Tipo:** DBTIMESTAMPOFFSET<br /><br /> **Escala implícita 0:** 26<br /><br /> **Escala implícita 1..9:** 28..36|  
|4|O componente de data é ignorado.|  
|5|O timezone é definido como UTC (por exemplo, 00:00).|  
|6|A hora é definida como zero.|  
|7|O componente date é definido como 1900-01-01.|  
|8|O deslocamento de timezone é ignorado.|  
|9|A cadeia de caracteres é analisada e convertida em um valor date, datetime, datetimeoffset ou time, dependendo do primeiro caractere de pontuação encontrado e da presença dos componentes restantes. A cadeia de caracteres é então convertida no tipo de destino, seguindo as regras da tabela ao final deste artigo para o tipo de origem descoberto por esse processo. Se não for possível analisar sem erro os dados fornecidos ou se qualquer parte do componente estive fora do intervalo permitido ou ainda se não houver nenhuma conversão do tipo literal para o tipo de destino, será postado um erro. Para os parâmetros datetime e smalldatetime, se o ano estiver fora do intervalo compatível com esses tipos, um erro será postado.<br /><br /> Para datetimeoffset, o valor deve estar dentro do intervalo após a conversão em UTC, mesmo que nenhuma conversão em UTC seja solicitada. O motivo disso é que o TDS e o servidor sempre normalizam a hora em valores datetimeoffset para UTC, por isso o cliente deve verificar se os componentes time estão dentro do intervalo com suporte após a conversão em UTC. Se o valor não estiver dentro do intervalo UTC compatível, um erro será postado.|  
|10|Para conversões de cliente para servidor, se ocorrer truncamento com perda de dados, será postado um erro. Esse erro também ocorrerá se o valor estiver fora do intervalo que pode ser representado pelo intervalo UTC usado pelo servidor. Se ocorrer o truncamento de segundos ou de segundos fracionários em uma conversão de cliente para servidor, somente um aviso será emitido.|  
|11|Para conversões de cliente para servidor, se ocorrer truncamento com perda de dados, será postado um erro.|
|12|Os segundos são definidos como zero e os segundos fracionários são descartados. Nenhum erro de truncamento é possível.|  
|N/D|O [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] existente e o comportamento anterior é mantido.|  
  
## <a name="see-also"></a>Consulte Também     
 [Melhorias de data e hora &#40;OLE DB&#41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
