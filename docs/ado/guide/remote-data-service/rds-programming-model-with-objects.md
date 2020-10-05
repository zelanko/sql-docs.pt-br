---
description: Modelo de programação do RDS com objetos
title: Modelo de programação de RDS com objetos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS programming model [ADO]
- RDS objects [ADO]
ms.assetid: 07ce0ef0-72f1-48f4-823d-1b65d28c0926
author: rothja
ms.author: jroth
ms.openlocfilehash: 6ee41cabf8175bc7f2a34c0381193e406d33f38f
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724907"
---
# <a name="rds-programming-model-with-objects"></a>Modelo de programação do RDS com objetos
O objetivo do RDS é obter acesso e atualizar fontes de dados por meio de um intermediário, como o IIS. O modelo de programação especifica a sequência de atividades necessárias para atingir essa meta. O modelo de objeto especifica os objetos cujos métodos e propriedades afetam o modelo de programação.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](/dotnet/framework/wcf/).  
  
 O RDS fornece os meios para executar a seguinte sequência de ações:  
  
-   Especifique o programa a ser invocado no servidor e obtenha uma maneira (proxy) para referir-se a ele do cliente ([RDS. Espaço de disco](../../reference/rds-api/dataspace-object-rds.md)).  
  
-   Invocar o programa do servidor. Passe parâmetros para o programa do servidor que identifica a fonte de dados e o comando a ser emitido (proxy ou [RDS. DataControl](../../reference/rds-api/datacontrol-object-rds.md)).  
  
-   O programa de servidor Obtém um objeto [Recordset](../../reference/ado-api/recordset-object-ado.md) da fonte de dados, normalmente usando o ADO. Opcionalmente, o objeto **Recordset** é processado no servidor ([RDSServer. datafactory](../../reference/rds-api/datafactory-object-rdsserver.md)).  
  
-   O programa de servidor retorna o objeto **Recordset** final para o aplicativo cliente (proxy).  
  
-   No cliente, o objeto **Recordset** é colocado em um formulário que pode ser facilmente usado por controles visuais (controle visual e **RDS. DataControl**).  
  
-   As alterações no objeto **Recordset** são enviadas de volta para o servidor e usadas para atualizar a fonte de dados (**RDS. DataControl** ou **RDSServer. datafactory**).  
  
## <a name="see-also"></a>Consulte Também  
 [Resumo do modelo de objeto RDS](./rds-object-model-summary.md)   
 [Objeto DataControl (RDS)](../../reference/rds-api/datacontrol-object-rds.md)   
 [Objeto datafactory (RDSServer)](../../reference/rds-api/datafactory-object-rdsserver.md)   
 [Objeto DataSpace (RDS)](../../reference/rds-api/dataspace-object-rds.md)   
 [Cenário de RDS](./rds-scenario.md)   
 [Tutorial do RDS](./rds-tutorial.md)   
 [Objeto Recordset (ADO)](../../reference/ado-api/recordset-object-ado.md)   
 [Segurança e uso RDS](./rds-usage-and-security.md)