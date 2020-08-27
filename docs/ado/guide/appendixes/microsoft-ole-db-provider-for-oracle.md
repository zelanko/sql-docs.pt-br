---
description: Visão geral de Provedor Microsoft OLE DB para Oracle
title: Provedor Microsoft OLE DB para Oracle | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], OLE DB provider for Oracle
- OLE DB provider for Oracle [ADO]
- Oracle provider [ADO]
ms.assetid: 44fae9dd-5585-4cd6-8bbd-3248a78931b4
author: rothja
ms.author: jroth
ms.openlocfilehash: d8da5e3d5de1ac0ee3f3dfa1b0f989679af3cd1d
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991007"
---
# <a name="microsoft-ole-db-provider-for-oracle-overview"></a>Visão geral de Provedor Microsoft OLE DB para Oracle
> [!IMPORTANT]
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o provedor de OLE DB da Oracle.

 O Provedor Microsoft OLE DB para Oracle permite que o ADO acesse bancos de dados Oracle.

## <a name="connection-string-parameters"></a>Parâmetros de cadeia de conexão
 Para se conectar a esse provedor, defina o argumento do *provedor* da propriedade [ConnectionString](../../reference/ado-api/connectionstring-property-ado.md) como:

```vb
MSDAORA
```

 A leitura da propriedade [Provider](../../reference/ado-api/provider-property-ado.md) retornará essa cadeia de caracteres também.

 Se uma consulta de junção com um conjunto de chaves ou cursor dinâmico for executada em um banco de dados Oracle, ocorrerá um erro. O Oracle só dá suporte a um cursor somente leitura estático.

## <a name="typical-connection-string"></a>Cadeia de conexão típica
 Uma cadeia de conexão típica para esse provedor é:

```vb
"Provider=MSDAORA;Data Source=serverName;User ID=MyUserID; Password=MyPassword;"
```

 A cadeia de caracteres consiste nessas palavras-chave:

|Palavra-chave|Descrição|
|-------------|-----------------|
|**Provedor**|Especifica o provedor de OLE DB para Oracle.|
|**Fonte de Dados**|Especifica o nome de um servidor.|
|**ID de usuário**|Especifica um nome de usuário.|
|**Senha**|Especifica a senha do usuário.|

> [!NOTE]
>  Se você estiver se conectando a um provedor de fonte de dados que dá suporte à autenticação do Windows, especifique **Trusted_Connection = Sim** ou **segurança integrada = SSPI** , em vez de ID de usuário e informações de senha na cadeia de conexão.

## <a name="provider-specific-connection-parameters"></a>Parâmetros de conexão específicos do provedor
 O provedor dá suporte a vários parâmetros de conexão específicos do provedor, além daqueles definidos pelo ADO. Assim como acontece com as propriedades de conexão ADO, essas propriedades específicas do provedor podem ser definidas por meio da coleção [Properties](../../reference/ado-api/properties-collection-ado.md) de uma [conexão](../../reference/ado-api/connection-object-ado.md) ou como parte de **ConnectionString**.

 Esses parâmetros são totalmente descritos na [referência do programador de OLE DB](/previous-versions/windows/desktop/ms713643(v=vs.85)). O [índice de propriedades dinâmicas do ADO](../../reference/ado-api/ado-dynamic-property-index.md) fornece uma referência cruzada entre esses nomes de parâmetro e as propriedades de OLE DB correspondentes.

|Parâmetro|Descrição|
|---------------|-----------------|
|**Identificador da Janela**|Indica o identificador de janela a ser usado para solicitar informações adicionais.|
|**Identificador de Localidade**|Indica um número de bits de 32 exclusivo (por exemplo, 1033) que especifica as preferências relacionadas ao idioma do usuário. Essas preferências indicam como as datas e horas são formatadas, os itens são classificados alfabeticamente, as cadeias de caracteres são comparadas e assim por diante.|
|**Serviços OLE DBs**|Indica um bitmask que especifica OLE DB serviços a serem habilitados ou desabilitados.|
|**Prompt**|Indica se o usuário deve ser avisado enquanto uma conexão está sendo estabelecida.|
|**Propriedades estendidas**|Uma cadeia de caracteres que contém informações de conexão estendidas específicas do provedor. Use essa propriedade somente para informações de conexão específicas do provedor que não podem ser descritas por meio do mecanismo de propriedade.|

## <a name="see-also"></a>Consulte Também
 Propriedade [ConnectionString (](../../reference/ado-api/connectionstring-property-ado.md) ADO) provedor de conjunto de [Propriedades](../../reference/ado-api/provider-property-ado.md) (ADO) [Recordset (](../../reference/ado-api/recordset-object-ado.md) ADO)