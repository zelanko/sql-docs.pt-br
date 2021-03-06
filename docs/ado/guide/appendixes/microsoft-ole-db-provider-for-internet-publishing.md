---
description: Visão geral do provedor do Microsoft OLE DB para publicação na Internet
title: Microsoft OLE DB Provider para publicação na Internet | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB provider for Internet publishing [ADO]
- providers [ADO], OLE DB provider for Internet publishing
- Internet Publishing provider [ADO]
ms.assetid: 66a208d9-b580-4655-a41e-1d36e5b5bfca
author: rothja
ms.author: jroth
ms.openlocfilehash: f924e1bec97ed399f4d6d3351c8d18b1d8dad5b1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991057"
---
# <a name="microsoft-ole-db-provider-for-internet-publishing-overview"></a>Visão geral do provedor do Microsoft OLE DB para publicação na Internet
O provedor de OLE DB da Microsoft para publicação na Internet permite que o ADO acesse recursos servidos pelo Microsoft FrontPage ou pelo Microsoft Internet Information Server. Os recursos incluem arquivos de origem da Web, como arquivos HTML, ou pastas da Web do Windows 2000.

## <a name="connection-string-parameters"></a>Parâmetros de cadeia de conexão
 Para se conectar a esse provedor, defina o argumento do *provedor* da propriedade [ConnectionString](../../reference/ado-api/connectionstring-property-ado.md) como:

```vb
MSDAIPP.DSO
```

 Esse valor também pode ser definido ou lido usando a propriedade [Provider](../../reference/ado-api/provider-property-ado.md) .

## <a name="typical-connection-string"></a>Cadeia de conexão típica
 Uma cadeia de conexão típica para esse provedor é:

```vb
"Provider=MSDAIPP.DSO;Data Source=ResourceURL;User ID=MyUserID;Password=MyPassword;"
```

 - ou -

```vb
"URL=ResourceURL;User ID=MyUserID;Password=MyPassword;"
```

 A cadeia de caracteres consiste nessas palavras-chave:

|Palavra-chave|Descrição|
|-------------|-----------------|
|**Provedor**|Especifica o provedor de OLE DB para publicação na Internet.|
|**Fonte de dados** -ou- **URL**|Especifica a URL de um arquivo ou diretório publicado em uma pasta da Web.|
|**ID de usuário**|Especifica um nome de usuário.|
|**Senha**|Especifica a senha do usuário.|

> [!NOTE]
>  Se você estiver se conectando a um provedor de fonte de dados que dá suporte à autenticação do Windows, especifique **Trusted_Connection = Sim** ou **segurança integrada = SSPI** , em vez de ID de usuário e informações de senha na cadeia de conexão.

 Se você definir o valor de *ResourceURL* de "URL =" na cadeia de conexão com um valor inválido, por padrão, o provedor de publicação na Internet gerará uma caixa de diálogo para solicitar um valor válido. Isso é um comportamento indesejável para um componente na camada intermediária de um aplicativo, pois ele suspende a execução do programa até que a caixa de diálogo seja desmarcada e o cliente pareça congelar, pois não recebeu uma resposta do componente.

> [!NOTE]
>  Se MSDAIPP. O DSO é explicitamente especificado como o valor do provedor, seja com a palavra-chave da cadeia de conexão do *provedor* ou com a propriedade do **provedor** , você não pode usar "URL =" na cadeia de conexão. Se você fizer isso, ocorrerá um erro. Em vez disso, basta especificar a URL, conforme mostrado no tópico [usando o ADO com o provedor de OLE DB para publicação na Internet](../data/the-ole-db-provider-for-internet-publishing.md).

## <a name="see-also"></a>Consulte Também
 [Cenário de publicação na Internet](../data/internet-publishing-scenario.md) [o provedor de OLE DB para publicação na Internet](../data/the-ole-db-provider-for-internet-publishing.md)