---
description: Visão geral do Microsoft OLE DB Provider para serviço de indexação da Microsoft
title: Provedor do Microsoft OLE DB para Microsoft Indexing Service | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Indexing Service provider [ADO]
- providers [ADO], OLE DB provider for Microsoft Indexing service
- OLE DB provider for Microsoft Indexing service [ADO]
ms.assetid: f86a0598-5097-471b-8318-d2c859d085f2
author: rothja
ms.author: jroth
ms.openlocfilehash: b3e479ca023efb704bf496c9ffaeaca2f1b6ba15
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991037"
---
# <a name="microsoft-ole-db-provider-for-microsoft-indexing-service-overview"></a>Visão geral do Microsoft OLE DB Provider para serviço de indexação da Microsoft
O provedor de OLE DB da Microsoft para o serviço de indexação da Microsoft fornece acesso somente leitura programático aos dados do sistema de arquivos e da Web indexados pelo serviço de indexação da Microsoft. Os aplicativos ADO podem emitir consultas SQL para recuperar conteúdo e informações de propriedade de arquivo.

 O provedor está livre de threads e UNICODE habilitado.

## <a name="connection-string-parameters"></a>Parâmetros de cadeia de conexão
 Para se conectar a esse provedor, defina o argumento **Provider =** como a propriedade [ConnectionString](../../reference/ado-api/connectionstring-property-ado.md) como:

```vb
MSIDXS
```

 A leitura da propriedade [Provider](../../reference/ado-api/provider-property-ado.md) retornará essa cadeia de caracteres também.

## <a name="typical-connection-string"></a>Cadeia de conexão típica
 Uma cadeia de conexão típica para esse provedor é:

```vb
"Provider=MSIDXS;Data Source=myCatalog;Locale Identifier=nnnn;"
```

 A cadeia de caracteres consiste nessas palavras-chave:

|Palavra-chave|Descrição|
|-------------|-----------------|
|**Provedor**|Especifica o provedor de OLE DB para o serviço de indexação da Microsoft. Normalmente, essa é a única palavra-chave especificada na cadeia de conexão.|
|**Fonte de Dados**|Especifica o nome do catálogo do serviço de indexação. Se essa palavra-chave não for especificada, o catálogo de sistema padrão será usado.|
|**Identificador de Localidade**|Especifica um número exclusivo de bits de 32 (por exemplo, 1033) que especifica as preferências relacionadas ao idioma do usuário. Se essa palavra-chave não for especificada, o identificador de localidade do sistema padrão será usado.|

## <a name="command-text"></a>Texto do comando
 A sintaxe de consulta SQL do serviço de indexação consiste em extensões para a instrução **Select** do sql-92 e suas cláusulas **from** e **Where** . Os resultados da consulta são retornados por meio de conjuntos de linhas OLE DB, que podem ser consumidos pelo ADO e manipulados como objetos [Recordset](../../reference/ado-api/recordset-object-ado.md) .

 Você pode pesquisar palavras ou frases exatas ou usar caracteres curinga para Pesquisar padrões ou derivações de palavras. A lógica de pesquisa pode ser baseada em decisões booleanas, termos ponderados ou proximidade com outras palavras. Você também pode pesquisar por "texto livre", que localiza correspondências com base no significado, em vez de palavras exatas.

 O dialeto de comando específico está totalmente documentado nas linguagens de consulta para a documentação do serviço de indexação.

 O provedor não aceita chamadas de procedimento armazenado ou nomes de tabela simples (por exemplo, a propriedade [CommandType](../../reference/ado-api/commandtype-property-ado.md) será sempre **adCmdText**).

## <a name="recordset-behavior"></a>Comportamento do conjunto de registros
 As tabelas a seguir listam os recursos disponíveis com um objeto **Recordset** aberto com esse provedor. Somente o tipo de cursor estático (**adOpenStatic**) está disponível.

 Para obter informações mais detalhadas sobre o comportamento do **conjunto de registros** para a configuração do provedor, execute o método de [suporte](../../reference/ado-api/supports-method.md) e enumere a coleção [Properties](../../reference/ado-api/properties-collection-ado.md) do **conjunto de registros** para determinar se as propriedades dinâmicas específicas do provedor estão presentes.

 **Disponibilidade das propriedades padrão do conjunto de registros ADO:**

