---
title: Caixa de diálogo Parâmetros da Consulta (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
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
ms.openlocfilehash: f1f530954b2449e3a85822ad04d87cd553ae26a9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47674164"
---
# <a name="query-parameters-dialog-box-visual-database-tools"></a>Caixa de diálogo Parâmetros da Consulta (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Essa caixa de diálogo permite digitar valores para os parâmetros definidos na consulta. Ela é exibida quando uma consulta contendo parâmetros que exigeem entradas de usuário final em tempo de execução é executada.  
  
## <a name="options"></a>Opções  
**Nome**  
Lista os parâmetros definidos para a consulta em execução. Se a consulta contiver parâmetros nomeados, os nomes aparecerão na lista. Se a consulta contiver parâmetros sem-nome, os nomes de parâmetro definidos pelo sistema serão listados para todos os parâmetros da consulta.  
  
**Value**  
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
  
