---
title: Modelo de programação do RDS com objetos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS programming model [ADO]
- RDS objects [ADO]
ms.assetid: 07ce0ef0-72f1-48f4-823d-1b65d28c0926
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b60f402cdc7ba861a0d0550a92d16fa7dd1f59b7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62931411"
---
# <a name="rds-programming-model-with-objects"></a>Modelo de programação do RDS com objetos
O objetivo do RDS é acessar e atualizar fontes de dados por meio de um intermediário, como o IIS. O modelo de programação Especifica a sequência de atividades necessárias para atingir essa meta. O modelo de objeto Especifica os objetos cujos métodos e propriedades afetam o modelo de programação.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 O RDS fornece os meios para executar a seguinte sequência de ações:  
  
-   Especifique o programa a ser invocado no servidor e obter uma maneira (proxy) para se referir a ele do cliente ([RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)).  
  
-   Invocar o programa do servidor. Passar parâmetros para o programa de servidor que identifica a fonte de dados e emitir o comando (proxy ou [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)).  
  
-   O programa de servidor obtém um [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto da fonte de dados, normalmente usando o ADO. Opcionalmente, o **conjunto de registros** objeto é processado no servidor ([RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)).  
  
-   O programa de servidor retorna o último **Recordset** objeto para o aplicativo cliente (proxy).  
  
-   No cliente, o **conjunto de registros** objeto deve ser colocado em um formulário que pode ser facilmente usado por controles visuais (controle visual e **RDS. DataControl**).  
  
-   Altera para o **conjunto de registros** objeto são enviadas de volta para o servidor e usado para atualizar a fonte de dados (**RDS. DataControl** ou **RDSServer.DataFactory**).  
  
## <a name="see-also"></a>Consulte também  
 [Resumo do modelo de objeto RDS](../../../ado/guide/remote-data-service/rds-object-model-summary.md)   
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [Objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)   
 [Objeto DataSpace (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)   
 [Cenário RDS](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [Tutorial RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Segurança e uso RDS](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


