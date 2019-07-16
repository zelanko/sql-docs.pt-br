---
title: Provedor Microsoft OLE DB para publicação na Internet | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB provider for Internet publishing [ADO]
- providers [ADO], OLE DB provider for Internet publishing
- Internet Publishing provider [ADO]
ms.assetid: 66a208d9-b580-4655-a41e-1d36e5b5bfca
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 19d719ddb4e5a2f7851a1d12dc4abe69069a354f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926759"
---
# <a name="microsoft-ole-db-provider-for-internet-publishing-overview"></a>Provedor Microsoft OLE DB para visão geral de publicação na Internet
O Microsoft OLE DB Provider para publicação na Internet permite que o ADO para acessar recursos atendidos pelo Microsoft FrontPage ou o Microsoft Internet Information Server. Os recursos incluem arquivos de origem da web, como arquivos HTML ou pastas do Windows 2000 da web.

## <a name="connection-string-parameters"></a>Parâmetros de cadeia de caracteres de Conexão
 Para se conectar ao provedor, defina as *provedor* argumento do [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propriedade para:

```vb
MSDAIPP.DSO
```

 Esse valor também pode ser definido ou lidos usando o [provedor](../../../ado/reference/ado-api/provider-property-ado.md) propriedade.

## <a name="typical-connection-string"></a>Cadeia de caracteres de Conexão típica
 Uma cadeia de caracteres de conexão típica para esse provedor é:

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
|**Provedor**|Especifica o provedor OLE DB para publicação na Internet.|
|**Fonte de dados** - ou - **URL**|Especifica a URL de um arquivo ou diretório publicado em uma pasta da Web.|
|**ID de usuário**|Especifica o nome de usuário.|
|**Senha**|Especifica a senha do usuário.|

> [!NOTE]
>  Se você estiver se conectando a um provedor de fonte de dados que dá suporte à autenticação do Windows, você deve especificar **Trusted_Connection = yes** ou **Integrated Security = SSPI** em vez de ID de usuário e senha informações na cadeia de conexão.

 Se você definir a *ResourceURL* valor da "URL =" na cadeia de conexão com um valor inválido, por padrão o provedor de Internet publicação gera uma caixa de diálogo para solicitar um valor válido. Isso é o comportamento indesejável para um componente na camada intermediária de um aplicativo, porque ele suspende a execução do programa até que a caixa de diálogo está desmarcada e o cliente é exibido para congelar porque não recebeu uma resposta do componente.

> [!NOTE]
>  Se MSDAIPP. DSO explicitamente é especificado como o valor do provedor, com o *provedor* palavra-chave de cadeia de caracteres de conexão ou o **provedor** propriedade, você não pode usar "URL =" na cadeia de conexão. Se você fizer isso, ocorrerá um erro. Em vez disso, basta especificar a URL conforme mostrado no tópico [usando o ADO com o provedor OLE DB para publicação na Internet](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md).

## <a name="see-also"></a>Consulte também
 [Cenário de publicação na Internet](../../../ado/guide/data/internet-publishing-scenario.md) [o provedor OLE DB para publicação na Internet](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)
