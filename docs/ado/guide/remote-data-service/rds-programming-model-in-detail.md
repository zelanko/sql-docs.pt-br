---
title: "Modelo de programação de RDS em detalhes | Microsoft Docs"
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
- RDS programming model [ADO], details
ms.assetid: 3e57af8d-519b-4467-a0bd-af468534cefd
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: db8a1222c560b54629baa34da595e0f5c49835b0
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="rds-programming-model-in-detail"></a>Modelo de programação de RDS em detalhes
Estes são os principais elementos do modelo de programação de RDS:  
  
-   RDS. Espaço de dados  
  
-   RDSServer.DataFactory  
  
-   RDS. DataControl  
  
-   Evento  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="rdsdataspace"></a>RDS. Espaço de dados  
 O aplicativo cliente deve especificar o servidor e o programa de servidor para invocar. Em troca, seu aplicativo recebe uma referência para o programa do servidor e pode tratar a referência como se fosse o programa do servidor.  
  
 O modelo de objeto do RDS incorpora essa funcionalidade com o [RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) objeto.  
  
 O programa de servidor é especificado com um identificador de programa, ou *ProgID*. O servidor usa o *ProgID* e o registro da máquina do servidor para localizar informações sobre o programa real para iniciar.  
  
 RDS faz uma distinção internamente dependendo se o programa de servidor está em um servidor remoto pela Internet ou intranet; um servidor em uma rede local; ou não em um servidor, mas em vez disso, em uma biblioteca de vínculo dinâmico (DLL) local. Essa distinção determina como as informações são trocadas entre o cliente e o servidor e fazem diferença tangível no tipo de referência retornado ao seu aplicativo cliente. No entanto, de seu ponto de Vista, essa distinção não tem significado especial. O que importa é que você recebe uma referência de programa utilizável.  
  
## <a name="rdsserverdatafactory"></a>RDSServer.DataFactory  
 RDS fornece um programa de servidor padrão que pode executar uma consulta SQL em relação à fonte de dados e retornar um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) do objeto ou colocar um **Recordset** do objeto e atualizar a fonte de dados.  
  
 O modelo de objeto do RDS incorpora essa funcionalidade com o [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) objeto.  
  
 Além disso, esse objeto tem um método para criar um vazio **registros** objeto que você pode preencher programaticamente ([CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md)) e o outro método para converter um **conjunto de registros**  objeto em uma cadeia de caracteres de texto para criar uma página da Web ([ConvertToString](../../../ado/reference/rds-api/converttostring-method-rds.md)).  
  
 Com o ADO, você pode substituir alguns a conexão padrão e o comportamento do comando do **RDSServer.DataFactory** com um **DataFactory** manipulador e um arquivo de personalização que contém a conexão, comando, e parâmetros de segurança.  
  
 O programa de servidor às vezes é chamado um *objeto comercial*. Você pode escrever seu próprio objeto de negócios personalizada que pode executar acesso a dados complicada, as verificações de validade e assim por diante. Mesmo ao gravar um objeto comercial personalizado, você pode criar uma instância de um **RDSServer.DataFactory** do objeto e usar alguns dos seus métodos para realizar suas próprias tarefas.  
  
## <a name="rdsdatacontrol"></a>RDS. DataControl  
 RDS fornece um meio para combinar a funcionalidade do **RDS. DataSpace** e **RDSServer.DataFactory**e também habilitar controles visuais usar com facilidade o **registros** objeto retornado por uma consulta de fonte de dados. Tentativas de RDS, para o caso mais comum, para fazer tanto quanto possível para obter acesso a informações em um servidor e exibi-lo em um controle visual automaticamente.  
  
 O modelo de objeto do RDS incorpora essa funcionalidade com o [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto.  
  
 O **RDS. DataControl** tem dois aspectos. Um aspecto referem-se à fonte de dados. Se você definir o comando e informações de conexão usando o **conectar** e **SQL** propriedades do **RDS. DataControl**, ele usará automaticamente o **RDS. DataSpace** para criar uma referência para o padrão **RDSServer.DataFactory** objeto. Em seguida, o **RDSServer.DataFactory** usará o **conectar** valor da propriedade para se conectar à fonte de dados, use o **SQL** valor da propriedade para obter um  **Conjunto de registros** da fonte de dados e retornar o **registros** o objeto para o **RDS. DataControl**.  
  
 O segundo aspecto referente à exibição da retornado **registros** informações em um controle visual. Você pode associar um controle visual com o **RDS. DataControl** (em um processo chamado associação) e obter acesso a informações associada **registros** objeto, exibindo os resultados da consulta em uma página da Web no Microsoft® Internet Explorer. Cada **RDS. DataControl** objeto associa um **registros** objeto, que representa os resultados de uma única consulta, para um ou mais controles visual (por exemplo, uma caixa de texto, caixa de combinação, controle de grade e assim por diante). Pode haver mais de um **RDS. DataControl** objeto em cada página. Cada **RDS. DataControl** objeto pode ser conectado a uma fonte de dados diferentes e contêm os resultados de uma consulta separada.  
  
 O **RDS. DataControl** objeto também tem seus próprios métodos para navegar, classificar e filtrar as linhas de associado **registros** objeto. Esses métodos são semelhantes, mas não o mesmo que os métodos no ADO **registros** objeto.  
  
## <a name="events"></a>Eventos  
 RDS dá suporte a dois dos seus próprios eventos, que são independentes do modelo de evento do ADO. O [onReadyStateChange](../../../ado/reference/rds-api/onreadystatechange-event-rds.md) evento é chamado sempre que o **RDS. DataControl** [estado de prontidão é](../../../ado/reference/rds-api/readystate-property-rds.md) alterações de propriedade, notificando você quando uma operação assíncrona for concluída com êxito, encerrada ou ocorreu um erro. O [onError](../../../ado/reference/rds-api/onerror-event-rds.md) evento é chamado sempre que ocorrer um erro, mesmo se o erro ocorrer durante uma operação assíncrona.  
  
> [!NOTE]
>  O Microsoft Internet Explorer fornece dois eventos adicionais ao RDS: **onDataSetChanged**, que indica que o **registros** é funcional, mas ainda recuperar linhas, e  **onDataSetComplete**, que indica que o **registros** concluir a recuperação de linhas.  
  
## <a name="see-also"></a>Consulte também  
 [Modelo de programação de RDS com objetos](../../../ado/guide/remote-data-service/rds-programming-model-with-objects.md)   
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [Objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)   
 [Objeto de espaço de dados (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)   
 [Cenário RDS](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [Tutorial RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Segurança e uso RDS](../../../ado/guide/remote-data-service/rds-usage-and-security.md)




