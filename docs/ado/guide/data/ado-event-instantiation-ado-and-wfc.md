---
title: "Instanciação de evento do ADO: ADO e WFC | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 02/15/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9ee4be21-657b-407a-afa4-0b27a6b096ce
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4d46ec3bdad80879ddc4a931d8668a5298972e58
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="ado-event-instantiation-ado-and-wfc"></a>Instanciação de evento do ADO: ADO e WFC
ADO para Windows Foundation Classes (ADO/WFC) desenvolve o modelo de evento do ADO e apresenta uma interface de programação de aplicativo simplificado. Em geral, o ADO/WFC intercepta eventos ADO, consolida os parâmetros de evento em uma classe de evento único e, em seguida, chama o manipulador de eventos.  
  
### <a name="to-use-ado-events-in-adowfc"></a>Usar eventos de ADO no ADO/WFC  
  
1.  Defina seu próprio manipulador de eventos para processar um evento. Por exemplo, se você quiser processar o **ConnectComplete** evento o **ConnectionEvent** família, você pode usar este código:  
  
    ```  
    public void onConnectComplete(Object sender,ConnectionEvent e)  
    {  
        System.out.println("onConnectComplete:" + e);  
    }  
    ```  
  
2.  Defina um objeto de manipulador para representar o manipulador de eventos. O objeto do manipulador deve ser do tipo de dados **ConnectEventHandler** para um evento do tipo **ConnectionEvent**, tipo de dados ou **RecordsetEventHandler** para um evento do tipo ** RecordsetEvent**. Por exemplo, código a seguir para sua **ConnectComplete** manipulador de eventos:  
  
    ```  
    ConnectionEventHandler handler =   
        new ConnectionEventHandler(this, "onConnectComplete");  
    ```  
  
     O primeiro argumento do **ConnectionEventHandler** construtor é uma referência à classe que contém o manipulador de eventos chamado no segundo argumento.  
  
3.  Adicione o manipulador de eventos para uma lista de manipuladores designado para processar um determinado tipo de evento. Use o método com um nome como **addOn***EventName*(*manipulador*).  
  
4.  Internamente, o ADO/WFC implementa todos os manipuladores de eventos do ADO. Portanto, um evento gerado por um **Conexão** ou **registros** operação é interceptada por um manipulador de eventos de ADO/WFC.  
  
     O manipulador de eventos de ADO/WFC passa ADO **ConnectionEvent** parâmetros em uma instância do ADO/WFC **ConnectionEvent** classe ou ADO **RecordsetEvent** parâmetros em um instância do ADO/WFC **RecordsetEvent** classe. Essas classes de ADO/WFC consolidam os parâmetros de evento ADO; ou seja, cada classe de ADO/WFC contém um membro de dados para cada parâmetro exclusivo em todo o ADO **ConnectionEvent** ou **RecordsetEvent** métodos.  
  
5.  ADO/WFC, em seguida, chama o manipulador de eventos com o objeto de evento de ADO/WFC. Por exemplo, o **onConnectComplete** manipulador tem uma assinatura como este:  
  
    ```  
    public void onConnectComplete(Object sender,ConnectionEvent e)  
    ```  
  
     O primeiro argumento é do tipo de objeto que enviou o evento ([Conexão](../../../ado/reference/ado-api/connection-object-ado.md) ou [registros](../../../ado/reference/ado-api/recordset-object-ado.md)), e o segundo argumento é o objeto de evento de ADO/WFC (**ConnectionEvent** ou **RecordsetEvent**).  
  
     A assinatura do seu manipulador de eventos é mais simples do que um evento de ADO. No entanto, você ainda deve entender o modelo de evento do ADO para saber quais parâmetros são aplicados a um evento e como responder.  
  
6.  Retorna o manipulador de eventos para o manipulador de ADO/WFC para o evento de ADO. ADO/WFC copia os membros de dados de evento de ADO/WFC pertinentes para os parâmetros de evento do ADO e, em seguida, retorna o manipulador de eventos do ADO.  
  
7.  Quando tiver terminado de processamento, remova o manipulador da lista de manipuladores de eventos de ADO/WFC. Use o método com um nome como **removeOn***EventName*(*manipulador*).  
  
## <a name="see-also"></a>Consulte também  
 [Resumo de manipulador de eventos de ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [ADO - índice de sintaxe do WFC](../../../ado/reference/ado-api/ado-wfc-syntax-index.md)   
 [Parâmetros de evento](../../../ado/guide/data/event-parameters.md)   
 [Como os manipuladores de eventos funcionam em conjunto](../../../ado/guide/data/how-event-handlers-work-together.md)   
 [Tipos de eventos](../../../ado/guide/data/types-of-events.md)

