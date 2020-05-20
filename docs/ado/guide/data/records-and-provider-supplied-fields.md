---
title: Registros e campos fornecidos pelo provedor | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- records-provided fields [ADO]
- provider-supplied fields [ADO]
ms.assetid: 77f95e0a-0cf2-411a-a792-593f77330fbd
author: rothja
ms.author: jroth
ms.openlocfilehash: abfa226c5bc6c94613a5d45c48a351811235455f
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764787"
---
# <a name="records-and-provider-supplied-fields"></a>Registros e campos fornecidos pelo provedor
Quando um objeto de [registro](../../../ado/reference/ado-api/record-object-ado.md) é aberto, sua origem pode ser a linha atual de um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md)aberto, uma URL absoluta ou uma URL relativa em conjunto com um objeto de [conexão](../../../ado/reference/ado-api/connection-object-ado.md) aberta.  
  
 Se o **registro** for aberto de um **conjunto de registros**, a coleção de [campos](../../../ado/reference/ado-api/fields-collection-ado.md) de objeto de **registro** conterá todos os campos do **conjunto de registros**, além de todos os campos adicionados pelo provedor subjacente.  
  
 O provedor pode inserir campos adicionais que servem como características complementares do **registro**. Como resultado, um **registro** pode ter campos exclusivos que não estejam no **conjunto de registros** como um todo ou qualquer **registro** derivado de outra linha do **conjunto de registros**.  
  
 Por exemplo, todas as linhas de um **conjunto de registros** derivado de uma fonte de dados de email podem ter colunas como from, to e Subject. Um **registro** derivado desse **conjunto de registros** terá os mesmos campos. No entanto, o **registro** também pode ter outros campos exclusivos para a mensagem específica representada por esse **registro**, como anexo e CC (cópia carbono).  
  
 Embora o objeto de **registro** e a linha atual do **conjunto de registros** tenham os mesmos campos, eles são diferentes porque os objetos **Record** e **Recordset** têm métodos e propriedades diferentes.  
  
 Um campo mantido em comum pelo **registro** e **conjunto de registros** pode ser modificado em qualquer objeto. No entanto, o campo não pode ser excluído no objeto **Record** , embora o provedor subjacente possa dar suporte à definição do campo como NULL.  
  
 Depois que o **registro** for aberto, você poderá adicionar campos programaticamente. Você também pode excluir campos que você adicionou, mas não pode excluir campos do **conjunto de registros**original.  
  
 Você também pode abrir o objeto **Record** diretamente de uma URL. Nesse caso, os campos adicionados ao **registro** dependem do provedor subjacente. Atualmente, a maioria dos provedores adiciona um conjunto de campos que descrevem a entidade representada pelo **registro**. Se a entidade consistir em um fluxo de bytes, como um arquivo simples, um objeto de [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) geralmente poderá ser aberto a partir do **registro**.  
  
## <a name="special-fields-for-document-source-providers"></a>Campos especiais para provedores de origem de documentos  
 Uma classe especial de provedores, chamada de *provedores de origem de documentos*, gerencia pastas e documentos. Quando um objeto de **registro** representa um documento ou um objeto **Recordset** representa uma pasta de documentos, o provedor de origem do documento popula esses objetos com um conjunto exclusivo de campos que descrevem as características do documento em vez do próprio documento real. Normalmente, um campo contém uma referência ao **fluxo** que representa o documento.  
  
 Esses campos constituem um **registro** de recurso ou **conjunto de registros** e são listados para os provedores específicos que dão suporte A eles no [Apêndice a: provedores](../../../ado/guide/appendixes/appendix-a-providers.md).  
  
 Duas constantes indexam a coleção **Fields** de um **registro** de recurso ou **conjunto de registros** para recuperar um par de campos comumente usados. A propriedade [valor](../../../ado/reference/ado-api/value-property-ado.md) do objeto **Field** retorna o conteúdo desejado.  
  
-   O campo acessado com a constante **adDefaultStream** contém um fluxo padrão associado ao objeto **Record** ou **Recordset** . O provedor atribui um fluxo padrão a um objeto.  
  
