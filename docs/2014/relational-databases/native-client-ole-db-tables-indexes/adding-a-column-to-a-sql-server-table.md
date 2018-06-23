---
title: Adicionar uma coluna a uma tabela do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- columns [OLE DB]
- AddColumn function
- SQL Server Native Client OLE DB provider, columns
- adding columns
ms.assetid: 22bae18a-bc9d-4617-8660-ed8b17a468d4
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 45909b981b21a496411b46200aceeaded0a9af47
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008884"
---
# <a name="adding-a-column-to-a-sql-server-table"></a>Adicionando uma coluna a uma tabela do SQL Server
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client expõe a **itabledefinition:: addColumn** função. Isso permite aos consumidores adicionar uma coluna para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela.  
  
 Quando você adiciona uma coluna para uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor do provedor OLE DB Native Client é restringido da seguinte forma:  
  
-   Caso DBPROP_COL_AUTOINCREMENT seja VARIANT_TRUE, DBPROP_COL_NULLABLE deve ser VARIANT_FALSE.  
  
-   Se a coluna é definida usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **timestamp** tipo de dados, DBPROP_COL_NULLABLE deve ser VARIANT_FALSE.  
  
-   Para qualquer outra definição de coluna, DBPROP_COL_NULLABLE deve ser VARIANT_TRUE.  
  
 Os consumidores especificam o nome da tabela como uma cadeia de caracteres Unicode no *pwszName* membro do *uName* união no *pTableID* parâmetro. O *eKind* membro *pTableID* deve ser DBKIND_NAME.  
  
 O nome da nova coluna é especificado como uma cadeia de caracteres Unicode no *pwszName* membro do *uName* união no *dbcid* membro do parâmetro DBCOLUMNDESC *pColumnDesc*. O *eKind* membro deve ser DBKIND_NAME.  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas e índices](tables-and-indexes.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)  
  
  
