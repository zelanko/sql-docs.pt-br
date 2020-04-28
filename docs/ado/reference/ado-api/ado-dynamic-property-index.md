---
title: Índice de propriedades dinâmicas do ADO | Microsoft Docs
ms.prod: sql
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- dynamic properties [ADO], index
ms.assetid: 80d389dd-46ef-459f-b0d4-6f712fc4f32d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9eb88905f56abf9c1c702f5fd73cbe61a1bcde3d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67921088"
---
# <a name="ado-dynamic-property-index"></a>Índice da propriedade dinâmica do ADO
Provedores de dados, provedores de serviços e componentes de serviço podem adicionar propriedades dinâmicas às coleções de **Propriedades** dos objetos de [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) e de [conexões](../../../ado/reference/ado-api/connection-object-ado.md) não abertas. Um determinado provedor também pode inserir propriedades adicionais quando esses objetos são abertos. Algumas dessas propriedades são listadas na seção [propriedades dinâmicas do ADO](../../../ado/reference/ado-api/ado-dynamic-properties.md) . Mais estão listados sob os provedores específicos na seção [Apêndice A: provedores](../../../ado/guide/appendixes/appendix-a-providers.md) .  
  
 As tabelas a seguir são índices cruzados dos nomes do ADO e do OLE DB para cada propriedade dinâmica do provedor de OLE DB padrão. Seus provedores podem adicionar mais propriedades do que as listadas aqui. Para obter informações específicas sobre propriedades dinâmicas específicas do provedor, consulte a documentação do provedor.  
  
 A referência do programador de OLE DB refere-se a um nome de propriedade ADO pelo termo "Descrição". Para obter mais informações sobre essas propriedades padrão, pesquise ou procure o índice na [documentação do OLE DB](https://msdn.microsoft.com/library/windows/desktop/ms722784.aspx)para a propriedade OLE DB por seu nome.  
  
## <a name="connection-dynamic-properties"></a>Propriedades dinâmicas da conexão  
  
|Nome da propriedade ADO|Nome da propriedade de OLE DB|  
|-----------------------|--------------------------|  
|Sessões ativas|DBPROP_ACTIVESESSIONS|  
|Anular Asynchable|DBPROP_ASYNCTXNABORT|  
|Asynchable confirmação|DBPROP_ASYNCTNXCOMMIT|  
|Níveis de isolamento de confirmação automática|DBPROP_SESS_AUTOCOMMITISOLEVELS|  
|Local do catálogo|DBPROP_CATALOGLOCATION|  
|Termo do catálogo|DBPROP_CATALOGTERM|  
|Definição de coluna|DBPROP_COLUMNDEFINITION|  
|Connect Timeout|DBPROP_INIT_TIMEOUT|  
|Catálogo atual|DBPROP_CURRENTCATALOG|  
|fonte de dados|DBPROP_INIT_DATASOURCE|  
|Nome da Fonte de Dados|DBPROP_DATASOURCENAME|  
|Modelo de Threading do objeto de fonte de dados|DBPROP_DSOTHREADMODEL|  
|Nome do DBMS|DBPROP_DBMSNAME|  
|Versão do DBMS|DBPROP_DBMSVER|  
|Propriedades estendidas|DBPROP_INIT_PROVIDERSTRING|  
|Agrupar por suporte|DBPROP_GROUPBY|  
|Suporte a tabelas heterogêneas|DBPROP_HETEROGENEOUSTABLES|  
|Diferenciar maiúsculas de minúsculas|DBPROP_IDENTIFIERCASE|  
|Catálogo Inicial|DBPROP_INIT_CATALOG|  
|Níveis de isolamento|DBPROP_SUPPORTEDTXNISOLEVELS|  
|Retenção de isolamento|DBPROP_SUPPORTEDTXNISORETAIN|  
|Identificador de Localidade|DBPROP_INIT_LCID|  
|Local|DBPROP_INIT_LOCATION|  
|Tamanho máximo do índice|DBPROP_MAXINDEXSIZE|  
|Tamanho máximo da linha|DBPROP_MAXROWSIZE|  
|O tamanho máximo da linha inclui o BLOB|DBPROP_MAXROWSIZEINCLUDESBLOB|  
|Máximo de tabelas em SELECT|DBPROP_MAXTABLESINSELECT|  
|Mode|DBPROP_INIT_MODE|  
|Vários conjuntos de parâmetros|DBPROP_MULTIPLEPARAMSETS|  
|Vários resultados|DBPROP_MULTIPLERESULTS|  
|Vários objetos de armazenamento|DBPROP_MULTIPLESTORAGEOBJECTS|  
|Atualização de várias tabelas|DBPROP_MULTITABLEUPDATE|  
|Ordem de agrupamento nula|DBPROP_NULLCOLLATION|  
|Comportamento de concatenação NULL|DBPROP_CONCATNULLBEHAVIOR|  
|Serviços OLE DBs|DBPROP_INIT_OLEDBSERVICES|  
|Versão do OLE DB|DBPROP_PROVIDEROLEDBVER|  
|Suporte a objeto OLE|DBPROP_OLEOBJECTS|  
|Abrir suporte a conjunto de linhas|DBPROP_OPENROWSETSUPPORT|  
|CLASSIFICAR por colunas na lista de seleção|DBPROP_ORDERBYCOLUMNSINSELECT|  
|Disponibilidade do parâmetro de saída|DBPROP_OUTPUTPARAMETERAVAILABILITY|  
|Acessadores de passagem por referência|DBPROP_BYREFACCESSORS|  
|Senha|DBPROP_AUTH_PASSWORD|  
|Informações de Persistência de Segurança|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|  
|Tipo de ID persistente|DBPROP_PERSISTENTIDTYPE|  
|Preparar comportamento de anulação|DBPROP_PREPAREABORTBEHAVIOR|  
|Preparar comportamento de confirmação|DBPROP_PREPARECOMMITBEHAVIOR|  
|Termo do procedimento|DBPROP_PROCEDURETERM|  
|Prompt|DBPROP_INIT_PROMPT|  
|Nome amigável do provedor|DBPROP_PROVIDERFRIENDLYNAME|  
|Nome do Provedor|DBPROP_PROVIDERFILENAME|  
|Versão do provedor|DBPROP_PROVIDERVER|  
|Fonte de dados somente leitura|DBPROP_DATASOURCEREADONLY|  
|Conversões de conjunto de linhas no comando|DBPROP_ROWSETCONVERSIONSONCOMMAND|  
|Termo do esquema|DBPROP_SCHEMATERM|  
|Uso do esquema|DBPROP_SCHEMAUSAGE|  
|Suporte a SQL|DBPROP_SQLSUPPORT|  
|Armazenamento estruturado|DBPROP_STRUCTUREDSTORAGE|  
|Suporte a subconsulta|DBPROP_SUBQUERIES|  
|Termo da tabela|DBPROP_TABLETERM|  
|DDL de transação|DBPROP_SUPPORTEDTXNDDL|  
|Id de Usuário|DBPROP_AUTH_USERID|  
|Nome do Usuário|DBPROP_USERNAME|  
|Identificador da Janela|DBPROP_INIT_HWND|  
  
## <a name="recordset-dynamic-properties"></a>Propriedades dinâmicas do conjunto de registros  
 Observe que as **propriedades dinâmicas** do objeto **Recordset** saem do escopo (tornam-se indisponíveis) quando o **conjunto de registros** é fechado.  
  
|Nome da propriedade ADO|Nome da propriedade de OLE DB|  
|-----------------------|--------------------------|  
|IAccessor|DBPROP_IACCESSOR|  
|IChapteredRowset||  
|IColumnsInfo|DBPROP_ICOLUMNSINFO|  
|IColumnsRowset|DBPROP_ICOLUMNSROWSET|  
|IConnectionPointContainer|DBPROP_ICONNECTIONPOINTCONTAINER|  
|IConvertType||  
|ILockBytes|DBPROP_ILOCKBYTES|  
|IRowset|DBPROP_IROWSET|  
|IDBAsynchStatus|DBPROP_IDBASYNCHSTATUS|  
|IParentRowset||  
|IRowsetChange|DBPROP_IROWSETCHANGE|  
|IRowsetExactScroll||  
|IRowsetFind|DBPROP_IROWSETFIND|  
|IRowsetIdentity|DBPROP_IROWSETIDENTITY|  
|IRowsetInfo|DBPROP_IROWSETINFO|  
|IRowsetLocate|DBPROP_IROWSETLOCATE|  
|IRowsetRefresh|DBPROP_IROWSETREFRESH|  
|IRowsetResynch||  
|IRowsetScroll|DBPROP_IROWSETSCROLL|  
|IRowsetUpdate|DBPROP_IROWSETUPDATE|  
|IRowsetView|DBPROP_IROWSETVIEW|  
|IRowsetIndex|DBPROP_IROWSETINDEX|  
|ISequentialStream|DBPROP_ISEQUENTIALSTREAM|  
|IStorage|DBPROP_ISTORAGE|  
|IStream|DBPROP_ISTREAM|  
|ISupportErrorInfo|DBPROP_ISUPPORTERRORINFO|  
|Ordem de acesso|DBPROP_ACCESSORDER|  
|Conjunto de linhas somente acréscimo|DBPROP_APPENDONLY|  
|Processamento de conjunto de linhas assíncrono|DBPROP_ROWSET_ASYNCH|  
|Recálculo automático|DBPROP_ADC_AUTORECALC|  
|Tamanho de busca em segundo plano|DBPROP_ASYNCHFETCHSIZE|  
|Prioridade de Thread de Segundo Plano|DBPROP_ASYNCHTHREADPRIORITY|  
|Tamanho do lote|DBPROP_ADC_BATCHSIZE|  
|Bloqueando objetos de armazenamento|DBPROP_BLOCKINGSTORAGEOBJECTS|  
|Tipo de indicador|DBPROP_BOOKMARKTYPE|  
|Indicação|DBPROP_IROWSETLOCATE|  
|Indicadores ordenados|DBPROP_ORDEREDBOOKMARKS|  
|Linhas filhas de cache|DBPROP_ADC_CACHECHILDROWS|  
|Colunas adiadas do cache|DBPROP_CACHEDEFERRED|  
|Alterar linhas inseridas|DBPROP_CHANGEINSERTEDROWS|  
|Privilégios de coluna|DBPROP_COLUMNRESTRICT|  
|Notificação de conjunto de colunas|DBPROP_NOTIFYCOLUMNSET|  
|Coluna gravável|DBPROP_MAYWRITECOLUMN|  
|Tempo limite do comando|DBPROP_COMMANDTIMEOUT|  
|Versão do mecanismo de cursor|DBPROP_ADC_CEVER|  
|Adiar coluna|DBPROP_DEFERRED|  
|Atrasar atualizações de objeto de armazenamento|DBPROP_DELAYSTORAGEOBJECTS|  
|Buscar versões anteriores|DBPROP_CANFETCHBACKWARDS|  
|Operações de filtro|DBPROP_FILTERCOMPAREOPS|  
|Operações de localização|DBPROP_FINDCOMPAREOPS|  
|Colunas ocultas (contagem)|DBPROP_HIDDENCOLUMNS|  
|Linhas de espera|DBPROP_CANHOLDROWS|  
|Linhas irmóveis|DBPROP_IMMOBILEROWS|  
|Tamanho inicial da busca|DBPROP_ASYNCHPREFETCHSIZE|  
|Indicadores literais|DBPROP_LITERALBOOKMARKS|  
|Identidade de linha literal|DBPROP_LITERALIDENTITY|  
|Manter status da alteração|DBPROP_ADC_MAINTAINCHANGESTATUS|  
|Máximo de linhas abertas|DBPROP_MAXOPENROWS|  
|Máximo de linhas pendentes|DBPROP_MAXPENDINGROWS|  
|Máximo de linhas|DBPROP_MAXROWS|  
|Uso de Memória|DBPROP_MEMORYUSAGE|  
|Granularidade da notificação|DBPROP_NOTIFICATIONGRANULARITY|  
|Fases de notificação|DBPROP_NOTIFICATIONPHASES|  
|Objetos transacionados|DBPROP_TRANSACTEDOBJECT|  
|Alterações de outros visíveis|DBPROP_OTHERUPDATEDELETE|  
|Inserções de outros visíveis|DBPROP_OTHERINSERT|  
|Próprias alterações visíveis|DBPROP_OWNUPDATEDELETE|  
|Próprias inserções visíveis|DBPROP_OWNINSERT|  
|Preservar ao abortar|DBPROP_ABORTPRESERVE|  
|Preservar ao confirmar|DBPROP_COMMITPRESERVE|  
|Private1||  
|Reinicialização rápida|DBPROP_QUICKRESTART|  
|Eventos reentrante|DBPROP_REENTRANTEVENTS|  
|Remover linhas excluídas|DBPROP_REMOVEDELETED|  
|Relatar várias alterações|DBPROP_REPORTMULTIPLECHANGES|  
|Remodelar nome|DBPROP_ADC_RESHAPENAME|  
|Comando Ressync|DBPROP_ADC_CUSTOMRESYNCH|  
|Retornar inserções pendentes|DBPROP_RETURNPENDINGINSERTS|  
|Notificação de exclusão de linha|DBPROP_NOTIFYROWDELETE|  
|Notificação da primeira alteração da linha|DBPROP_NOTIFYROWFIRSTCHANGE|  
|Notificação de inserção de linha|DBPROP_NOTIFYROWINSERT|  
|Privilégios de linha|DBPROP_ROWRESTRICT|  
|Notificação de ressincronização de linha|DBPROP_NOTIFYROWRESYNCH|  
|Modelo de threading de linha|DBPROP_ROWTHREADMODEL|  
|Notificação de desfazer alteração de linha|DBPROP_NOTIFYROWUNDOCHANGE|  
|Notificação de desfazer exclusão de linha|DBPROP_NOTIFYROWUNDODELETE|  
|Notificação de desfazer inserção de linha|DBPROP_NOTIFYROWUNDOINSERT|  
|Notificação de atualização de linha|DBPROP_NOTIFYROWUPDATE|  
|Notificação de alteração de posição de busca de conjunto de linhas|DBPROP_NOTIFYROWSETFETCHPOSITIONCHANGE|  
|Notificação de liberação de conjunto de linhas|DBPROP_NOTIFYROWSETRELEASE|  
|Rolar para trás|DBPROP_CANSCROLLBACKWARDS|  
|Cursor do servidor|DBPROP_SERVERCURSOR|  
|Ignorar indicadores excluídos|DBPROP_BOOKMARKSKIPPED|  
|Identidade de linha forte|DBPROP_STRONGIDENTITY|  
|Catálogo exclusivo|DBPROP_ADC_UNIQUECATALOG|  
|Linhas exclusivas|DBPROP_UNIQUEROWS|  
|Esquema exclusivo|DBPROP_ADC_UNIQUESCHEMA|  
|Tabela única|DBPROP_ADC_UNIQUETABLE|  
|Capacidade|DBPROP_UPDATABILITY|  
|Critérios de atualização|DBPROP_ADC_UPDATECRITERIA|  
|Atualizar ressincronização|DBPROP_ADC_UPDATERESYNC|  
|Usar indicadores|DBPROP_BOOKMARKS|
