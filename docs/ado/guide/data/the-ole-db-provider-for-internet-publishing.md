---
title: O provedor OLE DB para publicação na Internet | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB provider for Internet publishing [ADO]
- ADO, Internet publishing
- publishing to Internet [ADO]
- Internet publishing [ADO]
- providers [ADO], OLE DB provider for Internet publishing
ms.assetid: 4869aafa-7401-4ce1-93ce-45406a60274f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f70970ec872d3c921fa10e3eacb1c54d7c4de2d4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47632204"
---
# <a name="the-ole-db-provider-for-internet-publishing"></a>O Provedor OLE DB para publicação na Internet
O ADO [registro](../../../ado/reference/ado-api/record-object-ado.md) e [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objetos podem ser usados com o provedor Microsoft OLE DB para publicação na Internet (provedor de publicação da Internet) para acessar e manipular os recursos, como arquivos ou pastas da Web atendido pelo Microsoft FrontPage. Com o ADO, você pode especificar a origem de um **registro**, **Stream**, ou [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) ser uma URL. Você pode, em seguida, carregar, baixar, mover, copiar e excluir recursos ou manipular diretamente as propriedades do recurso.  
  
 Por exemplo de código que usa **registros** e **fluxos** com o provedor de publicação de Internet, consulte a [cenário de publicação de Internet](../../../ado/guide/data/internet-publishing-scenario.md).  
  
 O provedor de publicação de Internet é instalado com o Microsoft Windows 2000. Versões anteriores do provedor de publicação de Internet também estão disponíveis com o Microsoft Office 2000 e o Microsoft Internet Explorer 5.0.  
  
 Há três maneiras de conexão ADO com o provedor de publicação de Internet:  
  
-   Especifique "URL =" na cadeia de conexão. Por exemplo:  
  
    ```  
    objConn.Open "URL=http://servername"  
    ```  
  
-   Especifique Msdaipp.dso para o *provedor* palavra-chave da cadeia de caracteres de conexão. Por exemplo:  
  
    ```  
    objConn.Open "provider=MSDAIPP.DSO;data source=http://servername"  
    ```  
  
-   Especifique Msdaipp.dso para o [provedor](../../../ado/reference/ado-api/provider-property-ado.md) propriedade da [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto. Por exemplo:  
  
    ```  
    objConn.Provider = "MSDAIPP.DSO"  
    objConn.Open "http://servername"  
    ```  
  
> [!NOTE]
>  Se Msdaipp.dso for especificado explicitamente como o valor do provedor, com o *provedor* palavra-chave de cadeia de caracteres de conexão ou o **provedor** propriedade, você não pode usar "URL =" na cadeia de conexão. Se você fizer isso, ocorrerá um erro. Em vez disso, basta Especifica a URL conforme mostrado anteriormente.  
  
 Para obter informações mais específicas sobre o provedor de publicação de Internet, consulte [Microsoft OLE DB Provider para publicação na Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md), ou a documentação do provedor fornecido com o aplicativo de origem com o qual o provedor OLE DB para Publicação na Internet foi instalado: Windows 2000, o Office 2000 ou o Internet Explorer 5.0.
