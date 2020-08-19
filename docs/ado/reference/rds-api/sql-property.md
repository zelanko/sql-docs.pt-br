---
description: Propriedade SQL
title: Propriedade SQL | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- SQL property [RDS]
ms.assetid: e0dabf23-a159-4fe5-a962-3df544a21f5c
author: rothja
ms.author: jroth
ms.openlocfilehash: c21e12d3601f40b1749067f04ce3d655ea0c1109
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438598"
---
# <a name="sql-property"></a>Propriedade SQL
Indica a cadeia de caracteres de consulta usada para recuperar o [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
 Você pode definir a propriedade **SQL** em tempo de design no [RDS. ](../../../ado/reference/rds-api/datacontrol-object-rds.md) Marcas de objeto do objeto DataControl ou em tempo de execução no código de script.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Design time: <PARAM NAME="SQL" VALUE="QueryString">  
Run time: DataControl.SQL = "QueryString"  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *QueryString*  
 Um valor de **cadeia de caracteres** que contém uma solicitação de dados SQL válida.  
  
 *DataControl*  
 Uma variável de objeto que representa um **RDS. Objeto DataControl** .  
  
## <a name="remarks"></a>Comentários  
 Em geral, essa é uma instrução SQL (usando o dialeto do servidor de banco de dados), como `"Select * from NewTitles"` . Para garantir que os registros sejam correspondidos e atualizados com precisão, uma consulta atualizável deve conter um campo diferente de um campo binário longo ou um campo computado.  
  
 A propriedade **SQL** será opcional se um objeto comercial personalizado do lado do servidor recuperar os dados para o cliente.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade SQL (VBScript)](../../../ado/reference/rds-api/sql-property-example-vbscript.md)   
 [Propriedade Connect (RDS)](../../../ado/reference/rds-api/connect-property-rds.md)   
 [Método de consulta (RDS)](../../../ado/reference/rds-api/query-method-rds.md)   
 [Método de atualização (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)   
 [Método SubmitChanges (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


