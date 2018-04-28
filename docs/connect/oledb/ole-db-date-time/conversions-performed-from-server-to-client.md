---
title: Conversões executadas do servidor para cliente | Microsoft Docs
description: Conversões executadas do servidor para o cliente
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
- conversions [OLE DB], server to client
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 52b1a92e30f0b90f2ade7315b9cc3e6e67f05abc
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="conversions-performed-from-server-to-client"></a>Conversões executadas do servidor para o cliente
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Este artigo descreve conversões de data/hora executadas entre [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] (ou posterior) e um aplicativo cliente escrito com o Driver do OLE DB para SQL Server.  
  
## <a name="conversions"></a>Conversões  
 A tabela a seguir descreve conversões entre o tipo retornado para o cliente e o tipo na associação. Parâmetros de saída, se ICommandWithParameters:: SetParameterInfo foi chamado e o tipo especificado em *pwszDataSourceType* não corresponde ao tipo real no servidor, uma conversão implícita será executado pelo servidor , e o tipo retornado para o cliente corresponderá ao tipo especificado por meio de ICommandWithParameters:: SetParameterInfo. Isso pode levar a resultados de conversão inesperados quando as regras de conversão do servidor são diferentes daqueles descritos neste artigo. Por exemplo, quando é necessário fornecer uma data padrão, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa 1/1/1900 em vez de 30/12/1899.  
  
|Para -><br /><br /> De|DATE|DBDATE|DBTIME|DBTIME2|DBTIMESTAMP|DBTIMESTAMPOFFSET|FILETIME|BYTES|VARIANT|SSVARIANT|BSTR|STR|WSTR|  
|----------------------|----------|------------|------------|-------------|-----------------|-----------------------|--------------|-----------|-------------|---------------|----------|---------|----------|  
|Data|1, 7|OK|-|-|1|1, 3|1, 7|-|OK (VT_BSTR)|OK|OK|4|4|  
|Hora|5, 6, 7|-|9|OK|6|3, 6|5, 6|-|OK (VT_BSTR)|OK|OK|4|4|  
|Smalldatetime|7|8|9, 10|10|OK|3|7|-|7 (VT_DATE)|OK|OK|4|4|  
|Datetime|5, 7|8|9, 10|10|OK|3|7|-|7 (VT_DATE)|OK|OK|4|4|  
|Datetime2|5, 7|8|9, 10|10|7|3|5, 7|-|OK (VT_BSTR)|OK|OK|4|4|  
|Datetimeoffset|5, 7, 11|8, 11|9, 10, 11|10, 11|7, 11|OK|5, 7, 11|-|OK (VT_BSTR)|OK|OK|4|4|  
|Char, Varchar,<br /><br /> Nchar, Nvarchar|7, 13|12|12, 9|12|12|12|7, 13|N/A|N/A|N/A|N/A|N/A|N/A|  
|Sql_variant<br /><br /> (datetime)|7|8|9, 10|10|OK|3|7|-|7(VT_DATE)|OK|OK|4|4|  
|Sql_variant<br /><br /> (smalldatetime)|7|8|9, 10|10|OK|3|7|-|7(VT_DATE)|OK|OK|4|4|  
|Sql_variant<br /><br /> (date)|1, 7|OK|2|2|1|1, 3|1, 7|-|OK(VT_BSTR)|OK|OK|4|4|  
|Sql_variant<br /><br /> (time)|5, 6, 7|2|6|OK|6|3, 6|5, 6|-|OK(VT_BSTR)|OK|OK|4|4|  
|Sql_variant<br /><br /> (datetime2)|5, 7|8|9, 10|10|OK|3|5, 7|-|OK(VT_BSTR)|OK|OK|4|4|  
|Sql_variant<br /><br /> (datetimeoffset)|5, 7, 11|8, 11|9, 10, 11|10, 11|7, 11|OK|5, 7, 11|-|OK(VT_BSTR)|OK|OK|4|4|  
  
## <a name="key-to-symbols"></a>Legenda dos símbolos  
  
|Símbolo|Significado|  
|------------|-------------|  
|OK|Nenhuma conversão é necessária.|  
|-|Não há suporte a nenhuma conversão. Se a associação for validada quando IAccessor:: CreateAccessor é chamado, DBBINDSTATUS_UPSUPPORTEDCONVERSION será retornado em *rgStatus*. Quando a validação de acessador for adiada, DBSTATUS_E_BADACCESSOR será definido.|  
|1|Os campos de hora são definidos como zero.|  
|2|DBSTATUS_E_CANTCONVERTVALUE é definido.|  
|3|O fuso horário é definido como zero.|  
|4|Se o buffer do cliente não suficientemente grande, DBSTATUS_S_TRUNCATED será definido. Quando o tipo de servidor inclui frações de segundo, o número de dígitos na cadeia de caracteres de resultado corresponde exatamente à escala do tipo de servidor.|  
|5|O truncamento de segundos ou de frações de segundo é ignorado.|  
|6|A data é definida como a data atual, a menos que a origem seja uma literal de hora da cadeia de caracteres e o destino seja DBTYPE_DATE. Nesse caso, será usado 30/12/1899.|  
|7|Se o valor alagar, DBSTATUS_E_DATAOVERFLOW será definido.|  
|8|Os campos de hora são ignorados.|  
|9|Os campos de frações de segundo são ignorados.|  
|10|O componente de data é ignorado.|  
|11|A hora é convertida para o fuso horário do cliente. Se ocorrer um erro durante essa conversão, DBSTATUS_E_DATAOVERFLOW será definido.|  
|12|A cadeia de caracteres é analisada como um literal ISO e convertida para o tipo de destino. Se houver falha, a cadeia de caracteres será analisada como um literal de data OLE (que também tem componentes de hora) e convertida de uma data OLE (DBTYPE_DATE) para o tipo de destino. A cadeia de caracteres deverá se conformar com a sintaxe para literais do tipo de destino permitido para que a análise do formato ISO tenha êxito. Para que a análise de OLE tenha êxito, a cadeia de caracteres deve se conformar com a sintaxe reconhecida pelo OLE. Se não for possível analisar a cadeia de caracteres, DBSTATUS_E_CANTCONVERTVALUE será definido. Se qualquer valor de componente estiver fora do intervalo, DBSTATUS_E_DATAOVERFLOW será definido.|  
|13|A cadeia de caracteres é analisada como um literal ISO e convertida para o tipo de destino. Se houver falha, a cadeia de caracteres será analisada como um literal de data OLE (que também tem componentes de hora) e convertida de uma data OLE (DBTYPE_DATE) para o tipo de destino. A cadeia de caracteres deve se conformar com a sintaxe de literais datetime, a menos que o destino seja DBTYPE_DATE ou DBTYPE_DBTIMESTAMP. Se for o caso, um literal datetime ou time será permitido para que a análise de formato ISO tenha êxito. Para que a análise de OLE tenha êxito, a cadeia de caracteres deve se conformar com a sintaxe reconhecida pelo OLE. Se não for possível analisar a cadeia de caracteres, DBSTATUS_E_CANTCONVERTVALUE será definido. Se qualquer valor de componente estiver fora do intervalo, DBSTATUS_E_DATAOVERFLOW será definido.|  
  
## <a name="see-also"></a>Consulte também  
 [Associações e conversões &#40;OLE DB&#41;](../../oledb/ole-db-date-time/conversions-ole-db.md)  
  
  
