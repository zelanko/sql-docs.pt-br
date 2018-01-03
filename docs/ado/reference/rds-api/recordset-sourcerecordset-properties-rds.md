---
title: Conjunto de registros, propriedades SourceRecordset (RDS) | Microsoft Docs
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.component: reference
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords: Recordset property [ADO]
ms.assetid: a29e3fb9-306d-497a-9a59-1856a914e5e9
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dbe0667cd71609f092e3008bf65d7a5cca2faf37
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2017
---
# <a name="recordset-sourcerecordset-properties-rds"></a>Conjunto de registros, propriedades SourceRecordset (RDS)
Indica o **registros** objeto retornado de um objeto de negócios personalizada.  
  
 **Aplica-se a:** [DataControl objeto (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DataControl.SourceRecordset = Recordset  
Recordset = DataControl.Recordset   
```  
  
#### <a name="parameters"></a>Parâmetros  
 *DataControl*  
 Uma variável de objeto que representa um [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto.  
  
 *Conjunto de registros*  
 Uma variável de objeto que representa um **registros** objeto.  
  
## <a name="remarks"></a>Remarks  
 Você pode definir o **SourceRecordset** propriedade para um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) retornado de um objeto comercial personalizado.  
  
 Essas propriedades permitem que um aplicativo para controlar o processo de ligação por meio de um processo personalizado. Recebem um conjunto de linhas encapsulado em um **Recordset** para que você pode interagir diretamente com o **Recordset**, executar ações como propriedades de configuração ou iteração a **conjunto de registros** .  
  
 Você pode definir o **SourceRecordset** propriedade ou ler o **registros** propriedade em tempo de execução no código de script.  
  
 **SourceRecordset** é uma propriedade somente gravação, em comparação com o **registros** propriedade, que é uma propriedade somente leitura.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de propriedades de SourceRecordset (VBScript) e o conjunto de registros](../../../ado/reference/rds-api/recordset-and-sourcerecordset-properties-example-vbscript.md)   
 [Método CreateRecordset (RDS)](../../../ado/reference/rds-api/createrecordset-method-rds.md)   
 [Método Query (RDS)](../../../ado/reference/rds-api/query-method-rds.md)


