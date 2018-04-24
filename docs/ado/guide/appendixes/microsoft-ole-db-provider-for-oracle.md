---
title: Provedor Microsoft OLE DB para Oracle | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], OLE DB provider for Oracle
- OLE DB provider for Oracle [ADO]
- Oracle provider [ADO]
ms.assetid: 44fae9dd-5585-4cd6-8bbd-3248a78931b4
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 71ce9defd8d06a220da3c3f74c439d8a4a7ecc84
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="microsoft-ole-db-provider-for-oracle-overview"></a>Provedor Microsoft OLE DB para visão geral do Oracle
> [!IMPORTANT]
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o provedor do OLE DB do Oracle.

 O Microsoft OLE DB Provider for Oracle permite que o ADO acessar bancos de dados Oracle.

## <a name="connection-string-parameters"></a>Parâmetros de cadeia de caracteres de Conexão
 Para se conectar ao provedor, defina o *provedor* argumento o [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propriedade para:

```
MSDAORA
```

 Lendo o [provedor](../../../ado/reference/ado-api/provider-property-ado.md) propriedade retornará essa cadeia de caracteres.

 Se uma consulta de junção com um cursor keyset ou dynamic é executada em um banco de dados Oracle, ocorrerá um erro. Oracle só oferece suporte a um cursor estático somente leitura.

## <a name="typical-connection-string"></a>Cadeia de caracteres de Conexão típica
 Uma cadeia de conexão típica para esse provedor é:

```
"Provider=MSDAORA;Data Source=serverName;User ID=MyUserID; Password=MyPassword;"
```

 A cadeia de caracteres consiste nessas palavras-chave:

|Palavra-chave|Description|
|-------------|-----------------|
|**Provedor**|Especifica o provedor OLE DB para Oracle.|
|**Fonte de dados**|Especifica o nome de um servidor.|
|**ID de usuário**|Especifica o nome de usuário.|
|**Senha**|Especifica a senha do usuário.|

> [!NOTE]
>  Se você estiver se conectando a um provedor de fonte de dados que oferece suporte à autenticação do Windows, você deve especificar **Trusted_Connection = yes** ou **segurança integrada = SSPI** em vez de ID de usuário e senha informações na cadeia de conexão.

## <a name="provider-specific-connection-parameters"></a>Parâmetros de Conexão específicos do provedor
 O provedor oferece suporte a vários parâmetros de conexão específica do provedor, além daqueles definidos pelo ADO. Como com as propriedades de conexão ADO, essas propriedades específicas do provedor podem ser definidas por meio de [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção de um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) ou como parte do **ConnectionString**.

 Esses parâmetros são totalmente descritos o [referência do programador de DB OLE](http://msdn.microsoft.com/en-us/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8). O [índice de propriedade dinâmica de ADO](../../../ado/reference/ado-api/ado-dynamic-property-index.md) fornece uma referência cruzada entre esses nomes de parâmetros e as propriedades de OLE DB correspondentes.

|Parâmetro|Description|
|---------------|-----------------|
|**Identificador de janela**|Indica o identificador de janela a ser usado para solicitar informações adicionais.|
|**Identificador de Localidade**|Indica um número de 32 bits exclusivo (por exemplo, 1033) que especifica as preferências de idioma do usuário. Essas preferências indicam como datas e horas são formatadas, os itens são classificados em ordem alfabética, cadeias de caracteres são comparadas e assim por diante.|
|**Serviços do OLE DB**|Indica um bitmask que especifica os serviços de OLE DB para habilitar ou desabilitar.|
|**prompt**|Indica se o usuário enquanto está sendo estabelecida uma conexão.|
|**Propriedades estendidas**|Uma cadeia de caracteres que contém informações de conexão específicas do provedor, estendido. Use essa propriedade somente para informações de conexão específicas do provedor que não podem ser descritas por meio do mecanismo de propriedade.|

## <a name="see-also"></a>Consulte também
 [Propriedade ConnectionString (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [propriedade do provedor (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) [o objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
