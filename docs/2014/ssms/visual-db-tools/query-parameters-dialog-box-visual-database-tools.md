---
title: Caixa de diálogo Parâmetros da Consulta (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:69645
- vdt.dlgbox.definequeryparameters
ms.assetid: 31cdaee2-d7cd-4d64-a45f-924b27e8b1f0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 61707b6ca955ee137cbbc93a6a108dc3930e1b12
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63010695"
---
# <a name="query-parameters-dialog-box-visual-database-tools"></a>Caixa de diálogo Parâmetros da Consulta (Visual Database Tools)
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
 [Consultar com parâmetros &#40;Visual Database Tools&#41;](visual-database-tools.md)  
  
  
