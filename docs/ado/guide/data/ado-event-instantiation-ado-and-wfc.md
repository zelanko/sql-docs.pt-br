---
title: 'Instanciação de evento ADO: ADO e WFC | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 9ee4be21-657b-407a-afa4-0b27a6b096ce
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7dbbbf92c751093d2a7333b7ac1f76888d41d345
ms.sourcegitcommit: 734529a6f108e6ee6bfce939d8be562d405e1832
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2019
ms.locfileid: "70212334"
---
# <a name="ado-event-instantiation-ado-and-wfc"></a>Instanciação de evento ADO: ADO e WFC
O ADO para Windows Foundation classes (ADO/WFC) se baseia no modelo de evento ADO e apresenta uma interface de programação de aplicativo simplificada. Em geral, o ADO/WFC intercepta eventos ADO, consolida os parâmetros de evento em uma única classe de evento e, em seguida, chama o manipulador de eventos.  
  
### <a name="to-use-ado-events-in-adowfc"></a>Para usar eventos ADO no ADO/WFC  
  
1.  Defina seu próprio manipulador de eventos para processar um evento. Por exemplo, se você quisesse processar o evento **ConnectComplete** na família **ConnectionEvent** , você pode usar este código:  
  
    ```  
    public void onConnectComplete(Object sender,ConnectionEvent e)  
    {  
        System.out.println("onConnectComplete:" + e);  
    }  
    ```  
  
2.  Defina um objeto de manipulador para representar seu manipulador de eventos. O objeto Handler deve ser do tipo de dados **ConnectEventHandler** para um evento do tipo **ConnectionEvent**ou tipo de dados **RecordsetEventHandler** para um evento do tipo **RecordsetEvent**. Por exemplo, codifique o seguinte para o manipulador de eventos **ConnectComplete** :  
  
    ```  
    ConnectionEventHandler handler =   
        new ConnectionEventHandler(this, "onConnectComplete");  
    ```  
  
     O primeiro argumento do construtor **ConnectionEventHandler** é uma referência à classe que contém o manipulador de eventos chamado no segundo argumento.  
  
3.  Adicione seu manipulador de eventos a uma lista de manipuladores designados para processar um determinado tipo de evento. Use o método com um nome como EventName (*manipulador*) de **addOn**.  
  
4.  O ADO/WFC implementa internamente todos os manipuladores de eventos do ADO. Portanto, um evento causado por uma **conexão** ou operação de **conjunto de registros** é interceptado por um manipulador de eventos ADO/wfc.  
  
     O manipulador de eventos ADO/WFC passa parâmetros ADO **ConnectionEvent** em uma instância da classe ADO/WFC **CONNECTIONEVENT** ou parâmetros ADO **RecordsetEvent** em uma instância da classe ADO/WFC **RecordsetEvent** . Essas classes ADO/WFC consolidam os parâmetros do evento ADO; ou seja, cada classe ADO/WFC contém um membro de dados para cada parâmetro exclusivo em todos os métodos **ConnectionEvent** ou **RecordsetEvent** do ADO.  
  
5.  Em seguida, o ADO/WFC chama o manipulador de eventos com o objeto de evento ADO/WFC. Por exemplo, o manipulador **onConnectComplete** tem uma assinatura como esta:  
  
    ```  
    public void onConnectComplete(Object sender,ConnectionEvent e)  
    ```  
  
     O primeiro argumento é o tipo de objeto que enviou o evento ([conexão](../../../ado/reference/ado-api/connection-object-ado.md) ou [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md)) e o segundo argumento é o objeto de evento ADO/wfc (**ConnectionEvent** ou **RecordsetEvent**).  
  
     A assinatura do manipulador de eventos é mais simples do que um evento ADO. No entanto, você ainda deve entender o modelo de evento ADO para saber quais parâmetros se aplicam a um evento e como responder.  
  
6.  Retornar do manipulador de eventos para o manipulador ADO/WFC do evento ADO. O ADO/WFC copia os membros de dados do evento ADO/WFC pertinentes de volta para os parâmetros do evento ADO e, em seguida, o manipulador de eventos do ADO retorna.  
  
7.  Quando você terminar de processar, remova seu manipulador da lista de manipuladores de eventos ADO/WFC. Use o método com um nome como **remover**_EventName_(*manipulador*).  
  
## <a name="see-also"></a>Consulte também  
 [Resumo do manipulador de eventos do ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Índice de sintaxe ADO-WFC](../../../ado/reference/ado-api/ado-wfc-syntax-index.md)   
 [Parâmetros do evento](../../../ado/guide/data/event-parameters.md)   
 [Como os manipuladores de eventos funcionam juntos](../../../ado/guide/data/how-event-handlers-work-together.md)   
 [Tipos de eventos](../../../ado/guide/data/types-of-events.md)
