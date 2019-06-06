---
title: 'Etapa 1: Especifique um programa de servidor (Tutorial RDS) | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], specifying server program
ms.assetid: d8bb35b1-c02a-4231-8d55-016e56e53b95
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 03d60a00a116f771e3854a4fe1b6b5ec512c0708
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704173"
---
# <a name="step-1-specify-a-server-program-rds-tutorial"></a>Etapa 1: Especificar um programa de servidor (Tutorial RDS)
No caso mais geral, use o [RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) objeto [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) método para especificar o programa de servidor padrão, [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md), ou seu próprio programa de servidor personalizado (objeto de negócios). Um programa de servidor é instanciado no servidor e uma referência para o programa de servidor, ou *proxy*, será retornado.  
  
 Este tutorial usa o programa de servidor padrão:  
  
```vb
Sub RDSTutorial1()  
   Dim DS as New RDS.DataSpace  
   Dim DF as Object  
   Set DF = DS.("RDSServer.DataFactory", "https://yourServer")  
...  
```  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Consulte também  
 [Etapa 2: Invocar o programa de servidor (Tutorial RDS)](../../../ado/guide/remote-data-service/step-2-invoke-the-server-program-rds-tutorial.md)   
 [Tutorial RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
