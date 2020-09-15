---
description: Verificar consultas (Visual Database Tools)
title: Verificar consultas
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:100644
helpviewer_keywords:
- verifying queries
- queries [SQL Server], verifying
- checking queries
ms.assetid: 1382c0c0-46dc-45f9-ab38-9bba1d347eea
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 944d34dbbec6da87d4f3ebd7920d9acd2ad162c4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88417722"
---
# <a name="verify-queries-visual-database-tools"></a>Verificar consultas (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Para evitar problemas, você pode verificar a consulta compilada para garantir que a sintaxe está correta. Essa opção é especialmente útil quando você digita instruções no [Painel SQL](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md).  
  
Algumas observações a serem consideradas sobre verificação de consultas:  
  
-   Uma instrução poderá ser válida e, portanto, ser verificada com êxito, mesmo se não puder ser representada no **Painel de Diagrama** e no **Painel Critérios**.  
  
-   A verificação SQL pode detectar alguns, mas não todos os erros SQL. Se uma consulta contiver um erro não detectado durante a verificação SQL, o banco de dados detectará o erro quando você executar a consulta.  
  
-   Consultas que contêm parâmetros não podem ser verificadas.  
  
### <a name="to-verify-an-sql-statement"></a>Para verificar uma instrução SQL  
  
-   Clique com o botão direito do mouse no **Painel SQL**e selecione **Verificar Sintaxe SQL** no menu de atalho.  
  
## <a name="see-also"></a>Consulte Também  
[Executar consultas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/run-queries-visual-database-tools.md)  
[Executar operações básicas com consultas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
