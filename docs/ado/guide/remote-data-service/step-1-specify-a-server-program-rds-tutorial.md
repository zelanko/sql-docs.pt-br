---
description: 'Etapa 1: Especificar um programa de servidor (Tutorial RDS)'
title: 'Etapa 1: especificar um programa de servidor (tutorial RDS) | Microsoft Docs'
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 32e01e2dd12dcfb098222ffb7c8da0d9a4527d5d
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88759156"
---
# <a name="step-1-specify-a-server-program-rds-tutorial"></a>Etapa 1: Especificar um programa de servidor (Tutorial RDS)
No caso mais geral, use o [RDS. ](../../reference/rds-api/dataspace-object-rds.md) Método [CreateObject](../../reference/rds-api/createobject-method-rds.md) do objeto DataSpace para especificar o programa de servidor padrão, [RDSServer. datafactory](../../reference/rds-api/datafactory-object-rdsserver.md)ou seu próprio programa de servidor personalizado (objeto Business). Um programa de servidor é instanciado no servidor e uma referência ao programa do servidor, ou *proxy*, é retornada.  
  
 Este tutorial usa o programa de servidor padrão:  
  
```vb
Sub RDSTutorial1()  
   Dim DS as New RDS.DataSpace  
   Dim DF as Object  
   Set DF = DS.("RDSServer.DataFactory", "https://yourServer")  
...  
```  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Consulte Também  
 [Etapa 2: invocar o programa de servidor (tutorial RDS)](./step-2-invoke-the-server-program-rds-tutorial.md)   
 [Tutorial RDS (VBScript)](./rds-tutorial-vbscript.md)