---
title: bcp_getcolfmt | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- bcp_getcolfmt
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_getcolfmt function
ms.assetid: f8bdada5-7b2d-4475-8c98-f93e9d77b130
caps.latest.revision: 36
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b31203c3f8627102ec3320f2c038afe2886eeeec
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37420875"
---
# <a name="bcpgetcolfmt"></a>bcp_getcolfmt
  Usado para localizar o valor da propriedade de formato da coluna.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RETCODE bcp_getcolfmt (  
HDBC   
hdbc  
,  
INT   
field  
,  
INT   
property  
,  
void*   
pValue  
,  
INT   
cbvalue,  
INT*   
pcbLen  
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *HDBC*  
 É o identificador de conexão ODBC habilitado para cópia em massa.  
  
 *field*  
 É o número de coluna para o qual a propriedade é recuperada.  
  
 *property*  
 É um das constantes de propriedade.  
  
 *pValue*  
 É o ponteiro para o buffer do qual recuperar o valor dado propriedade.  
  
 *cbValue*  
 É o comprimento do buffer da propriedade em bytes.  
  
 *pcbLen*  
 Ponteiro para o comprimento dos dados que estão sendo retornados no buffer de propriedade.  
  
## <a name="returns"></a>Retorna  
 SUCCEED ou FAIL.  
  
## <a name="remarks"></a>Remarks  
 Valores de propriedade de formato de coluna são listados na [bcp_setcolfmt](bcp-setcolfmt.md) tópico. Os valores de propriedade da coluna são definidos chamando a função **bcp_setcolfmt** e a função **bcp_getcolfmt** é usada para localizar o valor da propriedade de formato da coluna.  
  
 Podem ser observadas alterações de comportamento, ao se conectar a um [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (ou posterior) computador do servidor, em comparação comparada anteriormente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versões. Para obter mais informações, consulte [descoberta de metadados](../native-client/features/metadata-discovery.md).  
  
## <a name="bcpgetcolfmt-support-for-enhanced-date-and-time-features"></a>Suporte de bcp_getcolfmt a recursos aprimorados de data e hora  
 Os tipos usados com o `BCP_FMT_TYPE` são de propriedade para tipos de data/hora conforme especificado no [alterações de cópia em massa para tipos de tempo e aprimorados de data &#40;OLE DB e ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).  
  
 Para obter mais informações, consulte [aprimoramentos de data e hora &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="see-also"></a>Consulte também  
 [Funções de cópia em massa](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
