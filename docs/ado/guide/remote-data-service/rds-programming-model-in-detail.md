---
title: Modelo de programação de RDS em detalhes | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS programming model [ADO], details
ms.assetid: 3e57af8d-519b-4467-a0bd-af468534cefd
author: rothja
ms.author: jroth
ms.openlocfilehash: 6bf59580985a4c46fa163a00423bb7dd90ad9463
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82747752"
---
# <a name="rds-programming-model-in-detail"></a>Modelo de programação do RDS em detalhes
Veja a seguir os principais elementos do modelo de programação RDS:  
  
-   RDS.DataSpace  
  
-   RDSServer.DataFactory  
  
-   RDS.DataControl  
  
-   Evento  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="rdsdataspace"></a>RDS.DataSpace  
 O aplicativo cliente deve especificar o servidor e o programa de servidor a serem invocados. Em retorno, seu aplicativo recebe uma referência para o programa do servidor e pode tratar a referência como se fosse o próprio programa do servidor.  
  
 O modelo de objeto RDS incorpora essa funcionalidade com o [RDS. Objeto DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) .  
  
 O programa de servidor é especificado com um identificador de programa ou *ProgID*. O servidor usa o *ProgID* e o registro da máquina do servidor para localizar informações sobre o programa real a ser iniciado.  
  
 O RDS faz uma distinção interna, dependendo se o programa do servidor está em um servidor remoto na Internet ou em uma intranet; um servidor em uma rede local; ou não em um servidor, mas em uma DLL (biblioteca de vínculo dinâmico) local. Essa distinção determina como as informações são trocadas entre o cliente e o servidor e faz uma diferença tangível no tipo de referência retornado ao aplicativo cliente. No entanto, do ponto de vista, essa distinção não tem um significado especial. Tudo o que importa é que você receba uma referência de programa utilizável.  
  
## <a name="rdsserverdatafactory"></a>RDSServer.DataFactory  
 O RDS fornece um programa de servidor padrão que pode executar uma consulta SQL na fonte de dados e retornar um objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) ou pegar um objeto **Recordset** e atualizar a fonte de dados.  
  
 O modelo de objeto RDS incorpora essa funcionalidade ao objeto [RDSServer. datafactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) .  
  
 Além disso, esse objeto tem um método para criar um objeto **Recordset** vazio que você pode preencher programaticamente ([createrecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md)) e outro método para converter um objeto **Recordset** em uma cadeia de texto para criar uma página da Web ([ConvertToString](../../../ado/reference/rds-api/converttostring-method-rds.md)).  
  
 Com o ADO, você pode substituir alguns dos comportamentos padrão de conexão e comando do **RDSServer. datafactory** por um manipulador **DataFactory** e um arquivo de personalização que contém parâmetros de conexão, comando e segurança.  
  
 O programa de servidor, às vezes, é chamado de *objeto comercial*. Você pode escrever seu próprio objeto comercial personalizado que pode executar o acesso a dados complicado, verificações de validade e assim por diante. Mesmo ao escrever um objeto comercial personalizado, você pode criar uma instância de um objeto **RDSServer. datafactory** e usar alguns de seus métodos para realizar suas próprias tarefas.  
  
## <a name="rdsdatacontrol"></a>RDS.DataControl  
 O RDS fornece um meio de combinar a funcionalidade do **RDS. DataSpace** e **RDSServer. datafactory**e também permitem que os controles visuais usem facilmente o objeto **Recordset** retornado por uma consulta de uma fonte de dados. Tentativas de RDS, para o caso mais comum, para fazer o máximo possível para obter acesso automaticamente a informações em um servidor e exibi-las em um controle visual.  
  
 O modelo de objeto RDS incorpora essa funcionalidade com o [RDS. Objeto DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) .  
  
 O **RDS. O DataControl** tem dois aspectos. Um aspecto refere-se à fonte de dados. Se você definir as informações de conexão e de comando usando as propriedades **Connect** e **SQL** do **RDS. O DataControl**, ele usará automaticamente o **RDS. DataSpace** para criar uma referência ao objeto padrão **RDSServer. datafactory** . Em seguida, o **RDSServer. datafactory** usará o valor da propriedade **Connect** para se conectar à fonte de dados, usará o valor da propriedade **SQL** para obter um **conjunto de registros** da fonte de dados e retornará o objeto **Recordset** para o **RDS. Controle**de data.  
  
 O segundo aspecto refere-se à exibição de informações do **conjunto de registros** retornado em um controle visual. Você pode associar um controle visual com o **RDS. DataControl** (em um processo chamado Binding) e obter acesso às informações no objeto **Recordset** associado, exibindo os resultados da consulta em uma página da Web no Microsoft® Internet Explorer. Cada **RDS. O objeto DataControl** associa um objeto **Recordset** , representando os resultados de uma única consulta, a um ou mais controles visuais (por exemplo, uma caixa de texto, caixa de combinação, controle de grade e assim por diante). Pode haver mais de um **RDS. Objeto DataControl** em cada página. Cada **RDS. O objeto DataControl** pode ser conectado a uma fonte de dados diferente e conter os resultados de uma consulta separada.  
  
 O **RDS. O objeto DataControl** também tem seus próprios métodos para navegar, classificar e filtrar as linhas do objeto **Recordset** associado. Esses métodos são semelhantes, mas não os mesmos que os métodos no objeto **Recordset** do ADO.  
  
## <a name="events"></a>Eventos  
 O RDS dá suporte a dois de seus próprios eventos, que são independentes do modelo de evento ADO. O evento [onReadyStateChange](../../../ado/reference/rds-api/onreadystatechange-event-rds.md) é chamado sempre que o **RDS. A propriedade DataControl** [ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md) muda, notificando você quando uma operação assíncrona tiver sido concluída com êxito, encerrada ou sofreu um erro. O evento [OnError](../../../ado/reference/rds-api/onerror-event-rds.md) é chamado sempre que ocorrer um erro, mesmo se o erro ocorrer durante uma operação assíncrona.  
  
> [!NOTE]
>  O Microsoft Internet Explorer fornece dois eventos adicionais para RDS: **ondatasetchanged**, que indica que o **conjunto de registros** é funcional, mas ainda recupera linhas e **onDataSetComplete**, o que indica que o conjunto de **registros** concluiu a recuperação de linhas.  
  
## <a name="see-also"></a>Consulte Também  
 [Modelo de programação de RDS com objetos](../../../ado/guide/remote-data-service/rds-programming-model-with-objects.md)   
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [Objeto datafactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)   
 [Objeto DataSpace (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)   
 [Cenário de RDS](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [Tutorial do RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Segurança e uso RDS](../../../ado/guide/remote-data-service/rds-usage-and-security.md)



