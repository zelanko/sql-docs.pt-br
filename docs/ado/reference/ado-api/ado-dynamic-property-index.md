---
title: Índice de propriedade dinâmica do ADO | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 8dd1263d19972124166e1e11d91c8370fc3a9ff0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66696738"
---
# <a name="ado-dynamic-property-index"></a>Índice da propriedade dinâmica do ADO
Provedores de dados, provedores de serviços e componentes de serviço podem adicionar propriedades dinâmicas para o **propriedades** coleções da não abertos [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) e [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objetos. Um determinado provedor também pode inserir propriedades adicionais quando esses objetos são abertos. Algumas dessas propriedades são listadas na [propriedades dinâmicas do ADO](../../../ado/reference/ado-api/ado-dynamic-properties.md) seção. Mais são listados sob os provedores específicos no [apêndice a: Provedores de](../../../ado/guide/appendixes/appendix-a-providers.md) seção.  
  
 As tabelas a seguir são cross-indexes dos nomes de ADO e OLE DB para cada propriedade dinâmico do provedor OLE DB padrão. Seus provedores podem adicionar mais propriedades do que listados aqui. Para obter informações específicas sobre propriedades dinâmicas específicas do provedor, consulte a documentação do provedor.  
  
 O referência do programador DB OLE se refere a um nome de propriedade ADO usando o termo "Descrição". Para obter mais informações sobre essas propriedades padrão, pesquisar ou procurar o índice na [documentação do OLE DB](https://msdn.microsoft.com/library/windows/desktop/ms722784.aspx)para a propriedade do OLE DB por seu nome.  
  
## <a name="connection-dynamic-properties"></a>Propriedades dinâmicas da Conexão  
  
|Nome da propriedade ADO|Nome da propriedade do OLE DB|  
|-----------------------|--------------------------|  
|Sessões ativas|DBPROP_ACTIVESESSIONS|  
|Anulação Asynchable|DBPROP_ASYNCTXNABORT|  
|Confirmação de Asynchable|DBPROP_ASYNCTNXCOMMIT|  
|Níveis de isolamento de confirmação automática|DBPROP_SESS_AUTOCOMMITISOLEVELS|  
|Local do catálogo|DBPROP_CATALOGLOCATION|  
|Termo do catálogo|DBPROP_CATALOGTERM|  
|Definição de coluna|DBPROP_COLUMNDEFINITION|  
|Connect Timeout|DBPROP_INIT_TIMEOUT|  
|Catálogo atual|DBPROP_CURRENTCATALOG|  
|fonte de dados|DBPROP_INIT_DATASOURCE|  
|Nome da Fonte de Dados|DBPROP_DATASOURCENAME|  
|Objeto de fonte de dados modelo de Threading|DBPROP_DSOTHREADMODEL|  
|Nome do DBMS|DBPROP_DBMSNAME|  
|Versão do DBMS|DBPROP_DBMSVER|  
|Propriedades estendidas|DBPROP_INIT_PROVIDERSTRING|  
|Suporte GROUP BY|DBPROP_GROUPBY|  
|Suporte a tabelas heterogêneas|DBPROP_HETEROGENEOUSTABLES|  
|Maiusculas e minúsculas do identificador|DBPROP_IDENTIFIERCASE|  
|Catálogo Inicial|DBPROP_INIT_CATALOG|  
|Níveis de isolamento|DBPROP_SUPPORTEDTXNISOLEVELS|  
|Retenção de isolamento|DBPROP_SUPPORTEDTXNISORETAIN|  
|Identificador de Localidade|DBPROP_INIT_LCID|  
|Location|DBPROP_INIT_LOCATION|  
|Tamanho máximo de índice|DBPROP_MAXINDEXSIZE|  
|Tamanho máximo da linha|DBPROP_MAXROWSIZE|  
|Tamanho máximo de linha inclui BLOB|DBPROP_MAXROWSIZEINCLUDESBLOB|  
|Máximo de tabelas em SELECT|DBPROP_MAXTABLESINSELECT|  
|Modo|DBPROP_INIT_MODE|  
|Vários conjuntos de parâmetros|DBPROP_MULTIPLEPARAMSETS|  
|Vários resultados|DBPROP_MULTIPLERESULTS|  
|Vários objetos de armazenamento|DBPROP_MULTIPLESTORAGEOBJECTS|  
|Atualização multi-tabela|DBPROP_MULTITABLEUPDATE|  
|Ordem de agrupamento de NULL|DBPROP_NULLCOLLATION|  
|Comportamento de concatenação nulo|DBPROP_CONCATNULLBEHAVIOR|  
|Serviços do OLE DB|DBPROP_INIT_OLEDBSERVICES|  
|Versão do OLE DB|DBPROP_PROVIDEROLEDBVER|  
|Suporte do objeto OLE|DBPROP_OLEOBJECTS|  
|Suporte de conjunto de linhas aberto|DBPROP_OPENROWSETSUPPORT|  
|Colunas ORDER BY na lista de seleção|DBPROP_ORDERBYCOLUMNSINSELECT|  
|Disponibilidade do parâmetro de saída|DBPROP_OUTPUTPARAMETERAVAILABILITY|  
|Acessadores passe por referência|DBPROP_BYREFACCESSORS|  
|Senha|DBPROP_AUTH_PASSWORD|  
|Informações de Persistência de Segurança|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|  
|Tipo de ID persistente|DBPROP_PERSISTENTIDTYPE|  
|Preparar comportamento do abortar|DBPROP_PREPAREABORTBEHAVIOR|  
|Preparar comportamento da confirmação|DBPROP_PREPARECOMMITBEHAVIOR|  
|Termo de procedimento|DBPROP_PROCEDURETERM|  
|Aviso|DBPROP_INIT_PROMPT|  
|Nome amigável do provedor|DBPROP_PROVIDERFRIENDLYNAME|  
|Nome do Provedor|DBPROP_PROVIDERFILENAME|  
|Versão do provedor|DBPROP_PROVIDERVER|  
|Fonte de dados somente leitura|DBPROP_DATASOURCEREADONLY|  
|Conversões de conjunto de linhas no comando|DBPROP_ROWSETCONVERSIONSONCOMMAND|  
|Termo do esquema|DBPROP_SCHEMATERM|  
|Uso do esquema|DBPROP_SCHEMAUSAGE|  
|Suporte do SQL|DBPROP_SQLSUPPORT|  
|Armazenamento estruturado|DBPROP_STRUCTUREDSTORAGE|  
|Suporte subconsulta|DBPROP_SUBQUERIES|  
|Termo de tabela|DBPROP_TABLETERM|  
|Transação DDL|DBPROP_SUPPORTEDTXNDDL|  
|ID de usuário|DBPROP_AUTH_USERID|  
|Nome do Usuário|DBPROP_USERNAME|  
|Identificador de janela|DBPROP_INIT_HWND|  
  
## <a name="recordset-dynamic-properties"></a>Propriedades dinâmicas do conjunto de registros  
 Observe que o **propriedades dinâmicas** da **conjunto de registros** objeto vá fora do escopo (indisponível) quando o **Recordset** está fechado.  
  
|Nome da propriedade ADO|Nome da propriedade do OLE DB|  
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
|Conjunto de linhas somente de acréscimo|DBPROP_APPENDONLY|  
|Processamento assíncrono de conjunto de linhas|DBPROP_ROWSET_ASYNCH|  
|Recálculo automático|DBPROP_ADC_AUTORECALC|  
|Tamanho da busca em segundo plano|DBPROP_ASYNCHFETCHSIZE|  
|Prioridade de Thread de Segundo Plano|DBPROP_ASYNCHTHREADPRIORITY|  
|Tamanho do lote|DBPROP_ADC_BATCHSIZE|  
|Bloquear objetos de armazenamento|DBPROP_BLOCKINGSTORAGEOBJECTS|  
|Tipo de indicador|DBPROP_BOOKMARKTYPE|  
|Possíveis de indicação|DBPROP_IROWSETLOCATE|  
|Marcadores ordenados|DBPROP_ORDEREDBOOKMARKS|  
|Armazenar em cache linhas filho|DBPROP_ADC_CACHECHILDROWS|  
|Armazenar em cache colunas adiadas|DBPROP_CACHEDEFERRED|  
|Modificar linhas inseridas|DBPROP_CHANGEINSERTEDROWS|  
|Privilégios de coluna|DBPROP_COLUMNRESTRICT|  
|Notificação de conjunto de coluna|DBPROP_NOTIFYCOLUMNSET|  
|Coluna gravável|DBPROP_MAYWRITECOLUMN|  
|Tempo limite de comando|DBPROP_COMMANDTIMEOUT|  
|Versão do mecanismo de cursor|DBPROP_ADC_CEVER|  
|Adiar a coluna|DBPROP_DEFERRED|  
|Atualizações de objetos de armazenamento de atraso|DBPROP_DELAYSTORAGEOBJECTS|  
|Buscar na ordem inversa|DBPROP_CANFETCHBACKWARDS|  
|Operações do filtro|DBPROP_FILTERCOMPAREOPS|  
|As operações de localização|DBPROP_FINDCOMPAREOPS|  
|Colunas ocultas (contagem)|DBPROP_HIDDENCOLUMNS|  
|Manter linhas|DBPROP_CANHOLDROWS|  
|Linhas imóveis|DBPROP_IMMOBILEROWS|  
|Tamanho da busca inicial|DBPROP_ASYNCHPREFETCHSIZE|  
|Marcadores literais|DBPROP_LITERALBOOKMARKS|  
|Identidade de linha literal|DBPROP_LITERALIDENTITY|  
|Manter o Status de alteração|DBPROP_ADC_MAINTAINCHANGESTATUS|  
|Máximo de linhas abertas|DBPROP_MAXOPENROWS|  
|Máximo de linhas pendentes|DBPROP_MAXPENDINGROWS|  
|Máximo de linhas|DBPROP_MAXROWS|  
|Uso de Memória|DBPROP_MEMORYUSAGE|  
|Granularidade de notificação|DBPROP_NOTIFICATIONGRANULARITY|  
|Fases de notificação|DBPROP_NOTIFICATIONPHASES|  
|Objetos transacionados|DBPROP_TRANSACTEDOBJECT|  
|Alterações de outros visíveis|DBPROP_OTHERUPDATEDELETE|  
|Inserções de outros visíveis|DBPROP_OTHERINSERT|  
|Modificações próprias visíveis|DBPROP_OWNUPDATEDELETE|  
|Indicações próprias visíveis|DBPROP_OWNINSERT|  
|Preservar no abortar|DBPROP_ABORTPRESERVE|  
|Preservar na confirmação|DBPROP_COMMITPRESERVE|  
|Private1||  
|Reinicialização rápida|DBPROP_QUICKRESTART|  
|Eventos reentrantes|DBPROP_REENTRANTEVENTS|  
|Remover linhas excluídas|DBPROP_REMOVEDELETED|  
|Reportar múltiplas mudanças|DBPROP_REPORTMULTIPLECHANGES|  
|Alterar a forma de nome|DBPROP_ADC_RESHAPENAME|  
|Comando de ressincronização|DBPROP_ADC_CUSTOMRESYNCH|  
|Retorna inserções pendentes|DBPROP_RETURNPENDINGINSERTS|  
|Notificação de exclusão da linha|DBPROP_NOTIFYROWDELETE|  
|Primeira notificação de alteração de linha|DBPROP_NOTIFYROWFIRSTCHANGE|  
|Notificação de inserção de linha|DBPROP_NOTIFYROWINSERT|  
|Privilégios de linhas|DBPROP_ROWRESTRICT|  
|Notificação de ressincronização de linha|DBPROP_NOTIFYROWRESYNCH|  
|Modelo de Threading de linha|DBPROP_ROWTHREADMODEL|  
|Notificação de alteração de desfazer de linha|DBPROP_NOTIFYROWUNDOCHANGE|  
|Notificação de desfazer deleção de linha|DBPROP_NOTIFYROWUNDODELETE|  
|Notificação desfazer inserção de linha|DBPROP_NOTIFYROWUNDOINSERT|  
|Notificação de atualização de linha|DBPROP_NOTIFYROWUPDATE|  
|Notificação de alteração de posição de busca do conjunto de linhas|DBPROP_NOTIFYROWSETFETCHPOSITIONCHANGE|  
|Notificação de liberação de conjunto de linhas|DBPROP_NOTIFYROWSETRELEASE|  
|Rolar na ordem inversa|DBPROP_CANSCROLLBACKWARDS|  
|Cursor de servidor|DBPROP_SERVERCURSOR|  
|Ignorar marcadores apagados|DBPROP_BOOKMARKSKIPPED|  
|Identidade de linha forte|DBPROP_STRONGIDENTITY|  
|Catálogo exclusivo|DBPROP_ADC_UNIQUECATALOG|  
|Linhas exclusivas|DBPROP_UNIQUEROWS|  
|Esquema exclusivo|DBPROP_ADC_UNIQUESCHEMA|  
|Tabela única|DBPROP_ADC_UNIQUETABLE|  
|Capacidade de atualização|DBPROP_UPDATABILITY|  
|Critérios de atualização|DBPROP_ADC_UPDATECRITERIA|  
|Ressincronização de atualização|DBPROP_ADC_UPDATERESYNC|  
|Usar indicadores|DBPROP_BOOKMARKS|
