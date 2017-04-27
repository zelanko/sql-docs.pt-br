---
title: "Caixa de diálogo Parâmetros da Consulta (Visual Database Tools) | Microsoft Docs"
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
- vdtsql.chm:69645
- vdt.dlgbox.definequeryparameters
ms.assetid: 31cdaee2-d7cd-4d64-a45f-924b27e8b1f0
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: fbf5a6857226aee3b091aa63ac8fe7868c55c68d
ms.lasthandoff: 04/11/2017

---
# <a name="query-parameters-dialog-box-visual-database-tools"></a>Caixa de diálogo Parâmetros da Consulta (Visual Database Tools)
Essa caixa de diálogo permite digitar valores para os parâmetros definidos na consulta. Ela é exibida quando uma consulta contendo parâmetros que exigeem entradas de usuário final em tempo de execução é executada.  
  
## <a name="options"></a>Opções  
**Nome**  
Lista os parâmetros definidos para a consulta em execução. Se a consulta contiver parâmetros nomeados, os nomes aparecerão na lista. Se a consulta contiver parâmetros sem-nome, os nomes de parâmetro definidos pelo sistema serão listados para todos os parâmetros da consulta.  
  
**Value**  
Digite o valor de cada parâmetro listado em **Nome**. O valor usado mais recentemente aparecerá como valor de parâmetro padrão.  
  
## <a name="example"></a>Exemplo  
A consulta a seguir, do Painel SQL, abre a caixa de diálogo Parâmetros da Consulta quando executada no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject_md.md)] .  
  
```  
SELECT   FirstName, LastName  
FROM    Person.Person AS Lastname  
WHERE   (LastName = @Param1);  
```  
  
## <a name="see-also"></a>Consulte também  
[Consultar com parâmetros &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/query-with-parameters-visual-database-tools.md)  
  

