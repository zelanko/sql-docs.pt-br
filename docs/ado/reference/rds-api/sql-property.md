---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d4d665e2b2f9ac4d61951da3cccbd16db76127a5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47727014"
---
# <a name="sql-property"></a>Propriedade SQL
Indica a cadeia de caracteres de consulta usada para recuperar o [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
 Você pode definir as **SQL** propriedade em tempo de design no [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) marcas de objeto do objeto, ou em tempo de execução no código de script.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Design time: <PARAM NAME="SQL" VALUE="QueryString">  
Run time: DataControl.SQL = "QueryString"  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *QueryString*  
 Um **cadeia de caracteres** valor que contém uma solicitação de dados SQL válida.  
  
 *DataControl*  
 Uma variável de objeto que representa um **RDS. DataControl** objeto.  
  
## <a name="remarks"></a>Comentários  
 Em geral, isso é uma instrução SQL (usando o dialeto do servidor de banco de dados), como `"Select * from NewTitles"`. Para garantir que os registros são correspondidos e atualizados com precisão, uma consulta atualizável deve conter um campo que não seja um campo binário longo ou um campo computado.  
  
 O **SQL** propriedade é opcional se um objeto de negócios personalizada do lado do servidor recupera os dados para o cliente.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo da propriedade SQL (VBScript)](../../../ado/reference/rds-api/sql-property-example-vbscript.md)   
 [Propriedade Connect (RDS)](../../../ado/reference/rds-api/connect-property-rds.md)   
 [Método Query (RDS)](../../../ado/reference/rds-api/query-method-rds.md)   
 [Método Refresh (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)   
 [Método SubmitChanges (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


