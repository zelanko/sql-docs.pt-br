---
description: Caixa de diálogo Parâmetros da Consulta (Visual Database Tools)
title: Caixa de diálogo Parâmetros de Consulta
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:69645
- vdt.dlgbox.definequeryparameters
ms.assetid: 31cdaee2-d7cd-4d64-a45f-924b27e8b1f0
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: ea62b4a278ca2f6b6c272f404d8446973fa51680
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88313952"
---
# <a name="query-parameters-dialog-box-visual-database-tools"></a>Caixa de diálogo Parâmetros da Consulta (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Essa caixa de diálogo permite digitar valores para os parâmetros definidos na consulta. Ela é exibida quando uma consulta contendo parâmetros que exigeem entradas de usuário final em tempo de execução é executada.  
  
## <a name="options"></a>Opções  
**Nome**  
Lista os parâmetros definidos para a consulta em execução. Se a consulta contiver parâmetros nomeados, os nomes aparecerão na lista. Se a consulta contiver parâmetros sem-nome, os nomes de parâmetro definidos pelo sistema serão listados para todos os parâmetros da consulta.  
  
**Valor**  
Digite o valor de cada parâmetro listado em **Nome**. O valor usado mais recentemente aparecerá como valor de parâmetro padrão.  
  
## <a name="example"></a>Exemplo  
A consulta a seguir, do Painel SQL, abre a caixa de diálogo Parâmetros da Consulta quando executada no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
```  
SELECT   FirstName, LastName  
FROM    Person.Person AS Lastname  
WHERE   (LastName = @Param1);  
```  
  
## <a name="see-also"></a>Consulte Também  
[Consultar com parâmetros &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-parameters-visual-database-tools.md)  
  
