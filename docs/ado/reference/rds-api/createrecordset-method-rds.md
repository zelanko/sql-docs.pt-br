---
title: Método CreateRecordset (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4b376924dfb1833165a1f40ecfd1487c49eb2dcb
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51604616"
---
# <a name="createrecordset-method-rds"></a>Método CreateRecordset (RDS)
Cria um vazio, desconectado [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.CreateRecordset(ColumnInfos)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Objeto*  
 Uma variável de objeto que representa um [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) ou [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto.  
  
 *ColumnsInfos*  
 Um **Variant** matriz de atributos que definem cada coluna na **Recordset** criado. Cada definição de coluna contém uma matriz de quatro atributos necessários e um atributo opcional.  
  
|attribute|Description|  
|---------------|-----------------|  
|Nome|Nome do cabeçalho da coluna.|  
|Tipo|Inteiro do tipo de dados.|  
|Tamanho|Inteiro da largura em caracteres, independentemente do tipo de dados.|  
|Nulidade|Valor booliano.|  
|Escala (opcional)|Esse atributo opcional define a escala para campos numéricos. Se esse valor não for especificado, serão truncados para uma escala de três valores numéricos. Precisão não é afetada, mas o número de dígitos após o ponto decimal será truncado para três.|  
  
 O conjunto de matrizes de coluna, em seguida, é agrupado em uma matriz, que define o **conjunto de registros**.  
  
## <a name="remarks"></a>Comentários  
 O objeto de negócios do lado do servidor pode popular resultante **Recordset** com dados de um provedor de dados não - OLE DB, como um sistema operacional do arquivo contendo cotações de ações.  
  
 A seguinte tabela lista os [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) valores com suporte a **CreateRecordset** método. O número listado é o número de referência usado para definir os campos.  
  
 Cada um dos tipos de dados é de comprimento fixo ou comprimento variável. Tipos de comprimento fixo devem ser definidos com um tamanho de – 1, porque o tamanho é predeterminado e uma definição de tamanho ainda é necessária. Tipos de dados de comprimento variável que um tamanho de 1 a 32767.  
  
 Para alguns dos tipos de dados da variável, o tipo pode ser forçado para o tipo indicado na coluna de substituição. Você não verá as substituições até após o **Recordset** é criado e preenchido. Em seguida, você pode verificar o tipo de dados, se necessário.  
  
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



