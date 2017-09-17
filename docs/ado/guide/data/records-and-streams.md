---
title: Registros e fluxos | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- streams [ADO]
- streams [ADO], about streams
- records [ADO]
ms.assetid: 4d68868e-2611-4b5c-9a89-7caa5f753151
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d11617fc364b3ce9f2c4f5b37623f4c74f968517
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="records-and-streams"></a>Registros e fluxos
ADO atualmente fornece o [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto como o principal meio de acesso a informações em fontes de dados, como bancos de dados relacionais. No entanto, alguns provedores oferecem suporte a [registro](../../../ado/reference/ado-api/record-object-ado.md) e [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) objetos como objetos alternativos ou complementares com a qual os dados de provedores podem ser manipulados. Para obter informações específicas sobre **registro** comportamento, consulte a documentação do provedor.  
  
## <a name="records"></a>Registros  
 **Registro** objetos essencialmente funcionar como uma linha **registros**s. No entanto, **registros** limitaram funcionalidade em comparação comparada **conjuntos de registros** e têm diferentes propriedades e métodos. A fonte de dados em um **registro** objeto pode ser um comando que retorna uma linha de dados do provedor. Usando **registro** objetos em vez de **registros** objetos para receber os resultados de uma consulta que retorna uma linha de dados elimina a sobrecarga de criar uma instância mais complexo **conjunto de registros ** objeto.  
  
 **Registro** objetos podem atender outro propósito, particularmente com provedores de fontes de dados diferentes bancos de dados relacionais tradicionais, como o [Microsoft OLE DB Provider para Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Muitas das informações que devem ser processadas existe, como tabelas em bancos de dados, mas como mensagens no email e sistemas de arquivos em sistemas de arquivos modernos. O **registro** e **fluxo** objetos facilitam o acesso a informações armazenadas nas fontes diferentes de bancos de dados relacionais.  
  
 O **registro** objeto pode representar e gerenciar os dados, como arquivos e diretórios em um sistema de arquivos ou pastas e mensagens de um sistema de email. Para esses fins, a fonte para o **registro** pode ser a linha atual de uma abertas **registros**, uma URL absoluta ou uma URL relativa em conjunto com um aberto [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
 Normalmente, um **registros** pode ser usado para representar um contêiner ou pai em uma hierarquia como uma pasta ou diretório. Um **registro** pode ser usado para retornar informações específicas sobre um nó no contêiner pai, como um arquivo ou documento. O principal motivo **registros** são usados para representar este tipo de informação é que essas fontes de dados heterogêneos. Isso significa que cada **registro** pode ter um conjunto diferente e o número de campos. Tradicional **conjuntos de registros** contendo linhas de um banco de dados são homogêneos, o que significa que cada linha tem o mesmo número e tipo de campos.  
  
 Para obter mais informações sobre como usar o **registro** de objeto para o processamento de dados heterogêneos de provedores, como o provedor de publicação, consulte [usando o ADO para Internet Publishing](../../../ado/guide/data/using-ado-for-internet-publishing.md).  
  
## <a name="streams"></a>Fluxos  
 O **fluxo** objeto fornece os meios para leitura, gravação e gerenciar um fluxo de bytes. Este fluxo de bytes pode ser texto ou binário e o tamanho é limitado apenas pelos recursos do sistema. Normalmente, o ADO **fluxo** objetos são usados para as seguintes finalidades:  
  
-   Para conter os dados de um **registros** salvos em formato XML. Esses fluxos de XML de salvo **Recordset**s pode ser usado como a origem, ao abrir um novo **registros**. Para obter mais informações, consulte [fluxos e persistência](../../../ado/guide/data/streams-and-persistence.md).  
  
-   Para conter [CommandStreams](../../../ado/reference/ado-api/commandstream-property-ado.md) a ser executada em relação ao provedor, como uma alternativa para [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md). Por exemplo, diagramas de atualização XML pode ser usados como a origem para um comando com o Microsoft OLE DB Provider para SQL Server.  
  
-   Para receber os resultados do provedor em um formato diferente de um **registros**, como os resultados XML do Microsoft OLE DB Provider para SQL Server. Para obter mais informações, consulte [recuperar conjuntos de resultados em fluxos](../../../ado/guide/data/retrieving-resultsets-into-streams.md).  
  
-   Para conter o texto ou bytes que constituem um arquivo ou uma mensagem, geralmente usados com provedores, como o Microsoft OLE DB Provider para publicação de Internet. Para obter mais informações sobre esse uso do **fluxo** objetos, consulte [usando o ADO para Internet Publishing](../../../ado/guide/data/using-ado-for-internet-publishing.md).  
  
 Um **fluxo** objeto pode ser aberto em:  
  
-   Um arquivo simple especificado com uma URL.  
  
-   Um campo de um **registro** ou **registros** que contém um **fluxo** objeto.  
  
-   O fluxo de padrão de um **registro** ou **registros** objeto que representa um diretório ou arquivo composto.  
  
-   Um campo de recurso que contém a URL de um arquivo simple.  
  
-   Nenhuma fonte específica em todos os. Nesse caso, um **fluxo** objeto é aberto na memória. Dados podem ser gravados nele e, em seguida, salvos em outro **fluxo** ou arquivo.  
  
-   Um campo BLOB em um **registros**.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Fluxos e persistência](../../../ado/guide/data/streams-and-persistence.md)  
  
-   [Fluxos de comando](../../../ado/guide/data/command-streams.md)  
  
-   [Recuperando conjuntos de resultados em fluxos](../../../ado/guide/data/retrieving-resultsets-into-streams.md)  
  
-   [Usando o ADO para publicação na Internet](../../../ado/guide/data/using-ado-for-internet-publishing.md)
