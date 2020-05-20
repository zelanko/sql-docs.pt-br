---
title: 'Etapa 3: o servidor Obtém um conjunto de registros (tutorial RDS) | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], server obtains Recordset
ms.assetid: 9c6779c9-1208-4696-ac51-c39f3a6d9240
author: rothja
ms.author: jroth
ms.openlocfilehash: 1bd510ae09bf4c4d3cdc684925823381e40235c4
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764667"
---
# <a name="step-3-server-obtains-a-recordset-rds-tutorial"></a>Etapa 3: O servidor obtém um conjunto de registros (Tutorial RDS)
O programa do servidor usa a cadeia de conexão e o texto do comando para consultar a fonte de dados para as linhas desejadas. Normalmente, o ADO é usado para recuperar esse **conjunto de registros**, embora outras interfaces de acesso a dados da Microsoft, como OLE DB, possam ser usadas.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Um programa de servidor personalizado pode ter a seguinte aparência:  
  
```vb
Public Function ServerProgram(cn as String, qry as String) as Object  
Dim rs as New ADODB.Recordset  
   rs.CursorLocation = adUseClient  
   rs.Open qry, cn   
   rs.ActiveConnection = Nothing  
   Set ServerProgram = rs  
End Function  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Etapa 4: o servidor retorna o conjunto de registros (tutorial RDS)](../../../ado/guide/remote-data-service/step-4-server-returns-the-recordset-rds-tutorial.md)   
 [Tutorial RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
