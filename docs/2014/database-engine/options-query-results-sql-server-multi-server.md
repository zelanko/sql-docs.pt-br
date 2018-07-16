---
title: Opções (consulta resultados SQL Server-Multi-Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.sqleditors.multiserverresultssettings
- VS.ToolsOptionsPages.QueryResults.SqlServer.SQLMultiServerResults
ms.assetid: d6768bd8-9cb5-4606-a726-a33a1df9e1bb
caps.latest.revision: 9
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: c3088e2e265ef44a7d490001b9a7060186ba2c3c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37271792"
---
# <a name="options-query-results-sql-server-multi-server"></a>Opções (consulta resultados SQL Server-Multi-Server)
  Ao consultar vários servidores ao mesmo tempo, use esta página para especificar as opções de exibição de um conjunto de resultados. A mesclagem de resultados combina os conjuntos de resultados de todos os servidores em um único conjunto de resultados. Ao mesclar resultados, o primeiro servidor que responde define o esquema para o conjunto de resultados. Para mesclar os conjuntos de resultados, a consulta deve retornar o mesmo número de colunas, com os mesmos nomes de colunas de cada servidor. Ao mesclar resultados, uma mensagem é exibida para cada servidor que não corresponde ao esquema (contagem e nomes de colunas) que é retornado pelo primeiro servidor que retorna resultados.  
  
 Se você não mesclar resultados, o conjunto de resultados de cada servidor será exibido em sua própria grade com seu próprio esquema.  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 **Mesclar resultados**  
 Selecione esta caixa de seleção para combinar os conjuntos de resultados de vários servidores na mesma grade.  
  
 **Adicione o nome do servidor aos resultados**  
 Selecione esta caixa de seleção para incluir uma coluna adicional que indica o nome do servidor que gerou cada linha.  
  
 **Adicionar nome de logon aos resultados**  
 Selecione esta caixa de seleção para incluir uma coluna adicional que indica o logon usado para conectar-se ao servidor que gerou cada linha.  
  
## <a name="see-also"></a>Consulte também  
 [Criar um servidor de gerenciamento Central e grupo de servidores &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-a-central-management-server-and-server-group.md)   
 [Executar instruções em vários servidores simultaneamente &#40;SQL Server Management Studio&#41;](../ssms/register-servers/execute-statements-against-multiple-servers-simultaneously.md)  
  
  
