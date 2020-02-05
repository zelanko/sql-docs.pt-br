---
title: 'Tutorial: usando o tipo de dados hierarchyid | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: quickstart
helpviewer_keywords:
- tutorials [hierarchyid]
- hierarchyid [Database Engine], tutorial
ms.assetid: 5a7f7cfd-7faf-439f-8085-8fd6bf7db355
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ae451d86f2490765f3871deca925f4b6348e2304
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68140424"
---
# <a name="tutorial-using-the-hierarchyid-data-type"></a>Tutorial: Usando o tipo de dados hierarchyid
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
Este tutorial se destina a usuários com experiência no [!INCLUDE[tsql](../../includes/tsql-md.md)], mas não familiarizados com o tipo de dados **hierarchyid** .  
  
## <a name="what-you-will-learn"></a>O que você aprenderá  
Este tutorial é dividido em duas lições:  
  
[Lição 1: convertendo uma tabela em uma estrutura hierárquica](../../relational-databases/tables/lesson-1-converting-a-table-to-a-hierarchical-structure.md)  
Nesta lição, você aprenderá a usar uma tabela de funcionário existente que foi estruturada como uma hierarquia pai/filho e move os dados para uma nova tabela que representa a hierarquia, usando o tipo de dados **hierarchyid** . Esta lição exige o banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
[Lição 2: criando e gerenciando dados em uma tabela hierárquica](../../relational-databases/tables/lesson-2-creating-and-managing-data-in-a-hierarchical-table.md)  
Nesta lição, você aprenderá a criar uma tabela usando o tipo de dados **hierarchyid** para representar a estrutura da hierarquia. Em seguida, você manipula os dados da tabela usando os métodos hierárquicos.  
  
## <a name="requirements"></a>Requisitos  
O sistema deverá ter o seguinte instalado:  
  
-   Qualquer edição do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou posterior.  
  
-   O [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] Express.  
  
-   Internet Explorer 6 ou versão posterior.  
  
## <a name="see-also"></a>Consulte Também  
[Tutorial: introdução ao Mecanismo de Banco de Dados](../../relational-databases/tutorial-getting-started-with-the-database-engine.md)  
[Tutorial: Gravando instruções Transact-SQL](../../t-sql/tutorial-writing-transact-sql-statements.md)  
[Referência de método de tipo de dados hierarchyid](https://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[Dados hierárquicos &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)  
  
  
  
