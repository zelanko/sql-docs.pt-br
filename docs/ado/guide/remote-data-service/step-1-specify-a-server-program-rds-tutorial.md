---
title: 'Etapa 1: Especificar um programa de servidor (Tutorial de RDS) | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], specifying server program
ms.assetid: d8bb35b1-c02a-4231-8d55-016e56e53b95
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dca4476288c3fb6a65f245f6fcd3380aec47666f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="step-1-specify-a-server-program-rds-tutorial"></a>Etapa 1: Especificar um programa de servidor (Tutorial de RDS)
No caso mais geral, use o [RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) objeto [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) método para especificar o programa de servidor padrão, [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md), ou seu próprio programa de servidor personalizado (objeto comercial). Um programa de servidor é instanciado no servidor e uma referência para o programa do servidor, ou *proxy*, será retornado.  
  
 Este tutorial usa o programa de servidor padrão:  
  
```  
Sub RDSTutorial1()  
   Dim DS as New RDS.DataSpace  
   Dim DF as Object  
   Set DF = DS.("RDSServer.DataFactory", "http://yourServer")  
...  
```  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Consulte também  
 [Etapa 2: Chamar o programa de servidor (Tutorial de RDS)](../../../ado/guide/remote-data-service/step-2-invoke-the-server-program-rds-tutorial.md)   
 [Tutorial RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
