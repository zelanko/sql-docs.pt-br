---
title: Modelo de programação do RDS básica | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 65dea5ebf2813267ef7e7bb83f2f37209ee2114f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47720874"
---
# <a name="basic-rds-programming-model"></a>Modelo de programação básica do RDS
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 RDS trata os aplicativos que existem no ambiente do seguinte: um aplicativo cliente especifica um programa que será executado em um servidor e os parâmetros necessários para retornar as informações desejadas. O programa invocado no servidor ganhos acesso à fonte de dados especificado, recupera as informações de, opcionalmente, processa os dados e, em seguida, retorna as informações resultantes ao seu aplicativo cliente em um formato que pode usar facilmente. O RDS fornece os meios para que você possa executar a seguinte sequência de ações:  
  
-   Especifique o programa a ser invocado no servidor e obter uma maneira de fazer referência a ele partir do cliente. (Essa referência é chamada, às vezes, uma *proxy*. Representa o programa de servidor remoto. O aplicativo cliente será "chamar" proxy como se fosse um programa local, mas ele realmente invoca o programa de servidor remoto.)  
  
-   Invocar o programa do servidor. Passe parâmetros para o programa de servidor que identifique a fonte de dados e emitir o comando. (O programa de servidor, na verdade, usa ADO para acessar a fonte de dados. ADO faz uma conexão com um dos parâmetros especificados e, em seguida, emite o comando especificado no parâmetro de.)  
  
-   O programa de servidor obtém um [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto da fonte de dados. Opcionalmente, o **Recordset** objeto for processado no servidor.  
  
-   O programa de servidor retorna o último **Recordset** objeto para o aplicativo cliente.  
  
-   No cliente, o **Recordset** objeto deve ser colocado em um formulário que pode ser facilmente usado por controles visuais.  
  
-   Todas as modificações a **Recordset** objeto são enviados para o programa de servidor, que usa para atualizar a fonte de dados.  
  
 Esse modelo de programação contém determinados recursos de conveniência. Se você não precisa de um programa de servidor complexas para acessar a fonte de dados e, se você fornecer a conexão necessária e os parâmetros de comando, RDS serão automaticamente recupere os dados especificados com um programa simples, de servidor padrão.  
  
 Se você precisar de processamento mais complexo, você pode especificar seu próprio programa de servidor personalizado. Por exemplo, como um programa de servidor personalizado tem toda a potência do ADO à sua disposição, ele pode se conectar a várias fontes de dados diferentes, combinar seus dados de alguma forma complexa e, em seguida, retornar um resultado simple, processado para o aplicativo cliente.  
  
 Por fim, se suas necessidades estiverem em algum lugar entre os dois, ADO agora dá suporte a personalizar o comportamento do programa de servidor padrão.  
  
## <a name="see-also"></a>Consulte também  
 [Modelo de programação do RDS em detalhes](../../../ado/guide/remote-data-service/rds-programming-model-in-detail.md)   
 [Cenário RDS](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [Tutorial RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Segurança e uso RDS](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


