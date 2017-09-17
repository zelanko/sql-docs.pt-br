---
title: "Modelo de programação de RDS com objetos | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- RDS programming model [ADO]
- RDS objects [ADO]
ms.assetid: 07ce0ef0-72f1-48f4-823d-1b65d28c0926
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2f89c867cb836ec69fd5fe59adf16d93f4708d0f
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="rds-programming-model-with-objects"></a>Modelo de programação de RDS com objetos
O objetivo do RDS é acessar e atualizar fontes de dados por meio de um intermediário, como o IIS. O modelo de programação Especifica a sequência de atividades necessárias para atingir essa meta. O modelo de objeto Especifica os objetos cujos métodos e propriedades afetam o modelo de programação.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 RDS fornece os meios para executar a seguinte sequência de ações:  
  
-   Especifique o programa a ser invocado no servidor e obter uma forma (proxy) para se referir a ele do cliente ([RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)).  
  
-   Invoque o programa do servidor. Passar parâmetros para o programa do servidor que identifica a fonte de dados e emitir o comando (proxy ou [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)).  
  
-   O programa de servidor obtém um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto da fonte de dados, normalmente usando o ADO. Opcionalmente, o **registros** objeto for processado no servidor ([RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)).  
  
-   O programa do servidor retorna o último **registros** objeto para o aplicativo cliente (proxy).  
  
-   No cliente, o **registros** objeto é colocado em um formulário que pode ser usado facilmente por controles visuais (controle visual e **RDS. DataControl**).  
  
-   Altera para o **registros** objeto são enviadas de volta para o servidor e usado para atualizar a fonte de dados (**RDS. DataControl** ou **RDSServer.DataFactory**).  
  
## <a name="see-also"></a>Consulte também  
 [Resumo do modelo de objeto de RDS](../../../ado/guide/remote-data-service/rds-object-model-summary.md)   
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [Objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)   
 [Objeto de espaço de dados (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)   
 [Cenário RDS](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [Tutorial RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Segurança e uso RDS](../../../ado/guide/remote-data-service/rds-usage-and-security.md)



