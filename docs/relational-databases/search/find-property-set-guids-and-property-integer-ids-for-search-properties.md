---
title: Localizar GUIDs do conjunto de propriedades e IDs de inteiro de propriedade para propriedades de pesquisa | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.component: search
ms.reviewer: ''
ms.suite: sql
ms.technology: search
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- search property lists [SQL Server], configuring
ms.assetid: 7db79165-8bcc-4be6-8d40-12d44deda79f
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 974155cff19984223d015c5ef38165ece3517c97
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38038454"
---
# <a name="find-property-set-guids-and-property-integer-ids-for-search-properties"></a>Localizar GUIDs do conjunto de propriedades e IDs de inteiro de propriedade para propriedades de pesquisa
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Este tópico discute como obter os valores que são necessários antes de adicionar uma propriedade a uma lista de propriedades de pesquisa, tornando-a pesquisável através de pesquisa de texto completo. Estes valores incluem o GUID do conjunto de propriedades e o identificador de inteiro de propriedade de uma propriedade de documento.  
  
 As propriedades de documentos que são extraídas por IFilters de dados binários – ou seja, de dados armazenados em uma coluna de tipo de dados **varbinary**, **varbinary(max)** (incluindo **FILESTREAM**) ou **image** – podem ser disponibilizadas para pesquisa de texto completo. Para tornar uma propriedade extraída pesquisável, adicione manualmente a propriedade a uma lista de propriedades de pesquisa. A lista de propriedades de pesquisa também deve ser associada a um ou mais índices de texto completo. Para obter mais informações, veja [Pesquisar propriedades de documento com listas de propriedades de pesquisa](../../relational-databases/search/search-document-properties-with-search-property-lists.md).  
  
 Antes de você poder acrescentar uma propriedade disponível a uma lista de propriedades, tem que localizar 2 pedaços de informações sobre a propriedade:  
  
-   O GUID do conjunto de propriedades da propriedade.  
  
-   A ID de inteiro da propriedade.  
  
 (Quando você adiciona uma propriedade a uma lista de propriedades, também precisa fornecer um nome e uma descrição. Entretanto, você não precisa usar o nome canônico e a descrição da propriedade.)  
  
 Este tópico descreve os métodos usados com frequência para localizar informações sobre propriedades disponíveis, especialmente sobre propriedades definidas pela Microsoft. Para obter informações sobre propriedades que foram definidas por terceiros, consulte a documentação de terceiros ou contate o fornecedor.  
  
##  <a name="wellknown"></a> Localizando informações sobre propriedades da Microsoft amplamente usadas e conhecidas  
 A Microsoft define centenas de propriedades de documento para uso em vários contextos, mas somente um pequeno subconjunto das propriedades disponíveis é usado por cada formato de arquivo. Dentre as propriedades frequentemente usadas do Windows está um conjunto pequeno de propriedades genéricas. Alguns exemplos de propriedades genéricas conhecidas são mostrados na tabela seguinte. A tabela mostra o nome conhecido, o nome canônico (da descrição de propriedade publicada pela Microsoft) no Windows, a GUID do conjunto de propriedades, o identificador de inteiro de propriedade e uma descrição sucinta.  
  
