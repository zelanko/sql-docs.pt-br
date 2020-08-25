---
description: Modelo de programação básica do RDS
title: Modelo de programação RDS básica | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS programming model [ADO]
ms.assetid: 0bdd236b-edff-4aac-94c3-93e1465ca6c5
author: rothja
ms.author: jroth
ms.openlocfilehash: ba02a22b987384e48a750705fa3c2baf6965f920
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88758746"
---
# <a name="basic-rds-programming-model"></a>Modelo de programação básica do RDS
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Os aplicativos RDS que existem no seguinte ambiente: um aplicativo cliente especifica um programa que será executado em um servidor e os parâmetros necessários para retornar as informações desejadas. O programa invocado no servidor obtém acesso à fonte de dados especificada, recupera as informações, opcionalmente processa os dados e, em seguida, retorna as informações resultantes para o aplicativo cliente em um formato que possa ser usado facilmente. O RDS fornece os meios para que você execute a seguinte sequência de ações:  
  
-   Especifique o programa a ser invocado no servidor e obtenha uma maneira de consultá-lo a partir do cliente. (Às vezes, essa referência é chamada de *proxy*. Representa o programa do servidor remoto. O aplicativo cliente "chamará" o proxy como se fosse um programa local, mas, na verdade, invoca o programa do servidor remoto.)  
  
-   Invocar o programa do servidor. Passe parâmetros para o programa do servidor que identifica a fonte de dados e o comando a ser emitido. (O programa de servidor realmente usa o ADO para obter acesso à fonte de dados. O ADO faz uma conexão com um dos parâmetros especificados e, em seguida, emite o comando especificado no outro parâmetro.)  
  
-   O programa de servidor Obtém um objeto [Recordset](../../reference/ado-api/recordset-object-ado.md) da fonte de dados. Opcionalmente, o objeto **Recordset** é processado no servidor.  
  
-   O programa de servidor retorna o objeto **Recordset** final para o aplicativo cliente.  
  
-   No cliente, o objeto **Recordset** é colocado em um formulário que pode ser facilmente usado por controles visuais.  
  
-   Todas as modificações no objeto **Recordset** são enviadas de volta para o programa do servidor, o que os utiliza para atualizar a fonte de dados.  
  
 Esse modelo de programação contém determinados recursos de conveniência. Se você não precisar de um programa de servidor complexo para acessar a fonte de dados e se fornecer a conexão necessária e os parâmetros de comando, o RDS recuperará automaticamente os dados especificados com um programa de servidor padrão simples.  
  
 Se precisar de processamento mais complexo, você poderá especificar seu próprio programa de servidor personalizado. Por exemplo, como um programa de servidor personalizado tem todo o potencial do ADO em sua disposição, ele pode se conectar a várias fontes de dados diferentes, combinar seus dados de alguma maneira complexa e retornar um resultado simples e processado para o aplicativo cliente.  
  
 Por fim, se suas necessidades estiverem em algum lugar entre elas, o ADO agora dará suporte à personalização do comportamento do programa servidor padrão.  
  
## <a name="see-also"></a>Consulte Também  
 [Modelo de programação de RDS em detalhes](./rds-programming-model-in-detail.md)   
 [Cenário de RDS](./rds-scenario.md)   
 [Tutorial do RDS](./rds-tutorial.md)   
 [Objeto Recordset (ADO)](../../reference/ado-api/recordset-object-ado.md)   
 [Segurança e uso RDS](./rds-usage-and-security.md)