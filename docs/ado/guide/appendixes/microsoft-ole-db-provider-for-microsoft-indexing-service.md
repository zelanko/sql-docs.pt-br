---
title: Provedor Microsoft OLE DB para Microsoft Indexing Service | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Indexing Service provider [ADO]
- providers [ADO], OLE DB provider for Microsoft Indexing service
- OLE DB provider for Microsoft Indexing service [ADO]
ms.assetid: f86a0598-5097-471b-8318-d2c859d085f2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1b4dfa4771fa60286e054270cb644c72cabe8e40
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62855851"
---
# <a name="microsoft-ole-db-provider-for-microsoft-indexing-service-overview"></a>Provedor Microsoft OLE DB para visão geral do serviço de indexação da Microsoft
O Microsoft OLE DB Provider for Microsoft Indexing Service fornece acesso programático de somente leitura para o sistema de arquivos e dados da Web indexados pelo serviço de indexação da Microsoft. Aplicativos ADO podem emitir consultas SQL para recuperar informações de propriedade de conteúdo e o arquivo.

 O provedor é de thread livre e UNICODE habilitado.

## <a name="connection-string-parameters"></a>Parâmetros de cadeia de caracteres de Conexão
 Para se conectar ao provedor, defina as **provedor =** argumento para o [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propriedade para:

```vb
MSIDXS
```

 Lendo a [provedor](../../../ado/reference/ado-api/provider-property-ado.md) propriedade retornará essa cadeia de caracteres.

## <a name="typical-connection-string"></a>Cadeia de caracteres de Conexão típica
 Uma cadeia de caracteres de conexão típica para esse provedor é:

```vb
"Provider=MSIDXS;Data Source=myCatalog;Locale Identifier=nnnn;"
```

 A cadeia de caracteres consiste nessas palavras-chave:

|Palavra-chave|Descrição|
|-------------|-----------------|
|**Provedor**|Especifica o provedor do OLE DB para Microsoft Indexing Service. Normalmente, essa é a única palavra-chave especificada na cadeia de conexão.|
|**Fonte de dados**|Especifica o nome do catálogo de serviço de indexação. Se essa palavra-chave não for especificado, o catálogo do sistema padrão será usado.|
|**Identificador de Localidade**|Especifica um número de 32 bits exclusivo (por exemplo, 1033) que especifica as preferências de idioma do usuário. Se essa palavra-chave não for especificado, o identificador de localidade do sistema padrão será usado.|

## <a name="command-text"></a>Texto do comando
 A sintaxe de consulta SQL do serviço de indexação consiste em extensões para o SQL-92 **selecionar** instrução e seu **FROM** e **onde** cláusulas. Os resultados da consulta são retornados por meio de conjuntos de linhas OLE DB, que podem ser consumidos pelo ADO e manipulados como [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objetos.

 Você pode procurar palavras exatas ou frases ou usar caracteres curinga para procurar padrões ou troncos de palavras. A lógica de pesquisa pode ser baseada em decisões de Boolianas, termos ponderados ou proximidade em outras palavras. Você também pode pesquisar por "texto livre", que localiza as correspondências com base em significado, em vez de palavras exatas.

 O dialeto do comando específico é totalmente documentado nas linguagens de consulta para obter a documentação do serviço de indexação.

 O provedor não aceita chamadas de procedimento armazenado ou nomes de tabela simples (por exemplo, o [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) propriedade sempre será **adCmdText**).

## <a name="recordset-behavior"></a>Comportamento do conjunto de registros
 As tabelas a seguir listam os recursos disponíveis com um **Recordset** objeto aberto com esse provedor. Somente o tipo de cursor estático (**adOpenStatic**) está disponível.

 Para obter mais informações sobre **conjunto de registros** comportamento para a sua configuração de provedor, execute o [dá suporte à](../../../ado/reference/ado-api/supports-method.md) método e enumerar os [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção da **Recordset** para determinar se as propriedades dinâmicas específicas do provedor estão presentes.

 **Disponibilidade de propriedades de conjunto de registros ADO padrão:**

|Propriedade|Disponibilidade|
|--------------|------------------|
|[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)|leitura/gravação|
|[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|leitura/gravação|
|[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)|somente leitura|
|[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|somente leitura|
|[Indicador](../../../ado/reference/ado-api/bookmark-property-ado.md)*|leitura/gravação|
|[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)|leitura/gravação|
|[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)|always **adUseServer**|
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|sempre **adOpenStatic**|
|[EditMode](../../../ado/reference/ado-api/editmode-property.md)|always **adEditNone**|
|[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|somente leitura|
|[Filter](../../../ado/reference/ado-api/filter-property.md)|leitura/gravação|
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|leitura/gravação|
|[MarshalOptions](../../../ado/reference/ado-api/marshaloptions-property-ado.md)|não disponível|
|[MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)|leitura/gravação|
|[PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)|somente leitura|
|[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)|leitura/gravação|
|[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)|somente leitura|
|[Origem](../../../ado/reference/ado-api/source-property-ado-recordset.md)|leitura/gravação|
|[Estado](../../../ado/reference/ado-api/state-property-ado.md)|somente leitura|
|[Status](../../../ado/reference/ado-api/status-property-ado-recordset.md)|somente leitura|

 \*Indicadores devem estar habilitados no provedor para que esse recurso existir na **conjunto de registros**.

 **Disponibilidade de métodos padrão do conjunto de registros ADO:**

|Método|Está disponível?|
|------------|----------------|
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|Não|
|[Cancelar](../../../ado/reference/ado-api/cancel-method-ado.md)|Sim|
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|Não|
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|Não|
|[Clone](../../../ado/reference/ado-api/clone-method-ado.md)|Sim|
|[Fechar](../../../ado/reference/ado-api/close-method-ado.md)|Sim|
|[Delete (excluir)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|Não|
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|Sim|
|[Migrar](../../../ado/reference/ado-api/move-method-ado.md)|Sim|
|[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Sim|
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)|Sim|
|[Abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md)|Sim|
|[Requery](../../../ado/reference/ado-api/requery-method.md)|Sim|
|[Resync](../../../ado/reference/ado-api/resync-method.md)|Sim|
|[Suporta](../../../ado/reference/ado-api/supports-method.md)|Sim|
|[Update (atualizar)](../../../ado/reference/ado-api/update-method.md)|Não|
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|Não|

 Para detalhes específicos de implementação e funcionais informações sobre o Microsoft OLE DB Provider para Microsoft Indexing Service, consulte o [guia do programador do DB OLE](https://msdn.microsoft.com/library/windows/desktop/ms713643.aspx), ou visite a página de serviços Web do Windows NT Server Web site.

## <a name="see-also"></a>Consulte também
 [Propriedade CommandType (ADO)](../../../ado/reference/ado-api/commandtype-property-ado.md) [propriedade ConnectionString (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [coleção Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) [propriedade Provider (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) [ O objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [dá suporte ao método](../../../ado/reference/ado-api/supports-method.md)
