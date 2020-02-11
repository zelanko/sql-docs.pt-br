---
title: DataTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- DataTypeEnum
helpviewer_keywords:
- DataTypeEnum enumeration [ADO]
ms.assetid: 2c57eca6-9336-4b06-ba10-9fef5926b1d0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 27386894ce6d1d393505d49b4863a0ba9bf3320b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67933220"
---
# <a name="datatypeenum"></a>DataTypeEnum
Especifica o tipo de dados de um [campo](../../../ado/reference/ado-api/field-object.md), [parâmetro](../../../ado/reference/ado-api/parameter-object.md)ou [Propriedade](../../../ado/reference/ado-api/property-object-ado.md). O indicador de tipo de OLE DB correspondente é mostrado entre parênteses na coluna Descrição da tabela a seguir.  
  
|Constante|Valor|DESCRIÇÃO|  
|--------------|-----------|-----------------|  
|**AdArray**|0x2000|Um valor de sinalizador, sempre combinado com outra constante de tipo de dados, que indica uma matriz de outro tipo de dados. Não se aplica a ADOX.|  
|**adBigInt**|20|Indica um inteiro com sinal de oito bytes (DBTYPE_I8).|  
|**adBinary**|128|Indica um valor binário (DBTYPE_BYTES).|  
|**adBoolean**|11|Indica um valor **booliano** (DBTYPE_BOOL).|  
|**adBSTR**|8|Indica uma cadeia de caracteres (Unicode) terminada em nulo (DBTYPE_BSTR).|  
|**adChapter**|136|Indica um valor de capítulo de quatro bytes que identifica linhas em um conjunto de linhas filho (DBTYPE_HCHAPTER).|  
|**adChar**|129|Indica um valor de cadeia de caracteres (DBTYPE_STR).|  
|**adCurrency**|6|Indica um valor de moeda (DBTYPE_CY). Currency é um número de ponto fixo com quatro dígitos à direita do ponto decimal. Ele é armazenado em um inteiro com sinal de oito bytes dimensionado por 10.000.|  
|**adDate**|7|Indica um valor de data (DBTYPE_DATE). Uma data é armazenada como Double, a parte inteira da qual é o número de dias desde 30 de dezembro de 1899 e a parte fracionária do que é a fração de um dia.|  
|**adDBDate**|133|Indica um valor de data (AAAAMMDD) (DBTYPE_DBDATE).|  
|**adDBTime**|134|Indica um valor de tempo (HHMMSS) (DBTYPE_DBTIME).|  
|**adDBTimeStamp**|135|Indica um carimbo de data/hora (AAAAMMDDHHMMSS mais uma fração em billionths) (DBTYPE_DBTIMESTAMP).|  
|**adDecimal**|14|Indica um valor numérico exato com precisão e escala fixas (DBTYPE_DECIMAL).|  
|**adDouble**|5|Indica um valor de ponto flutuante de precisão dupla (DBTYPE_R8).|  
|**adEmpty**|0|Não especifica nenhum valor (DBTYPE_EMPTY).|  
|**adError**|10|Indica um código de erro de 32 bits (DBTYPE_ERROR).|  
|**adFileTime**|64|Indica um valor de 64 bits que representa o número de intervalos de 100 nanossegundos desde 1º de janeiro de 1601 (DBTYPE_FILETIME).|  
|**adGUID**|72|Indica um GUID (identificador global exclusivo) (DBTYPE_GUID).|  
|**adIDispatch**|9|Indica um ponteiro para uma interface **IDispatch** em um objeto COM (DBTYPE_IDISPATCH).<br /><br /> **Observação** Atualmente, não há suporte para esse tipo de dados no ADO. O uso pode causar resultados imprevisíveis.|  
|**adInteger**|3|Indica um inteiro com sinal de quatro bytes (DBTYPE_I4).|  
|**adIUnknown**|13|Indica um ponteiro para uma interface **IUnknown** em um objeto COM (DBTYPE_IUNKNOWN).<br /><br /> **Observação** Atualmente, não há suporte para esse tipo de dados no ADO. O uso pode causar resultados imprevisíveis.|  
|**adLongVarBinary**|205|Indica um valor binário longo.|  
|**adLongVarChar**|201|Indica um valor de cadeia de caracteres longa.|  
|**adLongVarWChar**|203|Indica um longo valor de cadeia de caracteres Unicode terminada em nulo.|  
|**adNumeric**|131|Indica um valor numérico exato com precisão e escala fixas (DBTYPE_NUMERIC).|  
|**adPropVariant**|138|Indica um PROPVARIANT de automação (DBTYPE_PROP_VARIANT).|  
|**adSingle**|4|Indica um valor de ponto flutuante de precisão simples (DBTYPE_R4).|  
|**adSmallInt**|2|Indica um inteiro com sinal de dois bytes (DBTYPE_I2).|  
|**adTinyInt**|16|Indica um inteiro com sinal de um byte (DBTYPE_I1).|  
|**adUnsignedBigInt**|21|Indica um inteiro não assinado de oito bytes (DBTYPE_UI8).|  
|**adUnsignedInt**|19|Indica um inteiro não assinado de quatro bytes (DBTYPE_UI4).|  
|**adUnsignedSmallInt**|18|Indica um inteiro não assinado de dois bytes (DBTYPE_UI2).|  
|**adUnsignedTinyInt**|17|Indica um inteiro não assinado de um byte (DBTYPE_UI1).|  
|**adUserDefined**|132|Indica uma variável definida pelo usuário (DBTYPE_UDT).|  
|**adVarBinary**|204|Indica um valor binário.|  
|**adVarChar**|200|Indica um valor de cadeia de caracteres.|  
|**adVariant**|12|Indica uma **variante** de automação (DBTYPE_VARIANT).<br /><br /> **Observação** Atualmente, não há suporte para esse tipo de dados no ADO. O uso pode causar resultados imprevisíveis.|  
|**adVarNumeric**|139|Indica um valor numérico.|  
|**adVarWChar**|202|Indica uma cadeia de caracteres Unicode terminada em nulo.|  
|**adWChar**|130|Indica uma cadeia de caracteres Unicode terminada em nulo (DBTYPE_WSTR).|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. DataType. ARRAY|  
|AdoEnums. DataType. BIGINT|  
|AdoEnums. DataType. BINARY|  
|AdoEnums. DataType. BOOLIANo|  
|AdoEnums. DataType. BSTR|  
|AdoEnums. DataType. CHAPTER|  
|AdoEnums. DataType. CHAR|  
|AdoEnums. DataType. CURRENCY|  
|AdoEnums. DataType. DATE|  
|AdoEnums. DataType. DBDATE|  
|AdoEnums. DataType. DBTIME|  
|AdoEnums. DataType. DBTIMESTAMP|  
|AdoEnums. DataType. DECIMAL|  
|AdoEnums. DataType. DOUBLE|  
|AdoEnums. DataType. EMPTY|  
|AdoEnums. DataType. ERROR|  
|AdoEnums. DataType. FILETIME|  
|AdoEnums. DataType. GUID|  
|AdoEnums. DataType. IDISPATCH|  
|AdoEnums. DataType. INTEGER|  
|AdoEnums. DataType. IUNKNOWN|  
|AdoEnums. DataType. LONGVARBINARY|  
|AdoEnums. DataType. LONGVARCHAR|  
|AdoEnums. DataType. LONGVARWCHAR|  
|AdoEnums. DataType. NUMERIC|  
|AdoEnums. DataType. PROPVARIANT|  
|AdoEnums. DataType. SINGLE|  
|AdoEnums. DataType. SMALLINT|  
|AdoEnums. DataType. TINYINT|  
|AdoEnums. DataType. UNSIGNEDBIGINT|  
|AdoEnums. DataType. UNSIGNEDINT|  
|AdoEnums. DataType. UNSIGNEDSMALLINT|  
|AdoEnums. DataType. UNSIGNEDTINYINT|  
|AdoEnums. DataType. UserDefined|  
|AdoEnums. DataType. VARBINARY|  
|AdoEnums. DataType. VARCHAR|  
|AdoEnums. DataType. VARIANT|  
|AdoEnums. DataType. VARNUMERIC|  
|AdoEnums. DataType. VARWCHAR|  
|AdoEnums. DataType. WCHAR|  
  
## <a name="applies-to"></a>Aplica-se A  
  
|||  
|-|-|  
|[Método Append (ADO)](../../../ado/reference/ado-api/append-method-ado.md)|[Método CreateParameter (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)|  
|[Método CreateRecordset (RDS)](../../../ado/reference/rds-api/createrecordset-method-rds.md)|[Propriedade Type (ADO)](../../../ado/reference/ado-api/type-property-ado.md)|
