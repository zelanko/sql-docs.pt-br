---
title: Recursos modificados (banco de dados independente) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: databases
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- contained database, modifications to DBs
ms.assetid: a2942509-39a2-4903-b504-ae80a300a9de
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 126f826de61c9f4d53abab3d8977cbec71d8e75a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="modified-features-contained-database"></a>Recursos modificados (banco de dados independente)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Os recursos a seguir foram modificados para serem suportados por um banco de dados independente parcialmente. Normalmente, eles são modificados para que não ultrapassem o limite de banco de dados.  
  
 Para obter mais informações, veja [Bancos de dados independentes](../../relational-databases/databases/contained-databases.md).  
  
## <a name="alter-database"></a>ALTER DATABASE  
  
### <a name="application-level"></a>Nível de aplicativo  
 Ao usar a instrução ALTER DATABASE de dentro de um banco de dados independente, a sintaxe irá diferir da que é usada para um banco de dados dependente. Essa diferença inclui restrições de elementos da instrução que se estendem além do banco de dados para a instância. Para obter mais informações, veja [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
### <a name="instance-level"></a>Nível de instância  
 A sintaxe para a instrução ALTER DATABASE, quando usada fora de um banco de dados independente, irá diferir da que é usada para bancos de dados dependentes. Estas alterações impedem o cruzamento do limite de banco de dados. Para obter mais informações, veja [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
## <a name="create-database"></a>CREATE DATABASE  
 A sintaxe CREATE DATABASE para um banco de dados independente difere da que é usada em um banco de dados dependente. Veja [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md) para obter informações sobre novos requisitos de sintaxe e concessões.  
  
## <a name="temporary-tables"></a>Tabelas temporárias  
 São permitidas tabelas temporárias locais dentro de um banco de dados independente, mas o comportamento delas difere das usadas em bancos de dados dependentes. Em bancos de dados dependentes, os dados de tabelas temporárias são agrupados no agrupamento de **tempdb**. Em um banco de dados independente, os dados de tabelas temporárias são agrupados no agrupamento do banco de dados independente.  
  
 Todo os metadados associados a tabelas temporárias (por exemplo, nomes de tabelas e de colunas, índices, etc.) estarão no agrupamento de catálogo.  
  
 Podem não ser usadas restrições nomeadas em tabelas temporárias.  
  
 Tabelas temporárias podem não recorrer a tipos definidos pelo usuário, coleções de esquemas XML ou funções definidas pelo usuário.  
  
## <a name="collation"></a>Agrupamento  
 No modelo de banco de dados dependente, há três tipos separados de agrupamento: agrupamento de Banco de Dados, agrupamento de Instância e agrupamento de tempdb. Bancos de dados independentes usam apenas dois agrupamentos, agrupamento de banco de dados e o novo agrupamento de catálogo. Veja [Agrupamentos de banco de dados independentes](../../relational-databases/databases/contained-database-collations.md) para obter mais detalhes sobre o agrupamento de banco de dados independente.  
  
## <a name="user-options"></a>Opções de usuário  
 Ao habilitar bancos de dados independentes, é preciso definir a [Opção user options](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md) como 0 para a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [Agrupamentos de banco de dados independentes](../../relational-databases/databases/contained-database-collations.md)   
 [Bancos de dados independentes](../../relational-databases/databases/contained-databases.md)  
  
  
