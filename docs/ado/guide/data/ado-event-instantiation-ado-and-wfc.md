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
manager: craigg
ms.openlocfilehash: 753deabf2c8ae69c535b60f5c43dca20b002ed63
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63063002"
---
# <a name="ado-event-instantiation-ado-and-wfc"></a>Instanciação de evento ADO: ADO e WFC
ADO para Windows Foundation Classes (ADO/WFC) se baseia no modelo de evento ADO e apresenta uma interface de programação de aplicativos simplificado. Em geral, o ADO/WFC intercepta eventos ADO, consolida os parâmetros de evento em uma classe de evento único e, em seguida, chama o manipulador de eventos.  
  
### <a name="to-use-ado-events-in-adowfc"></a>Usar eventos ADO no ADO/WFC  
  
1.  Defina seu próprio manipulador de eventos para processar um evento. Por exemplo, se você quiser processar os **eventos ConnectComplete** evento na **ConnectionEvent** família, você pode usar este código:  
  
    ```  
    public void onConnectComplete(Object sender,ConnectionEvent e)  
    {  
        System.out.println("onConnectComplete:" + e);  
    }  
    ```  
  
2.  Defina um objeto de manipulador para representar seu manipulador de eventos. O objeto de manipulador deve ser do tipo de dados **ConnectEventHandler** para um evento do tipo **ConnectionEvent**, ou o tipo de dados **RecordsetEventHandler** para um evento do tipo  **RecordsetEvent**. Por exemplo, código a seguir para seu **eventos ConnectComplete** manipulador de eventos:  
  
    ```  
    ConnectionEventHandler handler =   
        new ConnectionEventHandler(this, "onConnectComplete");  
    ```  
  
     O primeiro argumento do **ConnectionEventHandler** construtor é uma referência à classe que contém o manipulador de eventos chamado no segundo argumento.  
  
3.  Adicione o manipulador de eventos para uma lista de manipuladores designado para processar um determinado tipo de evento. Use o método com um nome, como **addOn** *EventName*(*manipulador*).  
  
4.  Internamente, o ADO/WFC implementa todos os manipuladores de evento ADO. Portanto, um evento é causado por uma **Conexão** ou **Recordset** operação é interceptada por um manipulador de eventos ADO/WFC.  
  
     O manipulador de eventos ADO/WFC passa ADO **ConnectionEvent** parâmetros em uma instância do ADO/WFC **ConnectionEvent** classe ou ADO **RecordsetEvent** parâmetros em um instância do ADO/WFC **RecordsetEvent** classe. Essas classes de ADO/WFC consolidam os parâmetros de evento ADO; ou seja, cada classe de ADO/WFC contém um membro de dados para cada parâmetro exclusivo em todos os ADO **ConnectionEvent** ou **RecordsetEvent** métodos.  
  
5.  ADO/WFC, em seguida, chama o manipulador de eventos com o objeto de evento ADO/WFC. Por exemplo, sua **onConnectComplete** manipulador tem uma assinatura como esta:  
  
    ```  
    public void onConnectComplete(Object sender,ConnectionEvent e)  
    ```  
  
     O primeiro argumento é o tipo de objeto que enviou o evento ([Conexão](../../../ado/reference/ado-api/connection-object-ado.md) ou [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md)), e o segundo argumento é o objeto de evento ADO/WFC (**ConnectionEvent** ou **RecordsetEvent**).  
  
     A assinatura do seu manipulador de eventos é mais simples do que um evento do ADO. No entanto, ainda é necessário entender o modelo de evento ADO saber quais parâmetros se aplicam a um evento e como responder.  
  
6.  Retornar do seu manipulador de eventos para o manipulador de ADO/WFC para o evento do ADO. ADO/WFC copia os membros de dados de evento ADO/WFC pertinentes para os parâmetros de evento ADO e, em seguida, o manipulador de eventos ADO retorna.  
  
7.  Quando tiver terminado de processamento, remover o manipulador da lista de manipuladores de eventos ADO/WFC. Use o método com um nome, como **removeOn** *EventName*(*manipulador*).  
  
## <a name="see-also"></a>Consulte também  
 [Resumo do manipulador de eventos ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [ADO - WFC Syntax Index](../../../ado/reference/ado-api/ado-wfc-syntax-index.md)   
 [Parâmetros de evento](../../../ado/guide/data/event-parameters.md)   
 [Como os manipuladores de eventos funcionam juntos](../../../ado/guide/data/how-event-handlers-work-together.md)   
 [Tipos de eventos](../../../ado/guide/data/types-of-events.md)
