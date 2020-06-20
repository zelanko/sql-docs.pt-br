---
title: OLE DB
description: O provedor de OLE DB SQL Server Native Client é uma API COM para acessar dados, usada para ferramentas, utilitários ou componentes de nível baixo que precisam de alto desempenho.
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, about SQL Server Native Client OLE DB provider
- OLE DB, SQL Server Native Client OLE DB provider
- data access [SQL Server Native Client], OLE DB
- SQLNCLI, OLE DB
- OLE DB
- SQL Server Native Client OLE DB provider
- SQL Server Native Client, OLE DB
ms.assetid: da846da4-ec19-4a4f-81fb-7d5a2b2bf80a
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a5f945ca5abaa515823ea81ad30ca4292cc42690
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84948649"
---
# <a name="sql-server-native-client-ole-db"></a>SQL Server Native Client (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo (sqlncli) é uma API com de baixo nível que é usada para acessar dados. O provedor OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client é recomendado para desenvolver ferramentas, utilitários ou componentes de baixo nível que precisem de alto desempenho. O provedor OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client é um provedor nativo de alto desempenho que acessa o protocolo TDS do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] diretamente.  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client fornece suporte de OLE DB a aplicativos que se conectam ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo é um provedor compatível com OLE DB versão 2,0.  
 
> [!IMPORTANT]
> O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB de cliente nativo (sqlncli) permanece preterido e não é recomendável usá-lo para novos trabalhos de desenvolvimento. Em vez disso, use o novo [Driver do Microsoft OLE DB para SQL Server](../../../connect/oledb/oledb-driver-for-sql-server.md) (MSOLEDBSQL), que será atualizado com os recursos de servidor mais recentes.
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Criando um aplicativo provedor OLE DB do SQL Server Native Client](../../../relational-databases/native-client-ole-db-provider/creating-a-sql-server-native-client-ole-db-provider-application.md)  
  
-   [Objetos de fonte de dados &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
-   [Comandos](../../../relational-databases/native-client-ole-db-commands/commands.md)  
  
-   [Conjuntos de linhas](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
-   [Procedimentos armazenados](../../../relational-databases/native-client/ole-db/stored-procedures.md)  
  
-   [BLOBs e objetos OLE](../../../relational-databases/native-client-ole-db-blobs/blobs-and-ole-objects.md)  
  
-   [Tabelas e índices](../../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)  
  
-   [Tipos de dados &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-data-types/data-types-ole-db.md)  
  
-   [Suporte ao conjunto de linhas de esquema &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/schema-rowset-support-ole-db.md)  
  
-   [Parâmetros com valor de tabela &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)  
  
-   [Melhorias de data e hora &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
-   [Tipos CLR grandes definidos pelo usuário &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/large-clr-user-defined-types-ole-db.md)  
  
-   [Suporte a FILESTREAM &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/filestream-support-ole-db.md)  
  
-   [Transações](../../../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
-   [Erros](../../../relational-databases/native-client-ole-db-errors/errors.md)  
  
-   [SPNs &#40;Nomes da Entidade de Serviço&#41; em conexões de cliente &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/service-principal-names-spns-in-client-connections-ole-db.md)  
  
-   [Suporte a colunas esparsas &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/sparse-columns-support-ole-db.md)  
  
-   [SQL Server Native Client &#40;OLE DB referência de&#41;](../../../relational-databases/native-client-ole-db-interfaces/sql-server-native-client-ole-db-interfaces.md)  
  
-   [Tópicos de instruções do OLE DB](../../../relational-databases/native-client-ole-db-how-to/ole-db-how-to-topics.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Programação do SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
