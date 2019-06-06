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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2b7ce62ebedbd5d0622c8b69720f7153d7711a48
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700448"
---
# <a name="records-and-provider-supplied-fields"></a>Registros e campos fornecidos pelo provedor
Quando um [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto é aberto, sua origem pode ser a linha atual de um aberto [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md), uma URL absoluta ou uma URL relativa em conjunto com um aberto [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto .  
  
 Se o **registro** é aberta a partir um **conjunto de registros**, o **registro** objeto [campos](../../../ado/reference/ado-api/fields-collection-ado.md) coleção conterá todos os campos a  **Conjunto de registros**, além de todos os campos adicionados pelo provedor subjacente.  
  
 O provedor poderá inserir campos adicionais que servem como suplementares características do **registro**. Como resultado, uma **registro** podem ter campos exclusivos não na **conjunto de registros** como um todo ou em qualquer **registro** derivada de outra linha do **Recordset**.  
  
 Por exemplo, todas as linhas de uma **Recordset** derivado de um email de fonte de dados pode ter colunas, tais como de, para e de assunto. Um **registro** derivada dessa **Recordset** terão os mesmos campos. No entanto, o **registro** também podem ter outros campos exclusivos à mensagem específica representada por este **registro**, como anexo e Cc (cópia carbono).  
  
 Embora o **registro** objeto e a linha atual do **conjunto de registros** têm os mesmos campos, eles são diferentes porque **registro** e **Recordset**objetos têm diferentes métodos e propriedades.  
  
 Um campo mantido em comum pela **registro** e **Recordset** podem ser modificados em um objeto. No entanto, o campo não pode ser excluído na **registro** do objeto, embora o provedor subjacente possa oferecer suporte ao definir o campo como nulo.  
  
 Após o **registro** é aberto, você pode adicionar programaticamente campos. Você também pode excluir campos que você adicionou, mas você não pode excluir campos de original **conjunto de registros**.  
  
 Você também pode abrir o **registro** objeto diretamente a partir de uma URL. Nesse caso, os campos adicionados para o **registro** dependem do provedor subjacente. Atualmente, a maioria dos provedores de adicionar um conjunto de campos que descrevem a entidade representada pela **registro**. Se a entidade consiste em um fluxo de bytes, como um arquivo simple, uma [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objeto geralmente pode ser aberto na **registro**.  
  
## <a name="special-fields-for-document-source-providers"></a>Provedores de fonte de campos especiais para documento  
 Uma classe especial de provedores, chamado *provedores de origem de documento*, gerencia pastas e documentos. Quando um **registro** objeto representa um documento ou uma **Recordset** objeto representa uma pasta de documentos, o provedor de código-fonte do documento preenche esses objetos com um conjunto exclusivo de campos que descrevem características do documento em vez disso, de real próprio documento. Normalmente, um campo contém uma referência para o **Stream** que representa o documento.  
  
 Esses campos constituem um recurso **registro** ou **conjunto de registros** e são listadas para os provedores específicos que dão suporte a eles no [apêndice a: Provedores de](../../../ado/guide/appendixes/appendix-a-providers.md).  
  
 Índice de duas constantes a **campos** coleção de um recurso **registro** ou **Recordset** para recuperar um par de campos comumente usados. O **campo** objeto [valor](../../../ado/reference/ado-api/value-property-ado.md) propriedade retorna o conteúdo desejado.  
  
-   O campo acessado com o **adDefaultStream** constante contém um fluxo padrão associado a **registro** ou **Recordset** objeto. O provedor atribui um fluxo padrão para um objeto.  
  
-   O campo acessado com o **adRecordURL** constante contém a URL absoluta que identifica o documento.  
  
 Um provedor de origem de documento não dá suporte a [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção de **registro** e **campo** objetos. O conteúdo a **propriedades** coleção é nula para esses objetos.  
  
 Um provedor de código-fonte do documento pode adicionar uma propriedade específica do provedor, como **tipo de fonte de dados** para identificar se ele é um provedor de origem do documento. Para obter mais informações sobre como determinar o tipo de provedor, consulte a documentação do provedor.  
  
## <a name="resource-recordset-columns"></a>Colunas do conjunto de registros de recursos  
 Um *conjunto de registros de recurso* consiste nas seguintes colunas.  
  
|Nome da coluna|Tipo|Descrição|  
|-----------------|----------|-----------------|  
|RESOURCE_PARSENAME|AdVarWChar|Somente leitura. Indica a URL do recurso.|  
|RESOURCE_PARENTNAME|AdVarWChar|Somente leitura. Indica a URL absoluta do registro pai.|  
|RESOURCE_ABSOLUTEPARSENAME|AdVarWChar|Somente leitura. Indica a URL absoluta do recurso, que é a concatenação de PARENTNAME e PARSENAME.|  
|RESOURCE_ISHIDDEN|adBoolean|True se o recurso está oculto. Nenhuma linha será retornada, a menos que o comando que cria o conjunto de linhas explicitamente seleciona linhas onde RESOURCE_ISHIDDEN é True.|  
|RESOURCE_ISREADONLY|adBoolean|True se o recurso for somente leitura. Tenta abrir este recurso com DBBINDFLAG_WRITE e vai falha com DB_E_READONLY. Essa propriedade pode ser editada, mesmo quando o recurso só foi aberto para leitura.|  
|RESOURCE_CONTENTTYPE|AdVarWChar|Indica o probabilidade de uso do documento-por exemplo, um advogado do breve. Isso pode corresponder ao modelo do Office que foi usado para criar o documento.|  
|RESOURCE_CONTENTCLASS|AdVarWChar|Indica o tipo MIME do documento, que indica o formato como "`text/html`".|  
|RESOURCE_CONTENTLANGUAGE|AdVarWChar|Indica o idioma no qual o conteúdo é armazenado.|  
|RESOURCE_CREATIONTIME|adFileTime|Somente leitura. Indica uma estrutura FILETIME que contém a hora em que o recurso foi criado. A hora é relatada no formato Tempo Universal Coordenado (UTC).|  
|RESOURCE_LASTACCESSTIME|AdFileTime|Somente leitura. Indica uma estrutura FILETIME que contém a hora em que o recurso foi acessado pela última vez. A hora está no formato UTC. Os membros FILETIME são zero se o provedor não dá suporte a esse membro de tempo.|  
|RESOURCE_LASTWRITETIME|AdFileTime|Somente leitura. Indica uma estrutura FILETIME que contém a hora em que o recurso foi gravado pela última vez. A hora está no formato UTC. Os membros FILETIME são zero se o provedor não dá suporte a esse membro de tempo.|  
|RESOURCE_STREAMSIZE|asUnsignedBigInt|Somente leitura. Indica o tamanho do fluxo de padrão do recurso, em bytes.|  
|RESOURCE_ISCOLLECTION|adBoolean|Somente leitura. True se o recurso é uma coleção, como um diretório. False se o recurso é um arquivo simple.|  
|RESOURCE_ISSTRUCTUREDDOCUMENT|adBoolean|True se o recurso for um documento estruturado. False se o recurso não é um documento estruturado. Ele pode ser uma coleção ou um arquivo simples.|  
|DEFAULT_DOCUMENT|AdVarWChar|Somente leitura. Indica que este recurso contém uma URL para o documento simples do padrão de uma pasta ou um documento estruturado. Usado quando o fluxo padrão é solicitado de um recurso. Esta propriedade é em branco para um arquivo simples.|  
|CHAPTERED_CHILDREN|adChapter|Somente leitura. Opcional. Indica o capítulo do conjunto de linhas que contém os filhos do recurso. (O *provedor OLE DB para publicação na Internet* não usa essa coluna.)|  
|RESOURCE_DISPLAYNAME|AdVarWChar|Somente leitura. Indica o nome de exibição do recurso.|  
|RESOURCE_ISROOT|adBoolean|Somente leitura. True se o recurso é a raiz de uma coleção ou documento estruturado.|  
  
## <a name="see-also"></a>Consulte também  
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Apêndice a: provedores](../../../ado/guide/appendixes/appendix-a-providers.md)
