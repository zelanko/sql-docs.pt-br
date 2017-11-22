---
title: Registros e campos fornecidos pelo provedor | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- records-provided fields [ADO]
- provider-supplied fields [ADO]
ms.assetid: 77f95e0a-0cf2-411a-a792-593f77330fbd
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 16596d3ffa943f382e6c3a9ec2aa9c2e2e14432f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="records-and-provider-supplied-fields"></a>Registros e campos fornecidos pelo provedor
Quando um [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto está aberto, sua origem pode ser a linha atual de uma abertas [registros](../../../ado/reference/ado-api/recordset-object-ado.md), uma URL absoluta ou uma URL relativa em conjunto com um aberto [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto .  
  
 Se o **registro** é aberto a partir um **registros**, o **registro** objeto [campos](../../../ado/reference/ado-api/fields-collection-ado.md) coleção conterá todos os campos do  **Conjunto de registros**, além de todos os campos adicionados pelo provedor subjacente.  
  
 O provedor pode inserir campos adicionais que servem como suplementares características do **registro**. Como resultado, um **registro** pode ter campos exclusivos não no **Recordset** como um todo ou em qualquer **registro** derivado de outra linha do **registros**.  
  
 Por exemplo, todas as linhas de uma **registros** derivado de um email de fonte de dados pode ter colunas, tais como para e da entidade. Um **registro** derivada dessa **registros** terão os mesmos campos. No entanto, o **registro** também pode ter outros campos exclusivos para a mensagem em particular representada pelo **registro**, como anexo e Cc (cópia carbono).  
  
 Embora o **registro** objeto e a linha atual do **conjunto de registros** têm os mesmos campos, eles são diferentes porque **registro** e **Recordset**objetos têm propriedades e métodos diferentes.  
  
 Um campo mantido em comum o **registro** e **registros** pode ser modificada em um objeto. No entanto, o campo não pode ser excluído no **registro** do objeto, embora o provedor subjacente possa oferecer suporte a configuração do campo como nulo.  
  
 Após o **registro** é aberto, você pode programaticamente adicionar campos. Você também pode excluir campos que você adicionou, mas você não pode excluir campos de original **registros**.  
  
 Você também pode abrir o **registro** objeto diretamente a partir de uma URL. Nesse caso, os campos adicionados para o **registro** dependem do provedor subjacente. Atualmente, a maioria dos provedores de adicionar um conjunto de campos que descrevem a entidade representada pelo **registro**. Se a entidade consiste em um fluxo de bytes, como um arquivo simple, um [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) objeto geralmente pode ser aberto do **registro**.  
  
## <a name="special-fields-for-document-source-providers"></a>Provedores de código-fonte campos especiais para documento  
 Uma classe especial de provedores, chamado *provedores de origem de documento*, gerencia pastas e documentos. Quando um **registro** objeto representa um documento ou uma **registros** objeto representa uma pasta de documentos, o provedor de origem do documento preenche esses objetos com um conjunto de campos que descrevem exclusivo características do documento em vez disso, de real de documento em si. Normalmente, um campo contém uma referência para o **fluxo** que representa o documento.  
  
 Esses campos constituem um recurso **registro** ou **registros** e são listadas para os provedores específicos com suporte para elas no [apêndice a: provedores](../../../ado/guide/appendixes/appendix-a-providers.md).  
  
 Índice de duas constantes a **campos** coleção de um recurso **registro** ou **registros** para recuperar um par de campos comumente usados. O **campo** objeto [valor](../../../ado/reference/ado-api/value-property-ado.md) propriedade retorna o conteúdo desejado.  
  
-   O campo acessado com o **adDefaultStream** constante contém um fluxo padrão associado a **registro** ou **registros** objeto. O provedor atribui um fluxo padrão para um objeto.  
  
-   O campo acessado com o **adRecordURL** constante contém a URL absoluta que identifica o documento.  
  
 Um provedor de origem do documento não oferece suporte a [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção de **registro** e **campo** objetos. O conteúdo a **propriedades** coleção é nula para esses objetos.  
  
 Um provedor de origem do documento pode adicionar uma propriedade específica de provedor, como **o tipo de fonte de dados** para identificar se ele é um provedor de origem do documento. Para obter mais informações sobre como determinar o tipo de provedor, consulte a documentação do provedor.  
  
## <a name="resource-recordset-columns"></a>Colunas do conjunto de registros de recursos  
 Um *conjunto de registros de recursos* consiste nas seguintes colunas.  
  
|Nome da coluna|Tipo|Description|  
|-----------------|----------|-----------------|  
|RESOURCE_PARSENAME|AdVarWChar|Somente leitura. Indica a URL do recurso.|  
|RESOURCE_PARENTNAME|AdVarWChar|Somente leitura. Indica a URL absoluta do registro principal.|  
|RESOURCE_ABSOLUTEPARSENAME|AdVarWChar|Somente leitura. Indica a URL absoluta do recurso, que é a concatenação de PARENTNAME e PARSENAME.|  
|RESOURCE_ISHIDDEN|adBoolean|True se o recurso está oculto. Nenhuma linha será retornada, a menos que o comando que cria o conjunto de linhas explicitamente seleciona linhas onde RESOURCE_ISHIDDEN é True.|  
|RESOURCE_ISREADONLY|adBoolean|True se o recurso é somente leitura. Tenta abrir este recurso com DBBINDFLAG_WRITE e vai falha com DB_E_READONLY. Essa propriedade pode ser editada, mesmo quando o recurso só foi aberto para leitura.|  
|RESOURCE_CONTENTTYPE|AdVarWChar|Indica o uso de probabilidade do documento — por exemplo, um advogado do breve. Isto pode corresponder ao modelo do Office que foi usado para criar o documento.|  
|RESOURCE_CONTENTCLASS|AdVarWChar|Indica o tipo MIME do documento, que indica o formato como "`text/html`".|  
|RESOURCE_CONTENTLANGUAGE|AdVarWChar|Indica o idioma no qual o conteúdo é armazenado.|  
|RESOURCE_CREATIONTIME|adFileTime|Somente leitura. Indica uma estrutura FILETIME que contém a hora em que o recurso foi criado. O tempo é relatado no formato Tempo Universal Coordenado (UTC).|  
|RESOURCE_LASTACCESSTIME|adFileTime|Somente leitura. Indica uma estrutura FILETIME que contém a hora em que o recurso foi acessado pela última vez. A hora está no formato UTC. Os membros FILETIME são zero se o provedor não oferece suporte a esse membro de tempo.|  
|RESOURCE_LASTWRITETIME|adFileTime|Somente leitura. Indica uma estrutura FILETIME que contém a hora em que o recurso foi gravado pela última vez. A hora está no formato UTC. Os membros FILETIME são zero se o provedor não oferece suporte a esse membro de tempo.|  
|RESOURCE_STREAMSIZE|asUnsignedBigInt|Somente leitura. Indica o tamanho do fluxo de padrão do recurso, em bytes.|  
|RESOURCE_ISCOLLECTION|adBoolean|Somente leitura. True se o recurso é uma coleção, como um diretório. False se o recurso é um arquivo simple.|  
|RESOURCE_ISSTRUCTUREDDOCUMENT|adBoolean|True se o recurso for um documento estruturado. False se o recurso não é um documento estruturado. Pode ser uma coleção ou um arquivo simples.|  
|DEFAULT_DOCUMENT|AdVarWChar|Somente leitura. Indica que esse recurso contém uma URL para o documento simples padrão de uma pasta ou um documento estruturado. Usado quando for solicitado o fluxo de padrão de um recurso. Esta propriedade é em branco para um arquivo simples.|  
|CHAPTERED_CHILDREN|AdChapter|Somente leitura. Opcional. Indica o capítulo do conjunto de linhas que contém os filhos do recurso. (O *provedor OLE DB para Internet Publishing* não usar essa coluna.)|  
|RESOURCE_DISPLAYNAME|AdVarWChar|Somente leitura. Indica o nome de exibição do recurso.|  
|RESOURCE_ISROOT|adBoolean|Somente leitura. True se o recurso é a raiz de uma coleção ou um documento estruturado.|  
  
## <a name="see-also"></a>Consulte também  
 [Objeto de registro (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Apêndice A: Provedores](../../../ado/guide/appendixes/appendix-a-providers.md)
