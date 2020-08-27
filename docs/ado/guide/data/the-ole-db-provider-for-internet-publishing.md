---
description: O Provedor OLE DB para publicação na Internet
title: O provedor de OLE DB para publicação na Internet | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 7556d3857142a4762fd411f5175a38c2e4d58cf3
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979357"
---
# <a name="the-ole-db-provider-for-internet-publishing"></a>O Provedor OLE DB para publicação na Internet
O [registro](../../../ado/reference/ado-api/record-object-ado.md) ADO e os objetos [Stream](../../../ado/reference/ado-api/stream-object-ado.md) podem ser usados com o provedor de OLE DB da Microsoft para publicação na Internet (provedor de publicação da Internet) para acessar e manipular recursos, como pastas da Web ou arquivos servidos pelo Microsoft FrontPage. Com o ADO, você pode especificar a origem de um **registro**, **fluxo**ou [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) para ser uma URL. Em seguida, você pode carregar, baixar, mover, copiar e excluir recursos ou manipular diretamente as propriedades do recurso.  
  
 Por exemplo, o código que usa **registros** e **fluxos** com o provedor de publicação na Internet, consulte o [cenário de publicação na Internet](../../../ado/guide/data/internet-publishing-scenario.md).  
  
 O provedor de publicação da Internet é instalado com o Microsoft Windows 2000. As versões anteriores do provedor de publicação na Internet também estão disponíveis com o Microsoft Office 2000 e o Microsoft Internet Explorer 5,0.  
  
 Há três maneiras de conectar o ADO ao provedor de publicação da Internet:  
  
-   Especifique "URL =" na cadeia de conexão. Por exemplo:  
  
    ```  
    objConn.Open "URL=https://servername"  
    ```  
  
-   Especifique MSDAIPP. DSO para a palavra-chave *Provider* da cadeia de conexão. Por exemplo:  
  
    ```  
    objConn.Open "provider=MSDAIPP.DSO;data source=https://servername"  
    ```  
  
-   Especifique MSDAIPP. DSO para a propriedade [Provider](../../../ado/reference/ado-api/provider-property-ado.md) do objeto [Connection](../../../ado/reference/ado-api/connection-object-ado.md) . Por exemplo:  
  
    ```  
    objConn.Provider = "MSDAIPP.DSO"  
    objConn.Open "https://servername"  
    ```  
  
> [!NOTE]
>  Se MSDAIPP. DSO for explicitamente especificado como o valor do provedor, seja com a palavra-chave da cadeia de conexão do *provedor* ou com a propriedade do **provedor** , você não poderá usar "URL =" na cadeia de conexão. Se você fizer isso, ocorrerá um erro. Em vez disso, basta especificar a URL, conforme mostrado anteriormente.  
  
 Para obter informações mais específicas sobre o provedor de publicação na Internet, consulte [provedor de OLE DB da Microsoft para publicação na Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)ou a documentação do provedor fornecida com o aplicativo de origem com o qual o provedor de OLE DB para publicação na Internet foi instalado: Windows 2000, Office 2000 ou Internet Explorer 5,0.