|Propriedade|Disponibilidade|
|--------------|------------------|
|[AbsolutePage](../../reference/ado-api/absolutepage-property-ado.md)|leitura/gravação|
|[AbsolutePosition](../../reference/ado-api/absoluteposition-property-ado.md)|leitura/gravação|
|[ActiveConnection](../../reference/ado-api/activeconnection-property-ado.md)|somente leitura|
|[BOF](../../reference/ado-api/bof-eof-properties-ado.md)|somente leitura|
|[Indicador](../../reference/ado-api/bookmark-property-ado.md)*|leitura/gravação|
|[CacheSize](../../reference/ado-api/cachesize-property-ado.md)|leitura/gravação|
|[CursorLocation](../../reference/ado-api/cursorlocation-property-ado.md)|sempre **adUseServer**|
|[CursorType](../../reference/ado-api/cursortype-property-ado.md)|sempre **adOpenStatic**|
|[EditMode](../../reference/ado-api/editmode-property.md)|sempre **adEditNone**|
|[EOF](../../reference/ado-api/bof-eof-properties-ado.md)|somente leitura|
|[Filter](../../reference/ado-api/filter-property.md)|leitura/gravação|
|[LockType](../../reference/ado-api/locktype-property-ado.md)|leitura/gravação|
|[MarshalOptions](../../reference/ado-api/marshaloptions-property-ado.md)|não disponível|
|[MaxRecords](../../reference/ado-api/maxrecords-property-ado.md)|leitura/gravação|
|[PageCount](../../reference/ado-api/pagecount-property-ado.md)|somente leitura|
|[PageSize](../../reference/ado-api/pagesize-property-ado.md)|leitura/gravação|
|[RecordCount](../../reference/ado-api/recordcount-property-ado.md)|somente leitura|
|[Origem](../../reference/ado-api/source-property-ado-recordset.md)|leitura/gravação|
|[State](../../reference/ado-api/state-property-ado.md)|somente leitura|
|[Status](../../reference/ado-api/status-property-ado-recordset.md)|somente leitura|

 \*Os indicadores devem ser habilitados no provedor para que esse recurso exista no conjunto de **registros**.

 **Disponibilidade de métodos Recordset padrão do ADO:**

|Método|Disponível?|
|------------|----------------|
|[AddNew](../../reference/ado-api/addnew-method-ado.md)|Não|
|[Cancelar](../../reference/ado-api/cancel-method-ado.md)|Sim|
|[CancelBatch](../../reference/ado-api/cancelbatch-method-ado.md)|Não|
|[CancelUpdate](../../reference/ado-api/cancelupdate-method-ado.md)|Não|
|[Clone](../../reference/ado-api/clone-method-ado.md)|Sim|
|[Fechar](../../reference/ado-api/close-method-ado.md)|Sim|
|[Delete (excluir)](../../reference/ado-api/delete-method-ado-recordset.md)|Não|
|[GetRows](../../reference/ado-api/getrows-method-ado.md)|Sim|
|[Mover](../../reference/ado-api/move-method-ado.md)|Sim|
|[MoveFirst](../../reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Sim|
|[NextRecordset](../../reference/ado-api/nextrecordset-method-ado.md)|Sim|
|[Abrir](../../reference/ado-api/open-method-ado-recordset.md)|Sim|
|[Repita](../../reference/ado-api/requery-method.md)|Sim|
|[Sincronizar novamente](../../reference/ado-api/resync-method.md)|Sim|
|[Suporta](../../reference/ado-api/supports-method.md)|Sim|
|[Atualização](../../reference/ado-api/update-method.md)|Não|
|[UpdateBatch](../../reference/ado-api/updatebatch-method.md)|Não|

 Para obter detalhes de implementação específicos e informações funcionais sobre o provedor de OLE DB da Microsoft para o serviço de indexação da Microsoft, consulte o [Guia do programador de OLE DB](/previous-versions/windows/desktop/ms713643(v=vs.85))ou visite a página de serviços da Web do site do Windows NT Server.

## <a name="see-also"></a>Consulte Também
 Propriedade [CommandType](../../reference/ado-api/commandtype-property-ado.md) (ADO) [ConnectionString](../../reference/ado-api/connectionstring-property-ado.md) Property (ADO) [Properties Collection](../../reference/ado-api/properties-collection-ado.md) (ADO [) (ADO](../../reference/ado-api/provider-property-ado.md) ) [Recordset Object (](../../reference/ado-api/recordset-object-ado.md) ADO) continha o [método](../../reference/ado-api/supports-method.md)