---
title: Descartando uma tabela do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- tables [OLE DB]
- deleting tables
- SQL Server Native Client OLE DB provider, tables
- removing tables
- dropping tables
ms.assetid: b6d6c4de-43c6-473e-92aa-34ffddd58cbe
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: dd18658df32c8106432b3a791c1eda2b7edaabf7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120339"
---
# <a name="dropping-a-sql-server-table"></a>Descartando uma tabela do SQL Server
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client expõe a **itabledefinition:: Droptable** função. Isso permite que os consumidores removam uma [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela de banco de dados.  
  
 Os consumidores especificam o nome da tabela como uma cadeia de caracteres Unicode no *pwszName* membro do *uName* união no *pTableID* parâmetro. O *eKind* membro *pTableID* deve ser DBKIND_NAME.  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas e índices](tables-and-indexes.md)  
  
  