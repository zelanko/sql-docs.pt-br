---
title: Modelo de programação do RDS em detalhes | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b511f5d241216c2586870adadeb3c8586ee803be
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/12/2018
ms.locfileid: "51560453"
---
# <a name="rds-programming-model-in-detail"></a>Modelo de programação do RDS em detalhes
Estes são os principais elementos do modelo de programação do RDS:  
  
-   RDS.DataSpace  
  
-   RDSServer.DataFactory  
  
-   RDS.DataControl  
  
-   Evento  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="rdsdataspace"></a>RDS.DataSpace  
 O aplicativo cliente deve especificar o servidor e o programa de servidor para invocar. Em troca, seu aplicativo recebe uma referência para o programa de servidor e pode tratar a referência, como se fosse o próprio programa de servidor.  
  
 O modelo de objeto RDS incorpora essa funcionalidade com o [RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) objeto.  
  
 O programa de servidor é especificado com um identificador de programa, ou *ProgID*. O servidor usa o *ProgID* e registro do computador servidor para localizar informações sobre o programa real para iniciar.  
  
 RDS faz uma distinção internamente, dependendo se o programa de servidor está em um servidor remoto pela Internet ou intranet; um servidor em uma rede local; ou não em um servidor, mas em vez disso, em uma biblioteca de vínculo dinâmico (DLL) local. Essa distinção determina como as informações são trocadas entre o cliente e o servidor e fazem uma diferença tangível no tipo de referência retornada ao aplicativo cliente. No entanto, do seu ponto de Vista, essa distinção não tem significado especial. Tudo o que importa é que você receba uma referência de programa utilizável.  
  
## <a name="rdsserverdatafactory"></a>RDSServer.DataFactory  
 O RDS fornece um programa de servidor padrão que pode executar uma consulta SQL em relação à fonte de dados e retornar um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) do objeto ou tomar um **conjunto de registros** do objeto e atualizar a fonte de dados.  
  
 O modelo de objeto RDS incorpora essa funcionalidade com o [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) objeto.  
  
 Além disso, esse objeto tem um método para criar vazio **conjunto de registros** objeto que você pode preencher programaticamente ([CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md)) e o outro método para converter um **conjunto de registros**  objeto em uma cadeia de caracteres de texto para criar uma página da Web ([ConvertToString](../../../ado/reference/rds-api/converttostring-method-rds.md)).  
  
 Com o ADO, você pode substituir alguns da conexão padrão e o comportamento de comando do **RDSServer.DataFactory** com um **DataFactory** manipulador e um arquivo de personalização que contém a conexão, comando, e parâmetros de segurança.  
  
 O programa de servidor é chamado, às vezes, uma *objeto comercial*. Você pode escrever seu próprio objeto de negócios personalizada que pode executar acesso a dados complicada, verificações de validade e assim por diante. Até mesmo ao gravar um objeto comercial personalizado, você pode criar uma instância de um **RDSServer.DataFactory** de objeto e usar alguns de seus métodos para realizar suas próprias tarefas.  
  
## <a name="rdsdatacontrol"></a>RDS.DataControl  
 O RDS fornece um meio para combinar a funcionalidade do **RDS. DataSpace** e **RDSServer.DataFactory**e também habilitar controles visuais usar facilmente o **conjunto de registros** objeto retornado por uma consulta de uma fonte de dados. Tentativas de RDS, para o caso mais comum, para fazer tanto quanto possível para obter acesso a informações em um servidor e exibi-lo em um controle visual automaticamente.  
  
 O modelo de objeto RDS incorpora essa funcionalidade com o [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto.  
  
 O **RDS. DataControl** tem dois aspectos. Um aspecto se refere à fonte de dados. Se você definir o comando e as informações de conexão usando o **Connect** e **SQL** propriedades do **RDS. DataControl**, ele usará automaticamente o **RDS. DataSpace** para criar uma referência para o padrão **RDSServer.DataFactory** objeto. Em seguida, a **RDSServer.DataFactory** usará o **Connect** valor da propriedade para se conectar à fonte de dados, use o **SQL** valor da propriedade para obter um  **Conjunto de registros** na fonte de dados e retornar o **conjunto de registros** do objeto para o **RDS. DataControl**.  
  
 O segundo aspecto pertence à exibição da retornada **Recordset** informações em um controle visual. Você pode associar um controle visual com o **RDS. DataControl** (em um processo chamado associação) e obter acesso às informações no associado **Recordset** objeto, exibindo os resultados da consulta em uma página da Web no Microsoft® Internet Explorer. Cada **RDS. DataControl** objeto é associado a um **Recordset** objeto, que representa os resultados de uma única consulta, para um ou mais controles visuais (por exemplo, uma caixa de texto, caixa de combinação, controle de grade e assim por diante). Pode haver mais de um **RDS. DataControl** objeto em cada página. Cada **RDS. DataControl** objeto pode ser conectado a uma fonte de dados diferentes e conterá os resultados de uma consulta separada.  
  
 O **RDS. DataControl** objeto também tem seus próprios métodos para navegar, classificar e filtrar as linhas do associado **Recordset** objeto. Esses métodos são semelhantes, mas não o mesmo que os métodos em ADO **Recordset** objeto.  
  
## <a name="events"></a>Eventos  
 RDS dá suporte a dois dos seus próprios eventos, que são independentes do modelo de evento ADO. O [onReadyStateChange](../../../ado/reference/rds-api/onreadystatechange-event-rds.md) evento é chamado sempre que o **RDS. DataControl** [ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md) alterações de propriedade, o que os notifica você quando uma operação assíncrona for concluída com êxito, encerrado ou ocorreu um erro. O [onError](../../../ado/reference/rds-api/onerror-event-rds.md) eventos é chamado sempre que ocorrer um erro, mesmo se o erro ocorre durante uma operação assíncrona.  
  
> [!NOTE]
>  Microsoft Internet Explorer fornece dois eventos adicionais ao RDS: **onDataSetChanged**, que indica que o **conjunto de registros** é funcional, mas ainda recuperar linhas, e  **onDataSetComplete**, que indica que o **Recordset** concluir a recuperação de linhas.  
  
## <a name="see-also"></a>Consulte também  
 [Modelo de programação do RDS com objetos](../../../ado/guide/remote-data-service/rds-programming-model-with-objects.md)   
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [Objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)   
 [Objeto DataSpace (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)   
 [Cenário RDS](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [Tutorial RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Segurança e uso RDS](../../../ado/guide/remote-data-service/rds-usage-and-security.md)