-   O campo acessado com a constante **adRecordURL** contém a URL absoluta que identifica o documento.  
  
 Um provedor de origem de documento não dá suporte à coleção de [Propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) de objetos de **registro** e de **campo** . O conteúdo da coleção de **Propriedades** é nulo para esses objetos.  
  
 Um provedor de origem de documento pode adicionar uma propriedade específica do provedor, como o **tipo DataSource** , para identificar se é um provedor de origem de documento. Para obter mais informações sobre como determinar seu tipo de provedor, consulte a documentação do provedor.  
  
## <a name="resource-recordset-columns"></a>Colunas do conjunto de registros de recursos  
 Um *conjunto de registros de recurso* consiste nas colunas a seguir.  
  
|Nome da coluna|Tipo|Description|  
|-----------------|----------|-----------------|  
|RESOURCE_PARSENAME|AdVarWChar|Somente leitura. Indica a URL do recurso.|  
|RESOURCE_PARENTNAME|AdVarWChar|Somente leitura. Indica a URL absoluta do registro pai.|  
|RESOURCE_ABSOLUTEPARSENAME|AdVarWChar|Somente leitura. Indica a URL absoluta do recurso, que é a concatenação de PARENTname e PARSEname.|  
|RESOURCE_ISHIDDEN|AdBoolean|True se o recurso estiver oculto. Nenhuma linha será retornada, a menos que o comando que cria o conjunto de linhas explicitamente Selecione linhas em que RESOURCE_ISHIDDEN é true.|  
|RESOURCE_ISREADONLY|AdBoolean|True se o recurso for somente leitura. Tenta abrir esse recurso com DBBINDFLAG_WRITE e falhará com DB_E_READONLY. Essa propriedade pode ser editada mesmo quando o recurso tiver sido aberto apenas para leitura.|  
|RESOURCE_CONTENTTYPE|AdVarWChar|Indica o uso provável do documento – por exemplo, uma breve advogado. Isso pode corresponder ao modelo do Office que foi usado para criar o documento.|  
|RESOURCE_CONTENTCLASS|AdVarWChar|Indica o tipo MIME do documento, indicando o formato como " `text/html` ".|  
|RESOURCE_CONTENTLANGUAGE|AdVarWChar|Indica o idioma no qual o conteúdo é armazenado.|  
|RESOURCE_CREATIONTIME|adFileTime|Somente leitura. Indica uma estrutura FILETIME que contém a hora em que o recurso foi criado. A hora é relatada no formato UTC (tempo Universal Coordenado).|  
|RESOURCE_LASTACCESSTIME|AdFileTime|Somente leitura. Indica uma estrutura FILETIME que contém a hora em que o recurso foi acessado pela última vez. A hora está no formato UTC. Os membros FILETIME serão zero se o provedor não oferecer suporte a esse membro de tempo.|  
|RESOURCE_LASTWRITETIME|AdFileTime|Somente leitura. Indica uma estrutura FILETIME que contém a hora em que o recurso foi gravado pela última vez. A hora está no formato UTC. Os membros FILETIME serão zero se o provedor não oferecer suporte a esse membro de tempo.|  
|RESOURCE_STREAMSIZE|asUnsignedBigInt|Somente leitura. Indica o tamanho do fluxo padrão do recurso, em bytes.|  
|RESOURCE_ISCOLLECTION|AdBoolean|Somente leitura. True se o recurso for uma coleção, como um diretório. False se o recurso for um arquivo simples.|  
|RESOURCE_ISSTRUCTUREDDOCUMENT|AdBoolean|True se o recurso for um documento estruturado. False se o recurso não for um documento estruturado. Pode ser uma coleção ou um arquivo simples.|  
|DEFAULT_DOCUMENT|AdVarWChar|Somente leitura. Indica que esse recurso contém uma URL para o documento simples padrão de uma pasta ou um documento estruturado. Usado quando o fluxo padrão é solicitado de um recurso. Essa propriedade está em branco para um arquivo simples.|  
|CHAPTERED_CHILDREN|AdChapter|Somente leitura. Opcional. Indica o capítulo do conjunto de linhas que contém os filhos do recurso. (O *provedor de OLE DB para publicação na Internet* não usa esta coluna.)|  
|RESOURCE_DISPLAYNAME|AdVarWChar|Somente leitura. Indica o nome de exibição do recurso.|  
|RESOURCE_ISROOT|AdBoolean|Somente leitura. True se o recurso for a raiz de uma coleção ou documento estruturado.|  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Apêndice A: Provedores](../../../ado/guide/appendixes/appendix-a-providers.md)
