---
title: Especificar o comportamento de parametrização de consulta usando guias de plano | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- TEMPLATE plan guide
- PARAMETERIZATION FORCED option
- PARAMETERIZATION option
- PARAMETERIZATION SIMPLE option
- parameterization [SQL Server]
- overriding parameterization behavior
- plan guides [SQL Server], parameterization
- parameterized queries [SQL Server]
ms.assetid: f0f738ff-2819-4675-a8c8-1eb6c210a7e6
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 7a6cbd0829105c03dbb453de52d84455faeaef99
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907448"
---
# <a name="specify-query-parameterization-behavior-by-using-plan-guides"></a>Especificar comportamento de parametrização de consulta usando guias de plano
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Quando a opção de banco de dados PARAMETERIZATION está definida como SIMPLE, o otimizador de consulta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode optar por parametrizar as consultas. Isso significa que qualquer valor literal contido em uma consulta é substituído por parâmetros. Esse processo é denominado parametrização simples. Quando a parametrização SIMPLE está em vigor, você não pode controlar quais consultas são parametrizadas e quais não são. No entanto, você pode especificar que todas as consultas em um banco de dados sejam parametrizadas definindo a opção de banco de dados PARAMETERIZATION como FORCED. Esse processo é denominado parametrização forçada.  
  
 Você pode substituir o comportamento de parametrização de um banco de dados usando guias de plano das seguintes formas:  
  
-   Quando a opção de banco de dados PARAMETERIZATION está definida como SIMPLE, você pode especificar que haja a tentativa de parametrização forçada em uma determinada classe de consultas. Você faz isso criando uma guia de plano TEMPLATE no formulário parametrizado da consulta e especificando a dica de consulta PARAMETERIZATION FORCED no procedimento armazenado [sp_create_plan_guide](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md) . Você pode considerar esse tipo de guia de plano como uma forma de habilitar a parametrização forçada só em certa classe de consultas, em vez de em todas as consultas.  
  
-   Quando a opção de banco de dados PARAMETERIZATION está definida como FORCED, você pode especificar que, para uma determinada classe de consultas, haja somente a tentativa de parametrização simples, não a parametrização forçada. Você faz isso criando uma guia de plano TEMPLATE no formulário parametrizado de forçamento da consulta e especificando a dica de consulta PARAMETERIZATION SIMPLE em **sp_create_plan_guide**.  
  
 Considere a consulta a seguir no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] :  
  
```  
SELECT pi.ProductID, SUM(pi.Quantity) AS Total  
FROM Production.ProductModel AS pm   
    INNER JOIN Production.ProductInventory AS pi   
        ON pm.ProductModelID = pi.ProductID   
WHERE pi.ProductID = 101   
GROUP BY pi.ProductID, pi.Quantity HAVING SUM(pi.Quantity) > 50;  
```  
  
 Como um administrador de banco de dados, você determinou que não quer habilitar a parametrização forçada em todas as consultas no banco de dados. Porém, você quer evitar despesas de compilação em todas as consultas que são sintaticamente equivalentes à consulta anterior, mas só diferem em valores literais constantes. Em outras palavras, você quer parametrizar a consulta para que um plano de consulta para esse tipo de consulta seja reutilizado. Nesse caso, complete as seguintes etapas:  
  
1.  Recupere o formulário parametrizado da consulta. O único modo seguro de obter esse valor para uso em **sp_create_plan_guide** é usando o procedimento armazenado do sistema [sp_get_query_template](../../relational-databases/system-stored-procedures/sp-get-query-template-transact-sql.md) .  
  
2.  Crie a guia de plano no formulário parametrizado da consulta, especificando a dica de consulta PARAMETERIZATION FORCED.  

    > [!IMPORTANT]  
    >  Como parte da parametrização de uma consulta, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atribui um tipo de dados aos parâmetros que substituem os valores literais, dependendo do valor e tamanho do literal. O mesmo processo ocorre para o valor das literais constantes transferido para o parâmetro de saída **\@stmt** de **sp_get_query_template**. Como o tipo de dados especificado no argumento **\@params** de **sp_create_plan_guide** deve corresponder ao da consulta, uma vez que ele é parametrizado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], poderá ser necessário criar mais de uma guia de plano para abranger o intervalo completo de valores de parâmetro possíveis para a consulta.  

O script a seguir pode ser usado para obter a consulta parametrizada e criar uma guia de plano para ela:  
  
```  
DECLARE @stmt nvarchar(max);  
DECLARE @params nvarchar(max);  
EXEC sp_get_query_template   
    N'SELECT pi.ProductID, SUM(pi.Quantity) AS Total   
      FROM Production.ProductModel AS pm   
      INNER JOIN Production.ProductInventory AS pi ON pm.ProductModelID = pi.ProductID   
      WHERE pi.ProductID = 101   
      GROUP BY pi.ProductID, pi.Quantity   
      HAVING sum(pi.Quantity) > 50',  
    @stmt OUTPUT,   
    @params OUTPUT;  
EXEC sp_create_plan_guide   
    N'TemplateGuide1',   
    @stmt,   
    N'TEMPLATE',   
    NULL,   
    @params,   
    N'OPTION(PARAMETERIZATION FORCED)';  
```  
  
Da mesma forma, em um banco de dados no qual a parametrização forçada já está habilitada, você pode verificar se a consulta de exemplo e outras sintaticamente equivalentes, exceto pelos valores literais constantes, estão parametrizadas de acordo com as regras de parametrização simples. Para fazer isso, especifique PARAMETERIZATION SIMPLE em vez de PARAMETERIZATION FORCED na cláusula OPTION.  
  
> [!NOTE]  
>  Guias de plano TEMPLATE correspondem a instruções de consultas enviadas em lotes que só consistem em uma única instrução. Instruções existentes em lotes com várias instruções não são qualificadas para correspondência com guias de plano TEMPLATE.
