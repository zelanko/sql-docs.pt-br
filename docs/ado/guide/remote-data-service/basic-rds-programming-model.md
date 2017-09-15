---
title: "Modelo de programação de RDS básica | Microsoft Docs"
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
ms.assetid: 0bdd236b-edff-4aac-94c3-93e1465ca6c5
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d99d092b91ed150a3ad9163f2c4f7e513554e9f4
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="basic-rds-programming-model"></a>Modelo de programação de RDS básica
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 RDS endereços aplicativos que existem no seguinte ambiente: um aplicativo cliente especifica um programa que será executado em um servidor e os parâmetros necessários para retornar as informações desejadas. O programa de chamada no servidor ganhos acesso à fonte de dados especificado, recupera as informações de, opcionalmente processa os dados e, em seguida, retorna as informações resultantes ao seu aplicativo cliente em um formulário que pode usar facilmente. RDS fornece os meios para executar a seguinte sequência de ações:  
  
-   Especifique o programa a ser invocado no servidor e obter uma maneira de fazer referência a ele do cliente. (Essa referência às vezes é chamada um *proxy*. Representa o programa de servidor remoto. O aplicativo cliente "ligar" proxy como se fosse um programa local, mas na verdade, ele chama o programa de servidor remoto.)  
  
-   Invoque o programa do servidor. Passe parâmetros para o programa do servidor que identifique a fonte de dados e emitir o comando. (O programa do servidor, na verdade, usa ADO para acessar a fonte de dados. ADO faz uma conexão com um dos parâmetros de determinada e, em seguida, emite o comando especificado no parâmetro de.)  
  
-   O programa de servidor obtém um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto da fonte de dados. Opcionalmente, o **registros** objeto for processado no servidor.  
  
-   O programa do servidor retorna o último **registros** objeto para o aplicativo cliente.  
  
-   No cliente, o **registros** objeto é colocado em um formulário que pode ser usado facilmente por controles de visual.  
  
-   Todas as modificações de **registros** objeto são enviadas de volta para o programa de servidor, que usa para atualizar a fonte de dados.  
  
 Este modelo de programação contém alguns recursos de conveniência. Se você não precisa de um programa de servidor complexas para acessar a fonte de dados e, se você fornecer a conexão necessário e os parâmetros de comando, RDS serão automaticamente recupere os dados especificados com um programa simples, do servidor padrão.  
  
 Se você precisar de processamento mais complexo, você pode especificar seu próprio programa de servidor personalizado. Por exemplo, como um programa de servidor personalizado tem todo o poder do ADO à sua disposição, ele pode se conectar a várias fontes de dados diferentes, combinar os dados de alguma forma complexa e, em seguida, retornar um resultado de simple e processado para o aplicativo cliente.  
  
 Por fim, se suas necessidades em algum lugar no meio, ADO agora dá suporte a personalizar o comportamento do programa de servidor padrão.  
  
## <a name="see-also"></a>Consulte também  
 [Modelo de programação de RDS em detalhes](../../../ado/guide/remote-data-service/rds-programming-model-in-detail.md)   
 [Cenário RDS](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [Tutorial RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Segurança e uso RDS](../../../ado/guide/remote-data-service/rds-usage-and-security.md)



