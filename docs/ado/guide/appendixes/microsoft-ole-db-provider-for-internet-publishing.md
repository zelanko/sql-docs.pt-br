---
title: Provedor Microsoft OLE DB para publicação na Internet | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB provider for Internet publishing [ADO]
- providers [ADO], OLE DB provider for Internet publishing
- Internet Publishing provider [ADO]
ms.assetid: 66a208d9-b580-4655-a41e-1d36e5b5bfca
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c8d3caac3bd857b790372bd6b41fc818090210a0
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35271215"
---
# <a name="microsoft-ole-db-provider-for-internet-publishing-overview"></a>Provedor Microsoft OLE DB para visão geral de publicação na Internet
O Microsoft OLE DB Provider para publicação de Internet permite que o ADO para acessar os recursos atendidos pelo Microsoft FrontPage ou o Microsoft Internet Information Server. Os recursos incluem arquivos de origem da web, como arquivos HTML ou pastas da web do Windows 2000.

## <a name="connection-string-parameters"></a>Parâmetros de cadeia de caracteres de Conexão
 Para se conectar ao provedor, defina o *provedor* argumento o [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propriedade para:

```
MSDAIPP.DSO
```

 Esse valor também pode ser definido ou lidos usando o [provedor](../../../ado/reference/ado-api/provider-property-ado.md) propriedade.

## <a name="typical-connection-string"></a>Cadeia de caracteres de Conexão típica
 Uma cadeia de conexão típica para esse provedor é:

```
"Provider=MSDAIPP.DSO;Data Source=ResourceURL;User ID=MyUserID;Password=MyPassword;"
```

 -ou-

```
"URL=ResourceURL;User ID=MyUserID;Password=MyPassword;"
```

 A cadeia de caracteres consiste nessas palavras-chave:

|Palavra-chave|Description|
|-------------|-----------------|
|**Provedor**|Especifica o provedor OLE DB para publicação na Internet.|
|**Fonte de dados** - ou - **URL**|Especifica a URL de um arquivo ou diretório publicada em uma pasta da Web.|
|**ID de usuário**|Especifica o nome de usuário.|
|**Senha**|Especifica a senha do usuário.|

> [!NOTE]
>  Se você estiver se conectando a um provedor de fonte de dados que oferece suporte à autenticação do Windows, você deve especificar **Trusted_Connection = yes** ou **segurança integrada = SSPI** em vez de ID de usuário e senha informações na cadeia de conexão.

 Se você definir o *ResourceURL* valor o "URL =" na cadeia de conexão para um valor inválido, por padrão o provedor de publicação gera uma caixa de diálogo para solicitar um valor válido. Esse é o comportamento de indesejável para um componente na camada intermediária de um aplicativo, como ele suspende a execução do programa, até que a caixa de diálogo está desmarcada e o cliente é exibido para congelar porque não recebeu uma resposta do componente.

> [!NOTE]
>  Se MSDAIPP. DSO sejam especificado explicitamente como o valor do provedor, com o *provedor* palavra-chave de cadeia de caracteres de conexão ou o **provedor** propriedade, você não pode usar "URL =" na cadeia de conexão. Se você fizer isso, ocorrerá um erro. Em vez disso, basta especificar a URL como mostrado no tópico [usando o ADO com o provedor OLE DB para Internet Publishing](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md).

## <a name="see-also"></a>Consulte também
 [Cenário de publicação na Internet](../../../ado/guide/data/internet-publishing-scenario.md) [o provedor OLE DB para publicação na Internet](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)
