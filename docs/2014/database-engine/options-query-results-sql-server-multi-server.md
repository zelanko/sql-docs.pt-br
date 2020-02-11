---
title: Opções (resultados da consulta-SQL Server-multi-Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.sqleditors.multiserverresultssettings
- VS.ToolsOptionsPages.QueryResults.SqlServer.SQLMultiServerResults
ms.assetid: d6768bd8-9cb5-4606-a726-a33a1df9e1bb
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 6019a328463d27b4495ae0db70e844eb4e05d747
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66089973"
---
# <a name="options-query-results-sql-server-multi-server"></a>Opções (Resultados da Consulta/SQL Server/Multisservidor)
  Ao consultar vários servidores ao mesmo tempo, use esta página para especificar as opções de exibição de um conjunto de resultados. A mesclagem de resultados combina os conjuntos de resultados de todos os servidores em um único conjunto de resultados. Ao mesclar resultados, o primeiro servidor que responde define o esquema para o conjunto de resultados. Para mesclar os conjuntos de resultados, a consulta deve retornar o mesmo número de colunas, com os mesmos nomes de colunas de cada servidor. Ao mesclar resultados, uma mensagem é exibida para cada servidor que não corresponde ao esquema (contagem e nomes de colunas) que é retornado pelo primeiro servidor que retorna resultados.  
  
 Se você não mesclar resultados, o conjunto de resultados de cada servidor será exibido em sua própria grade com seu próprio esquema.  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 **Mesclar resultados**  
 Selecione esta caixa de seleção para combinar os conjuntos de resultados de vários servidores na mesma grade.  
  
 **Adicionar nome do servidor aos resultados**  
 Selecione esta caixa de seleção para incluir uma coluna adicional que indica o nome do servidor que gerou cada linha.  
  
 **Adicionar nome de logon aos resultados**  
 Selecione esta caixa de seleção para incluir uma coluna adicional que indica o logon usado para conectar-se ao servidor que gerou cada linha.  
  
## <a name="see-also"></a>Consulte Também  
 [Criar um servidor de gerenciamento central e um grupo de servidores &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-a-central-management-server-and-server-group.md)   
 [Executar instruções em vários servidores simultaneamente &#40;SQL Server Management Studio&#41;](../ssms/register-servers/execute-statements-against-multiple-servers-simultaneously.md)  
  
  
