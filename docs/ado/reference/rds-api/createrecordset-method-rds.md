---
description: Método CreateRecordset (RDS)
title: Método createrecordset (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: ad1c9b0f36922f29ce015fd459a1be3e788e07f5
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91721197"
---
# <a name="createrecordset-method-rds"></a>Método CreateRecordset (RDS)
Cria um [conjunto de registros](../ado-api/recordset-object-ado.md)vazio e desconectado.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](/dotnet/framework/wcf/).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.CreateRecordset(ColumnInfos)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Objeto*  
 Uma variável de objeto que representa um [RDSServer. datafactory](./datafactory-object-rdsserver.md) ou [RDS. Objeto DataControl](./datacontrol-object-rds.md) .  
  
 *ColumnsInfos*  
 Uma matriz **variante** de atributos que define cada coluna no **conjunto de registros** criado. Cada definição de coluna contém uma matriz de quatro atributos necessários e um atributo opcional.  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|Nome|Nome do cabeçalho da coluna.|  
|Tipo|Inteiro do tipo de dados.|  
|Tamanho|O número inteiro da largura em caracteres, independentemente do tipo de dados.|  
|Nulidade|$True.|  
|Escala (opcional)|Esse atributo opcional define a escala para campos numéricos. Se esse valor não for especificado, os valores numéricos serão truncados para uma escala de três. A precisão não é afetada, mas o número de dígitos após o ponto decimal será truncado para três.|  
  
 O conjunto de matrizes de coluna é então agrupado em uma matriz, que define o **conjunto de registros**.  
  
## <a name="remarks"></a>Comentários  
 O objeto comercial do lado do servidor pode preencher o **conjunto de registros** resultante com dados de um provedor de dados não OLE DB, como um arquivo do sistema operacional que contém Cotações de ações.  
  
 A tabela a seguir lista os valores de [DataTypeEnum](../ado-api/datatypeenum.md) com suporte pelo método **createrecordset** . O número listado é o número de referência usado para definir campos.  
  
 Cada um dos tipos de dados é de comprimento fixo ou variável. Os tipos de comprimento fixo devem ser definidos com um tamanho de-1, porque o tamanho é predeterminado e uma definição de tamanho ainda é necessária. Os tipos de dados de comprimento variável permitem um tamanho de 1 a 32767.  
  
 Para alguns dos tipos de dados variáveis, o tipo pode ser forçado para o tipo indicado na coluna de substituição. Você não verá as substituições até que o **conjunto de registros** seja criado e preenchido. Em seguida, você pode verificar o tipo de dados real, se necessário.  
  
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
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Objeto DataControl (RDS)](./datacontrol-object-rds.md)  
    :::column-end:::
    :::column:::
        [Objeto DataFactory (RDSServer)](./datafactory-object-rdsserver.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte Também  
 [Exemplo do método createrecordset (VB)](../ado-api/createrecordset-method-example-vb.md)   
 [Exemplo do método createrecordset (VBScript)](./createrecordset-method-example-vbscript.md)   
 [Método CreateObject (RDS)](./createobject-method-rds.md)