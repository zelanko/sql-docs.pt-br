---
title: Fornecer uma consulta de origem (Assistente de Importação e Exportação do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.providesourcequery.f1
ms.assetid: c8cbd07e-b9c3-422f-94b8-d6fc8cf31cf5
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 6da28ac9897681d963325fcaf7712f5ed4d3d88b
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965512"
---
# <a name="provide-a-source-query-sql-server-import-and-export-wizard"></a>Fornecer uma consulta de origem (Assistente de Importação e Exportação do SQL Server)
  Use a página **fornecer uma consulta de origem** para digitar a instrução SQL que irá gerar os dados a serem copiados da fonte de dados para o destino.  
  
 Para obter mais informações sobre este assistente, consulte [Assistente de Importação e Exportação do SQL Server](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Para saber mais sobre as opções de inicialização do assistente, bem como as permissões necessárias para executar o assistente com êxito, consulte [executar o assistente de importação e exportação do SQL Server](start-the-sql-server-import-and-export-wizard.md).  
  
 O objetivo do Assistente de Importação e Exportação do SQL Server é copiar dados de uma origem para um destino. O assistente também pode criar um banco de dados de destino e tabelas de destino para você. No entanto, se for necessário copiar vários bancos de dados ou tabelas, ou outros tipos de objetos de banco de dados, será necessário usar o Assistente para Copiar Banco de Dados. Para obter mais informações, consulte [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Opções  
 **Instrução SQL**  
 Digite uma instrução de consulta para recuperar linhas selecionadas de dados do banco de dados de origem. Por exemplo, a instrução de consulta a seguir recupera **vendedorid**, **SalesQuota**e **SalesYTD** do banco de dados AdventureWorks para pessoas de vendas cujo percentual de Comissão é maior que 1,5%.  
  
```  
SELECT SalesPersonID, SalesQuota, SalesYTD  
FROM Sales.SalesPerson  
WHERE CommissionPct > 0.015  
```  
  
 **Passar**  
 Verifica a sintaxe da instrução SQL na caixa de texto **Instrução SQL**.  
  
> [!NOTE]  
>  Se o tempo necessário para verificar a sintaxe da instrução ultrapassar o valor de tempo limite, que é de 30 segundos, a análise será interrompida e será gerado um erro. Você só conseguirá ir além dessa página do assistente quando a análise for bem-sucedida. Uma solução possível é criar uma exibição de banco de dados com base na consulta e consultar a exibição usando o assistente em vez de inserir o texto da consulta diretamente.  
  
 **Procurar**  
 Selecione um arquivo que contém uma instrução SQL usando a caixa de diálogo **abrir** . A seleção de um arquivo copia o texto do arquivo para a caixa de texto **instrução de consulta** .  
  
  
