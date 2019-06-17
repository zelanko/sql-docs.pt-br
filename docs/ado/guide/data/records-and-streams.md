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
manager: jroth
ms.openlocfilehash: 19fc6e61a10e1a92f0f674a23d00f1e1b06a596c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66701693"
---
# <a name="records-and-streams"></a>Registros e fluxos
Atualmente, o ADO fornece o [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto como o principal meio de acesso a informações em fontes de dados, como bancos de dados relacionais. No entanto, alguns provedores oferecem suporte a [registro](../../../ado/reference/ado-api/record-object-ado.md) e [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objetos como objetos alternativos ou complementares com a qual os dados de provedores podem ser manipulados. Para obter informações específicas sobre **registro** comportamento, consulte a documentação do provedor.  
  
## <a name="records"></a>Registros  
 **Registro** objetos essencialmente funcionar como uma linha **Recordset**s. No entanto, **registros** têm limitado em comparação comparada a funcionalidade **conjuntos de registros** e têm diferentes propriedades e métodos. O código-fonte para os dados em um **registro** objeto pode ser um comando que retorna uma linha de dados do provedor. Usando o **registro** objetos em vez de **conjunto de registros** objetos para receber os resultados de uma consulta que retorna uma linha de dados elimina a sobrecarga de instanciar mais complexo **conjunto de registros**  objeto.  
  
 **Registro** objetos podem atender outra finalidade, particularmente com provedores de fontes de dados diferentes bancos de dados relacionais tradicionais, como o [Microsoft OLE DB Provider para publicação na Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Muitas das informações que devem ser processadas existe, não como tabelas em bancos de dados, mas como mensagens em arquivos e sistemas de correio eletrônico em sistemas de arquivos modernos. O **registro** e **Stream** objetos facilitam o acesso a informações armazenadas em fontes diferentes de bancos de dados relacionais.  
  
 O **registro** objeto pode representar e gerenciar os dados, como arquivos e diretórios em um sistema de arquivos ou pastas e mensagens de um sistema de email. Para esses fins, a fonte para o **registro** pode ser a linha atual de um aberto **conjunto de registros**, uma URL absoluta ou uma URL relativa em conjunto com um aberto [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
 Normalmente, uma **Recordset** pode ser usado para representar um contêiner ou pai em uma hierarquia como uma pasta ou diretório. Um **registro** pode ser usado para retornar informações específicas sobre um nó no contêiner pai, como um arquivo ou documento. O principal motivo **registros** são usados para representar esse tipo de informação é que essas fontes de dados heterogêneos. Isso significa que cada **registro** pode ter um conjunto diferente e o número de campos. Tradicional **conjuntos de registros** contém linhas de um banco de dados são homogêneos, o que significa que cada linha tem o mesmo número e o tipo de campos.  
  
 Para obter mais informações sobre como usar o **registro** do objeto para o processamento de dados heterogêneos de provedores, como o provedor de publicação de Internet, consulte [usando o ADO para publicação na Internet](../../../ado/guide/data/using-ado-for-internet-publishing.md).  
  
## <a name="streams"></a>Fluxos  
 O **Stream** objeto fornece os meios para ler, escrever e gerenciar um fluxo de bytes. Esse fluxo de bytes pode ser texto ou binário e o tamanho é limitado apenas pelos recursos do sistema. Normalmente, o ADO **Stream** objetos são usados para as seguintes finalidades:  
  
-   Para conter os dados de um **Recordset** salvo no formato XML. Esses fluxos de XML de salvo **conjunto de registros**s pode ser usado como a origem, ao abrir uma nova **conjunto de registros**. Para obter mais informações, consulte [fluxos e persistência](../../../ado/guide/data/streams-and-persistence.md).  
  
-   Para conter [CommandStreams](../../../ado/reference/ado-api/commandstream-property-ado.md) para ser executada no provedor, como uma alternativa ao [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md). Por exemplo, diagramas de atualização XML pode ser usados como a origem para um comando com o Microsoft OLE DB Provider para SQL Server.  
  
-   Para receber os resultados do provedor em um formato diferente de um **Recordset**, como resultados XML do Microsoft OLE DB Provider para SQL Server. Para obter mais informações, consulte [recuperando conjuntos de resultados em fluxos](../../../ado/guide/data/retrieving-resultsets-into-streams.md).  
  
-   Para conter o texto ou bytes que compõem um arquivo ou uma mensagem, geralmente usados com provedores, como o provedor Microsoft OLE DB para publicação na Internet. Para obter mais informações sobre esse uso de **Stream** objetos, consulte [usando o ADO para publicação na Internet](../../../ado/guide/data/using-ado-for-internet-publishing.md).  
  
 Um **Stream** objeto pode ser aberto em:  
  
-   Um arquivo simples especificado com uma URL.  
  
-   Um campo de um **registro** ou **conjunto de registros** que contém um **Stream** objeto.  
  
-   O fluxo de padrão de um **registro** ou **Recordset** objeto que representa um diretório ou arquivo composto.  
  
-   Um campo de recurso que contém a URL de um arquivo simple.  
  
-   Nenhuma fonte específica em todas. Nesse caso, uma **Stream** objeto é aberto na memória. Dados podem ser gravados nele e, em seguida, salvos em outro **Stream** ou arquivo.  
  
-   Um campo BLOB em um **conjunto de registros**.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Fluxos e persistência](../../../ado/guide/data/streams-and-persistence.md)  
  
-   [Fluxos de comando](../../../ado/guide/data/command-streams.md)  
  
-   [Recuperando conjuntos de resultados em fluxos](../../../ado/guide/data/retrieving-resultsets-into-streams.md)  
  
-   [Usando o ADO para publicação na Internet](../../../ado/guide/data/using-ado-for-internet-publishing.md)
