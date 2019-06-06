---
title: 'Etapa 3: Servidor obtém um conjunto de registros (Tutorial RDS) | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: eb0afbbe470a1cc9cddbf9e9f2f892deb7ce0864
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704171"
---
# <a name="step-3-server-obtains-a-recordset-rds-tutorial"></a>Etapa 3: O servidor obtém um conjunto de registros (Tutorial RDS)
O programa de servidor usa o texto de cadeia de caracteres e o comando conectar para consultar a fonte de dados para as linhas desejadas. ADO normalmente é usado para recuperar esse **Recordset**, embora interfaces, de acesso a outros dados da Microsoft, como o OLE DB, poderia ser usado.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Um programa de servidor personalizado pode ter esta aparência:  
  
```vb
Public Function ServerProgram(cn as String, qry as String) as Object  
Dim rs as New ADODB.Recordset  
   rs.CursorLocation = adUseClient  
   rs.Open qry, cn   
   rs.ActiveConnection = Nothing  
   Set ServerProgram = rs  
End Function  
```  
  
## <a name="see-also"></a>Consulte também  
 [Etapa 4: Servidor retorna o conjunto de registros (Tutorial RDS)](../../../ado/guide/remote-data-service/step-4-server-returns-the-recordset-rds-tutorial.md)   
 [Tutorial RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
