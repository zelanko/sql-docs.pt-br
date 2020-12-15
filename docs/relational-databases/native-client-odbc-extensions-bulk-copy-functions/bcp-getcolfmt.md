---
description: bcp_getcolfmt
title: bcp_getcolfmt | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_getcolfmt
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_getcolfmt function
ms.assetid: f8bdada5-7b2d-4475-8c98-f93e9d77b130
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d22956e5331d8ab718d354b981d59d7cfef4eaeb
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97473777"
---
# <a name="bcp_getcolfmt"></a>bcp_getcolfmt
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Usado para localizar o valor da propriedade de formato da coluna.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RETCODE bcp_getcolfmt (  
        HDBC hdbc,  
        INT field,  
        INT property,  
        void* pValue,  
        INT cbvalue,  
        INT* pcbLen);  
```  
  
## <a name="arguments"></a>Argumentos  
 *hdbc*  
 É o identificador de conexão ODBC habilitado para cópia em massa.  
  
 *campo*  
 É o número de coluna para o qual a propriedade é recuperada.  
  
 *property*  
 É um das constantes de propriedade.  
  
 *Valores*  
 É o ponteiro para o buffer do qual recuperar o valor dado propriedade.  
  
 *cbValue*  
 É o comprimento do buffer da propriedade em bytes.  
  
 *pcbLen*  
 Ponteiro para o comprimento dos dados que estão sendo retornados no buffer de propriedade.  
  
## <a name="returns"></a>Retornos  
 SUCCEED ou FAIL.  
  
## <a name="remarks"></a>Comentários  
 Valores da propriedade de formato da coluna são listados no tópico [bcp_setcolfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setcolfmt.md) . Os valores de propriedade da coluna são definidos chamando a função **bcp_setcolfmt** e a função **bcp_getcolfmt** é usada para localizar o valor da propriedade de formato da coluna.  
  
 Podem ser observadas alterações de comportamento ao conectar a um computador de servidor [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (ou posterior), na comparação com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, veja [Descoberta de metadados](../../relational-databases/native-client/features/metadata-discovery.md).  
  
## <a name="bcp_getcolfmt-support-for-enhanced-date-and-time-features"></a>Suporte de bcp_getcolfmt a recursos aprimorados de data e hora  
 Os tipos usados com a propriedade **BCP_FMT_TYPE** para tipos de data/hora são conforme especificado em [alterações de cópia em massa para tipos de data e hora aprimorados &#40;OLE DB e&#41;ODBC](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).  
  
 Para obter mais informações, consulte [melhorias de data e hora &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Bulk Copy Functions](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
