---
title: Índice de propriedade dinâmica de ADO | Microsoft Docs
ms.prod: sql
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- dynamic properties [ADO], index
ms.assetid: 80d389dd-46ef-459f-b0d4-6f712fc4f32d
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3d646865c5fc95ed032c0cc21e973a3204162201
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="ado-dynamic-property-index"></a>Índice de propriedade dinâmica de ADO
Provedores de dados, provedores de serviços e componentes de serviços podem adicionar propriedades dinâmicas para o **propriedades** coleções de não o aberta [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) e [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objetos. Um determinado provedor também pode inserir propriedades adicionais quando esses objetos são abertos. Algumas dessas propriedades são listadas no [propriedades dinâmicas do ADO](../../../ado/reference/ado-api/ado-dynamic-properties.md) seção. Mais são listados na provedores específicos no [apêndice a: provedores](../../../ado/guide/appendixes/appendix-a-providers.md) seção.  
  
 As tabelas a seguir são cross-indexes dos nomes de ADO e OLE DB para cada propriedade de dinâmico do provedor OLE DB padrão. Seus provedores podem adicionar mais propriedades do que listados aqui. Para obter informações específicas sobre as propriedades dinâmicas específicos do provedor, consulte a documentação do provedor.  
  
 O referência do programador DB OLE refere-se a um nome de propriedade ADO, o termo "Descrição". Para obter mais informações sobre essas propriedades padrão, pesquisar ou procurar o índice de [documentação de OLE DB](https://msdn.microsoft.com/library/windows/desktop/ms722784.aspx)para a propriedade do OLE DB por seu nome.  
  
## <a name="connection-dynamic-properties"></a>Propriedades de Conexão dinâmica  
  
|Nome da propriedade ADO|Nome de propriedade do OLE DB|  
|-----------------------|--------------------------|  
|Sessões ativas|DBPROP_ACTIVESESSIONS|  
|Anulação de Asynchable|DBPROP_ASYNCTXNABORT|  
|Confirmação Asynchable|DBPROP_ASYNCTNXCOMMIT|  
|Níveis de isolamento de confirmação automática|DBPROP_SESS_AUTOCOMMITISOLEVELS|  
|Local do catálogo|DBPROP_CATALOGLOCATION|  
|Termo do catálogo|DBPROP_CATALOGTERM|  
|Definição de coluna|DBPROP_COLUMNDEFINITION|  
|Connect Timeout|DBPROP_INIT_TIMEOUT|  
|Catálogo atual|DBPROP_CURRENTCATALOG|  
|Fonte de dados|DBPROP_INIT_DATASOURCE|  
|Nome da Fonte de Dados|DBPROP_DATASOURCENAME|  
|Modelo de Threading do objeto de fonte de dados|DBPROP_DSOTHREADMODEL|  
|Nome do DBMS|DBPROP_DBMSNAME|  
|Versão do DBMS|DBPROP_DBMSVER|  
|Propriedades estendidas|DBPROP_INIT_PROVIDERSTRING|  
|GRUPO de suporte|DBPROP_GROUPBY|  
|Suporte a tabelas heterogêneos|DBPROP_HETEROGENEOUSTABLES|  
|Diferenciação de maiusculas e minúsculas identificador|DBPROP_IDENTIFIERCASE|  
|Catálogo Inicial|DBPROP_INIT_CATALOG|  
|Níveis de isolamento|DBPROP_SUPPORTEDTXNISOLEVELS|  
|Retenção de isolamento|DBPROP_SUPPORTEDTXNISORETAIN|  
|Identificador de Localidade|DBPROP_INIT_LCID|  
|Local|DBPROP_INIT_LOCATION|  
|Tamanho máximo de índice|DBPROP_MAXINDEXSIZE|  
|Tamanho máximo da linha|DBPROP_MAXROWSIZE|  
|Tamanho máximo de linha inclui BLOB|DBPROP_MAXROWSIZEINCLUDESBLOB|  
|Máximo de tabelas em SELECT|DBPROP_MAXTABLESINSELECT|  
|Modo|DBPROP_INIT_MODE|  
|Vários conjuntos de parâmetros|DBPROP_MULTIPLEPARAMSETS|  
|Vários resultados|DBPROP_MULTIPLERESULTS|  
|Vários objetos de armazenamento|DBPROP_MULTIPLESTORAGEOBJECTS|  
|Atualização de várias tabela|DBPROP_MULTITABLEUPDATE|  
|Ordem de agrupamento NULL|DBPROP_NULLCOLLATION|  
|Comportamento de concatenação de nulos|DBPROP_CONCATNULLBEHAVIOR|  
|Serviços do OLE DB|DBPROP_INIT_OLEDBSERVICES|  
|Versão do banco de dados OLE|DBPROP_PROVIDEROLEDBVER|  
|Suporte do objeto OLE|DBPROP_OLEOBJECTS|  
|Suporte de conjunto de linhas aberto|DBPROP_OPENROWSETSUPPORT|  
|Colunas ORDER BY na lista de seleção|DBPROP_ORDERBYCOLUMNSINSELECT|  
|Disponibilidade de parâmetro de saída|DBPROP_OUTPUTPARAMETERAVAILABILITY|  
|Acessadores passe por referência|DBPROP_BYREFACCESSORS|  
|Senha|DBPROP_AUTH_PASSWORD|  
|Informações de Persistência de Segurança|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|  
|ID do tipo|DBPROP_PERSISTENTIDTYPE|  
|Preparar o comportamento de anulação|DBPROP_PREPAREABORTBEHAVIOR|  
|Preparar o comportamento de confirmação|DBPROP_PREPARECOMMITBEHAVIOR|  
|Termo do procedimento|DBPROP_PROCEDURETERM|  
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
|Suporte de subconsulta|DBPROP_SUBQUERIES|  
|Termo de tabela|DBPROP_TABLETERM|  
|Transação de DDL|DBPROP_SUPPORTEDTXNDDL|  
|ID de usuário|DBPROP_AUTH_USERID|  
|Nome do Usuário|DBPROP_USERNAME|  
|Identificador de janela|DBPROP_INIT_HWND|  
  
## <a name="recordset-dynamic-properties"></a>Propriedades do conjunto de registros dinâmicos  
 Observe que o **propriedades dinâmicas** do **registros** objeto vá fora do escopo (indisponível) quando o **registros** está fechado.  
  
|Nome da propriedade ADO|Nome de propriedade do OLE DB|  
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
|Processamento assíncrono do conjunto de linhas|DBPROP_ROWSET_ASYNCH|  
|Recálculo automático|DBPROP_ADC_AUTORECALC|  
|Tamanho da busca em segundo plano|DBPROP_ASYNCHFETCHSIZE|  
|Prioridade de Thread de Segundo Plano|DBPROP_ASYNCHTHREADPRIORITY|  
|Tamanho do lote|DBPROP_ADC_BATCHSIZE|  
|Bloqueio de objetos de armazenamento|DBPROP_BLOCKINGSTORAGEOBJECTS|  
|Tipo de indicador|DBPROP_BOOKMARKTYPE|  
|Bookmarkable|DBPROP_IROWSETLOCATE|  
|Indicadores ordenados|DBPROP_ORDEREDBOOKMARKS|  
|Cache de linhas filho|DBPROP_ADC_CACHECHILDROWS|  
|Cache adiada colunas|DBPROP_CACHEDEFERRED|  
|Alterar as linhas inseridas|DBPROP_CHANGEINSERTEDROWS|  
|Privilégios de coluna|DBPROP_COLUMNRESTRICT|  
|Notificação de conjunto de coluna|DBPROP_NOTIFYCOLUMNSET|  
|Coluna gravável|DBPROP_MAYWRITECOLUMN|  
|Tempo limite de comando|DBPROP_COMMANDTIMEOUT|  
|Versão do mecanismo de cursor|DBPROP_ADC_CEVER|  
|Adiar a coluna|DBPROP_DEFERRED|  
|Atualizações de objetos de armazenamento de atraso|DBPROP_DELAYSTORAGEOBJECTS|  
|Buscar com versões anteriores|DBPROP_CANFETCHBACKWARDS|  
|Operações do filtro|DBPROP_FILTERCOMPAREOPS|  
|As operações de localização|DBPROP_FINDCOMPAREOPS|  
|Colunas ocultas (contagem)|DBPROP_HIDDENCOLUMNS|  
|Manter linhas|DBPROP_CANHOLDROWS|  
|Linhas immobile|DBPROP_IMMOBILEROWS|  
|Tamanho da busca inicial|DBPROP_ASYNCHPREFETCHSIZE|  
|Indicadores literal|DBPROP_LITERALBOOKMARKS|  
|Identidade de linha literal|DBPROP_LITERALIDENTITY|  
|Manter o Status da alteração|DBPROP_ADC_MAINTAINCHANGESTATUS|  
|Máximo de linhas aberto|DBPROP_MAXOPENROWS|  
|Máximo de linhas pendentes|DBPROP_MAXPENDINGROWS|  
|Máximo de linhas|DBPROP_MAXROWS|  
|Uso de Memória|DBPROP_MEMORYUSAGE|  
|Granularidade de notificação|DBPROP_NOTIFICATIONGRANULARITY|  
|Fases de notificação|DBPROP_NOTIFICATIONPHASES|  
|Objetos transacionados|DBPROP_TRANSACTEDOBJECT|  
|Outros alterações visíveis|DBPROP_OTHERUPDATEDELETE|  
|Outros inserções visíveis|DBPROP_OTHERINSERT|  
|Possui alterações visíveis|DBPROP_OWNUPDATEDELETE|  
|Próprias inserções visíveis|DBPROP_OWNINSERT|  
|Preservar a anulação|DBPROP_ABORTPRESERVE|  
|Preservar a confirmação|DBPROP_COMMITPRESERVE|  
|Private1||  
|Reinicialização rápida|DBPROP_QUICKRESTART|  
|Eventos reentrantes|DBPROP_REENTRANTEVENTS|  
|Remover linhas excluídas|DBPROP_REMOVEDELETED|  
|Várias alterações de relatórios|DBPROP_REPORTMULTIPLECHANGES|  
|Alterar a forma de nome|DBPROP_ADC_RESHAPENAME|  
|Sincronizar de comando|DBPROP_ADC_CUSTOMRESYNCH|  
|Retornar inserções pendentes|DBPROP_RETURNPENDINGINSERTS|  
|Notificação de exclusão de linha|DBPROP_NOTIFYROWDELETE|  
|Primeira notificação de alteração de linha|DBPROP_NOTIFYROWFIRSTCHANGE|  
|Notificação de inserção de linha|DBPROP_NOTIFYROWINSERT|  
|Privilégios de linha|DBPROP_ROWRESTRICT|  
|Notificação de ressincronização de linha|DBPROP_NOTIFYROWRESYNCH|  
|Modelo de Threading de linha|DBPROP_ROWTHREADMODEL|  
|Notificação de alteração de desfazer de linha|DBPROP_NOTIFYROWUNDOCHANGE|  
|Notificação de desfazer deleção de linha|DBPROP_NOTIFYROWUNDODELETE|  
|Notificação desfazer inserção de linha|DBPROP_NOTIFYROWUNDOINSERT|  
|Notificação de atualização de linha|DBPROP_NOTIFYROWUPDATE|  
|Notificação de alteração de posição de busca do conjunto de linhas|DBPROP_NOTIFYROWSETFETCHPOSITIONCHANGE|  
|Notificação de versão do conjunto de linhas|DBPROP_NOTIFYROWSETRELEASE|  
|Rolar para trás|DBPROP_CANSCROLLBACKWARDS|  
|Cursor de servidor|DBPROP_SERVERCURSOR|  
|Ignorar excluído indicadores|DBPROP_BOOKMARKSKIPPED|  
|Identidade de linha forte|DBPROP_STRONGIDENTITY|  
|Catálogo exclusivo|DBPROP_ADC_UNIQUECATALOG|  
|Linhas exclusivas|DBPROP_UNIQUEROWS|  
|Esquema exclusivo|DBPROP_ADC_UNIQUESCHEMA|  
|Tabela exclusiva|DBPROP_ADC_UNIQUETABLE|  
|Capacidade de atualização|DBPROP_UPDATABILITY|  
|Critérios de atualização|DBPROP_ADC_UPDATECRITERIA|  
|Ressincronização de atualização|DBPROP_ADC_UPDATERESYNC|  
|Usar indicadores|DBPROP_BOOKMARKS|