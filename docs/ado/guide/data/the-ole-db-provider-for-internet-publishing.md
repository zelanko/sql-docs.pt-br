---
title: "O provedor do OLE DB para publicação na Internet | Microsoft Docs"
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
- OLE DB provider for Internet publishing [ADO]
- ADO, Internet publishing
- publishing to Internet [ADO]
- Internet publishing [ADO]
- providers [ADO], OLE DB provider for Internet publishing
ms.assetid: 4869aafa-7401-4ce1-93ce-45406a60274f
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c19f0a93a5f7f685d7cd8dcdf6d916ae3955cff8
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="the-ole-db-provider-for-internet-publishing"></a>O provedor do OLE DB para publicação na Internet
O ADO [registro](../../../ado/reference/ado-api/record-object-ado.md) e [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) objetos podem ser usados com o Microsoft OLE DB Provider para publicação de Internet (provedor de publicação de Internet) para acessar e manipular os recursos, como arquivos ou pastas da Web atendido pelo Microsoft FrontPage. Com o ADO, você pode especificar a origem de um **registro**, **fluxo**, ou [registros](../../../ado/reference/ado-api/recordset-object-ado.md) ser uma URL. Você pode, em seguida, carregar, baixar, mover, copiar e excluir recursos ou manipular diretamente as propriedades do recurso.  
  
 Por exemplo de código que usa **registros** e **fluxos** com o provedor de publicação de Internet, consulte o [cenário de publicação de Internet](../../../ado/guide/data/internet-publishing-scenario.md).  
  
 O provedor de publicação é instalado com o Microsoft Windows 2000. Versões anteriores do provedor de publicação de Internet também estão disponíveis com o Microsoft Office 2000 e o Microsoft Internet Explorer 5.0.  
  
 Há três maneiras de conectar o ADO para o provedor de publicação:  
  
-   Especifique "URL =" na cadeia de conexão. Por exemplo:  
  
    ```  
    objConn.Open "URL=http://servername"  
    ```  
  
-   Especifique Msdaipp.dso para o *provedor* palavra-chave da cadeia de caracteres de conexão. Por exemplo:  
  
    ```  
    objConn.Open "provider=MSDAIPP.DSO;data source=http://servername"  
    ```  
  
-   Especifique Msdaipp.dso para o [provedor](../../../ado/reference/ado-api/provider-property-ado.md) propriedade o [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto. Por exemplo:  
  
    ```  
    objConn.Provider = "MSDAIPP.DSO"  
    objConn.Open "http://servername"  
    ```  
  
> [!NOTE]
>  Se Msdaipp.dso for explicitamente especificado como o valor do provedor, com o *provedor* palavra-chave de cadeia de caracteres de conexão ou o **provedor** propriedade, você não pode usar "URL =" na cadeia de conexão. Se você fizer isso, ocorrerá um erro. Em vez disso, basta Especifica a URL como mostrado anteriormente.  
  
 Para obter informações mais específicas sobre o provedor de publicação, consulte [Microsoft OLE DB Provider para Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md), ou a documentação do provedor fornecida com o aplicativo de origem com a qual o provedor OLE DB para Publicação de Internet foi instalado: Windows 2000, o Office 2000 ou o Internet Explorer 5.0.

