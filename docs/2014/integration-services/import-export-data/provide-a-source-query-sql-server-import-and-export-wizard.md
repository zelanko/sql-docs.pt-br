---
title: Fornecer uma consulta de origem (Assistente de Importação e Exportação do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.impexpwizard.providesourcequery.f1
ms.assetid: c8cbd07e-b9c3-422f-94b8-d6fc8cf31cf5
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 1c8ad78723a1325ac6e21365b3e00e43f2d36d55
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019839"
---
# <a name="provide-a-source-query-sql-server-import-and-export-wizard"></a>Fornecer uma consulta de origem (Assistente de Importação e Exportação do SQL Server)
  Use o **fornecer uma consulta de origem** página digitar a instrução SQL que irá gerar os dados a serem copiadas da fonte de dados para o destino.  
  
 Para saber mais sobre este assistente, consulte [SQL Server Import and Export Wizard](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Para saber mais sobre as opções para iniciar o assistente, bem como as permissões necessárias para executar o assistente com êxito, consulte [executar o Assistente de exportação e importação do SQL Server](start-the-sql-server-import-and-export-wizard.md).  
  
 O objetivo do Assistente de Importação e Exportação do SQL Server é copiar dados de uma origem para um destino. O assistente também pode criar um banco de dados de destino e tabelas de destino para você. No entanto, se for necessário copiar vários bancos de dados ou tabelas, ou outros tipos de objetos de banco de dados, será necessário usar o Assistente para Copiar Banco de Dados. Para obter mais informações, consulte [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Opções  
 **Instrução SQL**  
 Digite uma instrução de consulta para recuperar linhas selecionadas de dados do banco de dados de origem. Por exemplo, a seguinte instrução de consulta recupera o **SalesPersonID**, **SalesQuota**, e **SalesYTD** de AdventureWorks do banco de dados para vendedores cuja Porcentagem de comissão for superior a 1,5 por cento.  
  
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
  
  