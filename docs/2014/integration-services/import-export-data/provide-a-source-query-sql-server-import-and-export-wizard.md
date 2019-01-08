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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7f5c39e5d49c3252cd8aab49299d66d2a2467d95
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52769958"
---
# <a name="provide-a-source-query-sql-server-import-and-export-wizard"></a>Fornecer uma consulta de origem (Assistente de Importação e Exportação do SQL Server)
  Use o **fornecer uma consulta de origem** página digitar a instrução SQL que irá gerar os dados a serem copiadas da fonte de dados para o destino.  
  
 Para obter mais informações sobre este assistente, consulte [Assistente de Importação e Exportação do SQL Server](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Para saber mais sobre as opções para iniciar o assistente, bem como as permissões necessárias para executar o assistente com êxito, consulte [executar o Assistente de exportação e importação do SQL Server](start-the-sql-server-import-and-export-wizard.md).  
  
 O objetivo do Assistente de Importação e Exportação do SQL Server é copiar dados de uma origem para um destino. O assistente também pode criar um banco de dados de destino e tabelas de destino para você. No entanto, se for necessário copiar vários bancos de dados ou tabelas, ou outros tipos de objetos de banco de dados, será necessário usar o Assistente para Copiar Banco de Dados. Para obter mais informações, consulte [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Opções  
 **Instrução SQL**  
 Digite uma instrução de consulta para recuperar linhas selecionadas de dados do banco de dados de origem. Por exemplo, a seguinte instrução de consulta recupera o **SalesPersonID**, **SalesQuota**, e **SalesYTD** de AdventureWorks do banco de dados para vendedores cujo percentual de comissão for superior a 1,5 por cento.  
  
```  
SELECT SalesPersonID, SalesQuota, SalesYTD  
FROM Sales.SalesPerson  
WHERE CommissionPct > 0.015  
```  
  
 **Analisar**  
 Verifica a sintaxe da instrução SQL na caixa de texto **Instrução SQL**.  
  
> [!NOTE]  
>  Se o tempo necessário para verificar a sintaxe da instrução ultrapassar o valor de tempo limite, que é de 30 segundos, a análise será interrompida e será gerado um erro. Você só conseguirá ir além dessa página do assistente quando a análise for bem-sucedida. Uma solução possível é criar uma exibição de banco de dados com base na consulta e consultar a exibição usando o assistente em vez de inserir o texto da consulta diretamente.  
  
 **Procurar**  
 Selecione um arquivo que contém uma instrução SQL usando o **abrir** caixa de diálogo. Selecionando um arquivo copia o texto do arquivo para o **instrução de consulta** caixa de texto.  
  
  
