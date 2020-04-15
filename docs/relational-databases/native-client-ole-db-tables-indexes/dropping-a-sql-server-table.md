---
title: Descartar uma tabela do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- tables [OLE DB]
- deleting tables
- SQL Server Native Client OLE DB provider, tables
- removing tables
- dropping tables
ms.assetid: b6d6c4de-43c6-473e-92aa-34ffddd58cbe
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b6ae20812f7ebd9815d8cc010d5e2a24e994c75a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81279986"
---
# <a name="dropping-a-sql-server-table"></a>Descartando uma tabela do SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor Native Client OLE DB expõe a função **ITableDefinition::DropTable** para remover uma [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela de um banco de dados.  
  
 Especifique o nome da tabela como uma cadeia de caracteres Unicode no membro *pwszName* da união *uName* no parâmetro *pTableID*. O membro *eKind* de *pTableID* precisa ser DBKIND_NAME.  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas e índices](../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)  
  
  
