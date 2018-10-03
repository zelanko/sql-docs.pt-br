---
title: Conjunto de registros, propriedades SourceRecordset (RDS) | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Recordset property [ADO]
ms.assetid: a29e3fb9-306d-497a-9a59-1856a914e5e9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bc0b548015cc63117cff566a2c4507b266d5ab7b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47657504"
---
# <a name="recordset-sourcerecordset-properties-rds"></a>Conjunto de registros, propriedades SourceRecordset (RDS)
Indica o **Recordset** objeto retornado de um objeto comercial personalizado.  
  
 **Aplica-se a:** [objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DataControl.SourceRecordset = Recordset  
Recordset = DataControl.Recordset   
```  
  
#### <a name="parameters"></a>Parâmetros  
 *DataControl*  
 Uma variável de objeto que representa um [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto.  
  
 *Recordset*  
 Uma variável de objeto que representa um **Recordset** objeto.  
  
## <a name="remarks"></a>Comentários  
 Você pode definir as **SourceRecordset** propriedade para um [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) retornado de um objeto comercial personalizado.  
  
 Essas propriedades permitem que um aplicativo para controlar o processo de associação por meio de um processo personalizado. Eles recebem um conjunto de linhas encapsulado em um **conjunto de registros** para que você pode interagir diretamente com o **conjunto de registros**, executar ações como propriedades de configuração ou iterar por meio o **conjunto de registros** .  
  
 Você pode definir as **SourceRecordset** propriedade ou leitura a **Recordset** propriedade em tempo de execução no código de script.  
  
 **SourceRecordset** é uma propriedade somente gravação, em contraste com o **Recordset** propriedade, que é uma propriedade somente leitura.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte também  
 [Conjunto de registros e exemplo de propriedades SourceRecordset (VBScript)](../../../ado/reference/rds-api/recordset-and-sourcerecordset-properties-example-vbscript.md)   
 [Método CreateRecordset (RDS)](../../../ado/reference/rds-api/createrecordset-method-rds.md)   
 [Método Query (RDS)](../../../ado/reference/rds-api/query-method-rds.md)


