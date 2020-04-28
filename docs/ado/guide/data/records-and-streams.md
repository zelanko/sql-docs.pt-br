---
title: Registros e fluxos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- streams [ADO]
- streams [ADO], about streams
- records [ADO]
ms.assetid: 4d68868e-2611-4b5c-9a89-7caa5f753151
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4636df1451ba946b9a7bfb62e3d6775c35b1d6f3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67924495"
---
# <a name="records-and-streams"></a>Registros e fluxos
Atualmente, o ADO fornece o objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) como o principal meio de acesso às informações em fontes de dados, como bancos de dado relacionais. No entanto, alguns provedores dão suporte aos objetos [Record](../../../ado/reference/ado-api/record-object-ado.md) e [Stream](../../../ado/reference/ado-api/stream-object-ado.md) como objetos alternativos ou complementares com os quais os dados dos provedores podem ser manipulados. Para obter informações específicas sobre o comportamento do **registro** , consulte a documentação do provedor.  
  
## <a name="records"></a>Registros  
 Os objetos de **registro** essencialmente funcionam como s de **conjunto de registros**de uma linha. No entanto, os **registros** têm funcionalidade limitada em comparação com **conjuntos de registros** e têm propriedades e métodos diferentes. A origem dos dados em um objeto de **registro** pode ser um comando que retorna uma linha de dados do provedor. O uso de objetos de **registro** em vez de objetos **Recordset** para receber os resultados de uma consulta que retorna uma linha de dados elimina a sobrecarga de instanciar o objeto **Recordset** mais complexo.  
  
 Os objetos de **registro** podem atender a outra finalidade, especialmente com provedores de fontes de dados que não sejam bancos de dado relacionais tradicionais, como o [provedor de OLE DB da Microsoft para publicação na Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Grande parte das informações que devem ser processadas existe, não como tabelas em bancos de dados, mas como mensagens em sistemas de email e arquivos em sistemas de arquivos modernos. Os objetos **Record** e **Stream** facilitam o acesso a informações armazenadas em fontes diferentes de bancos de dados relacionais.  
  
 O objeto **Record** pode representar e gerenciar dados como diretórios e arquivos em um sistema de arquivos, pastas e mensagens em um sistema de email. Para essas finalidades, a origem do **registro** pode ser a linha atual de um **conjunto de registros**aberto, uma URL absoluta ou uma URL relativa em conjunto com um objeto de [conexão](../../../ado/reference/ado-api/connection-object-ado.md) aberta.  
  
 Normalmente, um **conjunto de registros** pode ser usado para representar um contêiner ou pai em uma hierarquia, como uma pasta ou um diretório. Um **registro** pode ser usado para retornar informações específicas sobre um nó no contêiner pai, como um arquivo ou documento. Os **registros** principais de motivo são usados para representar esse tipo de informação é que essas fontes de dados são heterogêneas. Isso significa que cada **registro** pode ter um conjunto e número de campos diferentes. Os **conjuntos de registros** tradicionais que contêm linhas de um banco de dados são homogêneos, o que significa que cada linha tem o mesmo número e tipo de campos.  
  
 Para obter mais informações sobre como usar o objeto **Record** para processar esses dados heterogêneos de provedores como o provedor de publicação da Internet, consulte [usando o ADO para publicação na Internet](../../../ado/guide/data/using-ado-for-internet-publishing.md).  
  
## <a name="streams"></a>Fluxos  
 O objeto **Stream** fornece os meios para ler, gravar e gerenciar um fluxo de bytes. Esse fluxo de bytes pode ser texto ou binário e é limitado em tamanho apenas pelos recursos do sistema. Normalmente, os objetos de **fluxo** do ADO são usados para as seguintes finalidades:  
  
-   Para conter os dados de um **conjunto de registros** salvo em formato XML. Esses fluxos XML do **conjunto de registros**s salvo podem ser usados como a origem ao abrir um novo **conjunto de registros**. Para obter mais informações, consulte [fluxos e persistência](../../../ado/guide/data/streams-and-persistence.md).  
  
-   Para conter [CommandStreams](../../../ado/reference/ado-api/commandstream-property-ado.md) a ser executado no provedor como uma alternativa para [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md). Por exemplo, os Updategrams XML podem ser usados como a origem de um comando no provedor de OLE DB da Microsoft para SQL Server.  
  
-   Para receber resultados do provedor em um formato diferente de um **conjunto de registros**, como resultados XML do provedor de OLE DB da Microsoft para SQL Server. Para obter mais informações, consulte [recuperando conjuntos de resultados em fluxos](../../../ado/guide/data/retrieving-resultsets-into-streams.md).  
  
-   Para conter o texto ou os bytes que compõem um arquivo ou uma mensagem, normalmente usados com provedores como o provedor de OLE DB da Microsoft para publicação na Internet. Para obter mais informações sobre esse uso de objetos **Stream** , consulte [usando o ADO para publicação na Internet](../../../ado/guide/data/using-ado-for-internet-publishing.md).  
  
 Um objeto de **fluxo** pode ser aberto em:  
  
-   Um arquivo simples especificado com uma URL.  
  
-   Um campo de um **registro** ou **conjunto de registros** que contém um objeto de **fluxo** .  
  
-   O fluxo padrão de um **registro** ou objeto de **conjunto de registros** que representa um diretório ou arquivo composto.  
  
-   Um campo de recurso que contém a URL de um arquivo simples.  
  
-   Nenhuma fonte específica. Nesse caso, um objeto de **fluxo** é aberto na memória. Os dados podem ser gravados nele e salvos em outro **fluxo** ou arquivo.  
  
-   Um campo de BLOB em um **conjunto de registros**.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Fluxos e persistência](../../../ado/guide/data/streams-and-persistence.md)  
  
-   [Fluxos de comando](../../../ado/guide/data/command-streams.md)  
  
-   [Recuperar conjuntos de resultados em fluxos](../../../ado/guide/data/retrieving-resultsets-into-streams.md)  
  
-   [Usar o ADO para publicação na Internet](../../../ado/guide/data/using-ado-for-internet-publishing.md)
