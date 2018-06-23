---
title: 'Tutorial: usando o tipo de dados hierarchyid | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- tutorials [hierarchyid]
- hierarchyid [Database Engine], tutorial
ms.assetid: 5a7f7cfd-7faf-439f-8085-8fd6bf7db355
caps.latest.revision: 15
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: a3d380b0ad7eb1fb6120d959e3b7fb303466c010
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36121221"
---
# <a name="tutorial-using-the-hierarchyid-data-type"></a>Tutorial: Usando o tipo de dados hierarchyid
  Este tutorial é destinado a usuários com experiência em [!INCLUDE[tsql](../../includes/tsql-md.md)], mas principiantes em tipo de dados `hierarchyid`.  
  
## <a name="what-you-will-learn"></a>O que você aprenderá  
 Este tutorial é dividido em duas lições:  
  
 [Lição 1: convertendo uma tabela em uma estrutura hierárquica](lesson-1-converting-a-table-to-a-hierarchical-structure.md)  
 Nesta lição, você usa uma tabela de funcionário existente, que foi estruturada como hierarquia pai/filho, e move os dados para uma tabela nova que represente a hierarquia, usando o tipo de dados `hierarchyid`. Esta lição exige o banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
 [Lição 2: criando e gerenciando dados em uma tabela hierárquica](lesson-2-creating-and-managing-data-in-a-hierarchical-table.md)  
 Nesta lição, você cria uma tabela usando o tipo de dados `hierarchyid` para representar a estrutura da hierarquia. Em seguida, você manipula os dados da tabela usando os métodos hierárquicos.  
  
## <a name="requirements"></a>Requisitos  
 O sistema deverá ter o seguinte instalado:  
  
-   Qualquer edição do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou posterior.  
  
-   O [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] Express.  
  
-   Internet Explorer 6 ou versão posterior.  
  
## <a name="see-also"></a>Consulte também  
 [Tutorial: Introdução ao mecanismo de banco de dados](../tutorial-getting-started-with-the-database-engine.md)   
 [Tutorial: Gravando instruções Transact-SQL](../../t-sql/tutorial-writing-transact-sql-statements.md)   
 [Referência de método de tipo de dados hierarchyid](/sql/t-sql/data-types/hierarchyid-data-type-method-reference)   
 [Dados hierárquicos &#40;do SQL Server&#41;](../hierarchical-data-sql-server.md)   
 [hierarchyid &#40;Transact-SQL&#41;](/sql/t-sql/data-types/hierarchyid-data-type-method-reference)  
  
  