|Nome conhecido|Nome canônico no Windows.|GUID do conjunto de propriedades|ID de inteiro|Descrição|  
|----------------------|----------------------------|-----------------------|----------------|-----------------|  
|Autores|**System.Author**|F29F85E0-4FF9-1068-AB91-08002B27B3D9|4|Autor ou autores de um determinado item.|  
|Marcas|**System.Keywords**|F29F85E0-4FF9-1068-AB91-08002B27B3D9|5|Conjunto de palavras-chave (também conhecidas como marcas) atribuído ao item.|  
|Tipo|**System.PerceivedType**|28636AA6-953D-11D2-B5D6-00C04FD918D0|9|Tipo de arquivo percebido com base em seu tipo canônico.|  
|Title|**System.Title**|F29F85E0-4FF9-1068-AB91-08002B27B3D9|2|Título do item. Por exemplo, o título de um documento, o assunto de uma mensagem, a legenda de uma fotografia ou o nome de uma música.|  
  
 Para encorajar a consistência entre formatos de arquivos, a Microsoft identificou subconjuntos de propriedades de documento frequentemente usadas e de alta prioridade para várias categorias de documentos. Estas incluem comunicações, contatos, documentos, arquivos de música, imagens e vídeos. Para obter mais informações sobre as principais propriedades classificadas para cada categoria, veja [Propriedades definidas pelo sistema para formatos de arquivos personalizados](http://go.microsoft.com/fwlink/?LinkId=144336) na documentação do Windows Search.  
  
 Um formato de arquivo específico pode implementar propriedades de três tipos:  
  
-   Propriedades genéricas definidas pela [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
-   Propriedades específicas de categoria definidas pela [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
-   Propriedades personalizadas, específicas de aplicativo, definidas pelo fornecedor de software.  
  
##  <a name="filtdump"></a> Localizando Informações sobre propriedades disponíveis usando FILTDUMP.EXE  
 Para saber quais propriedades são descobertas e extraídas por um IFilter instalado, você pode instalar e executar o utilitário **filtdump.exe** , que faz parte do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows SDK.  
  
 Você executa o **filtdump.exe** no prompt de comando e fornece um único argumento. Este argumento é o nome de um arquivo individual que tem um tipo de arquivo para o qual um IFilter é instalado. O utilitário exibe uma lista de todas as propriedades descobertas pelo IFilter no documento, com seus GUIDs de conjunto de propriedades, IDs de inteiro e informações adicionais.  
  
 Para obter informações sobre como instalar esse software, consulte [Microsoft Windows SDK para Windows 7 e .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=212980). Depois de baixar e instalar o SDK, examine as pastas a seguir para localizar o utilitário filtdump.exe.  
  
-   Para a versão de 64 bits, procure em `C:\Program Files\Microsoft SDKs\Windows\v7.1\Bin\x64`.  
  
-   Para a versão de 32 bits, procure em `C:\Program Files\Microsoft SDKs\Windows\v7.1\Bin`.  
  
##  <a name="propdesc"></a> Localizando valores de propriedades de pesquisa a partir de uma descrição de propriedades do Windows  
 Para uma propriedade de pesquisa Windows conhecida, você pode obter as informações necessárias dos atributos **formatID** e **propID** da descrição de propriedade (**propertyDescription**).  
  
 O exemplo a seguir mostra a parte relevante de uma descrição de propriedade típica do Microsoft, neste caso, da propriedade `System.Author` . O atributo `formatID` especifica o GUID do conjunto de propriedades, `F29F85E0-4FF9-1068-AB91-08002B27B3D9`, e o atributo `propID` especifica a ID de inteiro de propriedade, `4.` Observe que o atributo `name` especifica o nome de propriedade canônico do Windows, `System.Author`. (Este exemplo omite partes da descrição de propriedade que não são pertinentes.)  
  
```  
.  
propertyDescription  
name = System.Author  
…  
formatID = F29F85E0-4FF9-1068-AB91-08002B27B3D9  
propID = 4  
…  
```  
  
 Para obter a descrição completa desta propriedade, consulte [System.Author](http://go.microsoft.com/fwlink/?LinkId=144337) na documentação do Windows Search.  
  
 Para obter uma lista completa de propriedades do Windows, consulte [Propriedades do Windows](http://go.microsoft.com/fwlink/?LinkId=215013), também na documentação do Windows Search.  
  
##  <a name="examples"></a> Adicionando uma propriedade a uma lista de propriedades de pesquisa  
 O exemplo a seguir mostra como adicionar uma propriedade a uma lista de propriedades de pesquisa. O exemplo usa uma instrução [ALTER SEARCH PROPERTY LIST](../../t-sql/statements/alter-search-property-list-transact-sql.md) para adicionar a propriedade `System.Author` a uma lista de propriedades de pesquisa denominada `PropertyList1`e fornece um nome de usuário amigável para a propriedade, `Author`.  
  
```  
ALTER SEARCH PROPERTY LIST PropertyList1   
  ADD 'Author'  
    WITH (  
          PROPERTY_SET_GUID = 'F29F85E0-4FF9-1068-AB91-08002B27B3D9',  
          PROPERTY_INT_ID = 4,   
          PROPERTY_DESCRIPTION = 'System.Author - the author or authors of the item'   
         )  
GO  
```  
  
 Para obter mais informações sobre como criar uma lista de propriedades de pesquisa e associá-la a um índice de texto completo, veja [Pesquisar propriedades de documento com listas de propriedades de pesquisa](../../relational-databases/search/search-document-properties-with-search-property-lists.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Pesquisar propriedades de documento com listas de propriedades de pesquisa](../../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [Configurar e gerenciar filtros de pesquisa](../../relational-databases/search/configure-and-manage-filters-for-search.md)  
  
  
