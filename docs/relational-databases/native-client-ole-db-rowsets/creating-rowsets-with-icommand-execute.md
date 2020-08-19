---
description: 'Criar conjunto de linhas com ICommand:: Execute (provedor de OLE DB de cliente nativo)'
title: 'Criar conjunto de linhas com ICommand:: Execute (provedor de OLE DB de cliente nativo) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- rowsets [OLE DB], creating
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, creating
- Execute method
ms.assetid: 9b530b7d-8165-49d4-a978-5ced17c6705e
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bfb523c7a22c59d85f16821b2e3f5fbc1b6a1229
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428228"
---
# <a name="creating-rowsets-with-icommandexecute-in-sql-server-native-client"></a>Criando conjuntos de linhas com ICommand:: execute no SQL Server Native Client
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Para conjuntos de linhas criados usando o método **ICommand::Execute**, as propriedades que você deseja obter no conjunto de linhas resultante podem restringir o texto do comando. Isto é especialmente crítico para consumidores que dão suporte a texto de comando dinâmico.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo não pode usar [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cursores para dar suporte aos resultados de vários conjuntos de linhas gerados por muitos comandos. Se um consumidor solicitar um conjunto de linhas que exigir suporte de cursor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ocorrerá um erro se o texto do comando gerar mais de um só conjunto de linhas como seu resultado. Confira mais informações em [Comandos que geram resultados de vários conjuntos de linhas](../../relational-databases/native-client-ole-db-commands/commands-generating-multiple-rowset-results.md).  
  
 Os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjuntos de linhas do provedor de OLE DB de cliente nativo rolável são suportados pelos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cursores. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] indica limitações sobre cursores que são sensíveis às alterações feitas por outros usuários do banco de dados. Especificamente, as linhas em alguns cursores não podem ser ordenadas e a tentativa de criar um conjunto de linhas usando um comando que contenha uma cláusula SQL ORDER BY pode falhar. Para obter mais informações, confira [Conjuntos de linha e cursores do SQL Server](../../relational-databases/native-client-ole-db-rowsets/rowsets-and-sql-server-cursors.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Conjuntos de linhas](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
