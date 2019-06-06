---
title: Microsoft OLE DB Provider for Oracle | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], OLE DB provider for Oracle
- OLE DB provider for Oracle [ADO]
- Oracle provider [ADO]
ms.assetid: 44fae9dd-5585-4cd6-8bbd-3248a78931b4
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6af8fcd665fdfe503eab5aec591419982d0d3958
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702719"
---
# <a name="microsoft-ole-db-provider-for-oracle-overview"></a>Provedor Microsoft OLE DB para visão geral do Oracle
> [!IMPORTANT]
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o provedor do OLE DB do Oracle.

 O Microsoft OLE DB Provider for Oracle permite que o ADO para acessar bancos de dados Oracle.

## <a name="connection-string-parameters"></a>Parâmetros de cadeia de caracteres de Conexão
 Para se conectar ao provedor, defina as *provedor* argumento do [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propriedade para:

```vb
MSDAORA
```

 Lendo a [provedor](../../../ado/reference/ado-api/provider-property-ado.md) propriedade retornará essa cadeia de caracteres.

 Se uma consulta de junção com um cursor keyset ou dynamic é executada em um banco de dados Oracle, ocorrerá um erro. Oracle dá suporte apenas um cursor de somente leitura estático.

## <a name="typical-connection-string"></a>Cadeia de caracteres de Conexão típica
 Uma cadeia de caracteres de conexão típica para esse provedor é:

```vb
"Provider=MSDAORA;Data Source=serverName;User ID=MyUserID; Password=MyPassword;"
```

 A cadeia de caracteres consiste nessas palavras-chave:

|Palavra-chave|Descrição|
|-------------|-----------------|
|**Provedor**|Especifica o provedor OLE DB para Oracle.|
|**Fonte de dados**|Especifica o nome de um servidor.|
|**ID de usuário**|Especifica o nome de usuário.|
|**Senha**|Especifica a senha do usuário.|

> [!NOTE]
>  Se você estiver se conectando a um provedor de fonte de dados que dá suporte à autenticação do Windows, você deve especificar **Trusted_Connection = yes** ou **Integrated Security = SSPI** em vez de ID de usuário e senha informações na cadeia de conexão.

## <a name="provider-specific-connection-parameters"></a>Parâmetros de Conexão específicas do provedor
 O provedor oferece suporte a vários parâmetros de conexão específica do provedor além daqueles definidos pelo ADO. Como com as propriedades de conexão ADO, essas propriedades específicas do provedor podem ser definidas por meio de [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção de uma [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) ou como parte do **ConnectionString**.

 Esses parâmetros são totalmente descritos na [referência do programador DB OLE](https://msdn.microsoft.com/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8). O [índice de propriedade dinâmica do ADO](../../../ado/reference/ado-api/ado-dynamic-property-index.md) fornece uma referência cruzada entre esses nomes de parâmetro e as propriedades de OLE DB correspondentes.

|Parâmetro|Descrição|
|---------------|-----------------|
|**Identificador de janela**|Indica o identificador de janela a ser usado para solicitar informações adicionais.|
|**Identificador de Localidade**|Indica um número de 32 bits exclusivo (por exemplo, 1033) que especifica as preferências de idioma do usuário. Essas preferências indicam como datas e horas são formatadas, os itens são classificados em ordem alfabética, cadeias de caracteres são comparadas e assim por diante.|
|**Serviços do OLE DB**|Indica um bitmask que especifica os serviços do OLE DB para habilitar ou desabilitar.|
|**Solicitar**|Indica se deve solicitar ao usuário enquanto está sendo estabelecida uma conexão.|
|**Propriedades estendidas**|Uma cadeia de caracteres que contém informações de conexão específicas do provedor, estendida. Use essa propriedade apenas para informações de conexão específicas do provedor que não podem ser descritas por meio do mecanismo de propriedade.|

## <a name="see-also"></a>Consulte também
 [Propriedade ConnectionString (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [propriedade Provider (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) [objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
