---
title: "Método CreateRecordset (RDS) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- DataControl::CreateRecordset
- RDS.DataControl::CreateRecordset
- CreateRecordset
- RDSServer.DataFactory::CreateRecordset
- DataFactory::CreateRecordset
helpviewer_keywords:
- CreateRecordset method [RDS]
ms.assetid: 6840b1e5-c04d-4d3e-9dcc-42128c83492f
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2f5a273957b03cfb26e0f6d3f1b4aa563f9079e2
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="createrecordset-method-rds"></a>Método CreateRecordset (RDS)
Cria um vazio, desconectado [registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.CreateRecordset(ColumnInfos)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Objeto*  
 Uma variável de objeto que representa um [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) ou [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto.  
  
 *ColumnsInfos*  
 Um **Variant** matriz de atributos que definem cada coluna a **registros** criado. Cada definição de coluna contém uma matriz de quatro atributos necessários e um atributo opcional.  
  
|Atributo|Description|  
|---------------|-----------------|  
|Nome|Nome do cabeçalho da coluna.|  
|Tipo|Inteiro do tipo de dados.|  
|Tamanho|Inteiro da largura em caracteres, independentemente do tipo de dados.|  
|Nulidade|Valor booliano.|  
|Escala (opcional)|Este atributo opcional define a escala para campos numéricos. Se esse valor não for especificado, serão truncados em uma escala de três valores numéricos. Precisão não é afetada, mas o número de dígitos após o ponto decimal será truncado para três.|  
  
 O conjunto de matrizes de coluna, em seguida, é agrupado em uma matriz, que define o **registros**.  
  
## <a name="remarks"></a>Comentários  
 O objeto comercial do lado do servidor pode preencher resultante **registros** com dados de um provedor de dados não - OLE DB, como um sistema operacional do arquivo contendo cotações de ações.  
  
 A seguinte tabela lista o [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) valores com suporte a **CreateRecordset** método. O número listado é o número de referência usada para definir campos.  
  
 Cada um dos tipos de dados é de comprimento fixo ou comprimento variável. Tipos de comprimento fixo devem ser definidos com um tamanho de -1, porque o tamanho é predeterminado e uma definição de tamanho ainda é necessária. Tipos de dados de comprimento variável permitem um tamanho de 1 a 32767.  
  
 Para alguns dos tipos de dados da variável, o tipo pode ser forçado para o tipo indicado na coluna de substituição. Você não verá as substituições até após o **registros** é criada e preenchida. Em seguida, você pode verificar o tipo de dados reais, se necessário.  
  
|Comprimento|Constante|Número|Substituição|  
|------------|--------------|------------|------------------|  
|Fixo|**adTinyInt**|16||  
|Fixo|**adSmallInt**|2||  
|Fixo|**adInteger**|3||  
|Fixo|**adBigInt**|20||  
|Fixo|**adUnsignedTinyInt**|17||  
|Fixo|**adUnsignedSmallInt**|18||  
|Fixo|**adUnsignedInt**|19||  
|Fixo|**adUnsignedBigInt**|21||  
|Fixo|**adSingle**|4||  
|Fixo|**adDouble**|5||  
|Fixo|**adCurrency**|6||  
|Fixo|**adDecimal**|14||  
|Fixo|**adNumeric**|131||  
|Fixo|**adBoolean**|11||  
|Fixo|**adError**|10||  
|Fixo|**adGuid**|72||  
|Fixo|**adDate**|7||  
|Fixo|**adDBDate**|133||  
|Fixo|**adDBTime**|134||  
|Fixo|**adDBTimestamp**|135|7|  
|Variável|**adBSTR**|8|130|  
|Variável|**adChar**|129|200|  
|Variável|**adVarChar**|200||  
|Variável|**adLongVarChar**|201|200|  
|Variável|**adWChar**|130||  
|Variável|**adVarWChar**|202|130|  
|Variável|**adLongVarWChar**|203|130|  
|Variável|**adBinary**|128||  
|Variável|**adVarBinary**|204||  
|Variável|**adLongVarBinary**|205|204|  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)|[Objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo do método CreateRecordset (VB)](../../../ado/reference/ado-api/createrecordset-method-example-vb.md)   
 [Exemplo do método CreateRecordset (VBScript)](../../../ado/reference/rds-api/createrecordset-method-example-vbscript.md)   
 [Método CreateObject (RDS)](../../../ado/reference/rds-api/createobject-method-rds.md)




