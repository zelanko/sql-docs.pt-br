---
title: Verificar consultas (Visual Database Tools) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vdtsql.chm:100644
helpviewer_keywords:
- verifying queries
- queries [SQL Server], verifying
- checking queries
ms.assetid: 1382c0c0-46dc-45f9-ab38-9bba1d347eea
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e2aa0172a18bb1b01297caa9dcf4db07888ce083
ms.contentlocale: pt-br
ms.lasthandoff: 08/18/2017

---
# <a name="verify-queries-visual-database-tools"></a>Verificar consultas (Visual Database Tools)
Para evitar problemas, você pode verificar a consulta compilada para garantir que a sintaxe está correta. Essa opção é especialmente útil quando você digita instruções no [Painel SQL](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md).  
  
Algumas observações a serem consideradas sobre verificação de consultas:  
  
-   Uma instrução poderá ser válida e, portanto, ser verificada com êxito, mesmo se não puder ser representada no **Painel de Diagrama** e no **Painel Critérios**.  
  
-   A verificação SQL pode detectar alguns, mas não todos os erros SQL. Se uma consulta contiver um erro não detectado durante a verificação SQL, o banco de dados detectará o erro quando você executar a consulta.  
  
-   Consultas que contêm parâmetros não podem ser verificadas.  
  
### <a name="to-verify-an-sql-statement"></a>Para verificar uma instrução SQL  
  
-   Clique com o botão direito do mouse no **Painel SQL**e selecione **Verificar Sintaxe SQL** no menu de atalho.  
  
## <a name="see-also"></a>Consulte também  
[Executar consultas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/run-queries-visual-database-tools.md)  
[Executar operações básicas com consultas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  

