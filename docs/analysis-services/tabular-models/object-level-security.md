---
title: Segurança em nível de objeto de modelo de tabela do Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 13baecb045e9e9952b2cee43541dfb8991dfae33
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2018
ms.locfileid: "53071983"
---
# <a name="object-level-security"></a>Segurança em nível de objeto
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
Segurança do modelo de dados começa com a implementação efetiva [funções](../../analysis-services/tabular-models/roles-ssas-tabular.md) e filtros de nível de linha para definir permissões de usuário nos dados e objetos de modelo de dados. Começando com modelos de tabela 1400, você também pode definir segurança em nível de objeto, que inclui a segurança em nível de tabela e a segurança em nível de coluna de [objeto funções](https://docs.microsoft.com/bi-reference/tmsl/roles-object-tmsl).

## <a name="table-level-security"></a>Segurança em nível de tabela

Com a segurança de nível de tabela, você pode não apenas restringir o acesso aos dados da tabela, mas também existe a nomes de tabela confidenciais, ajudando a impedir que usuários mal-intencionados descubram se uma tabela. 

 Segurança em nível de tabela é definida nos metadados JSON com base no Model. BIM, [linguagem de script de modelo Tabular (TMSL)](https://docs.microsoft.com/bi-reference/tmsl/tabular-model-scripting-language-tmsl-reference), ou [objeto modelo de TOM (Tabular)](https://docs.microsoft.com/bi-reference/tom/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo). Defina o **metadataPermission** propriedade do **tablePermissions** classe no [objeto funções](https://docs.microsoft.com/bi-reference/tmsl/roles-object-tmsl) para **nenhum**.

Neste exemplo, a propriedade metadataPermission da classe tablePermissions para a tabela de produto é definida como none:

```
"roles": [
  {
    "name": "Users",
    "description": "All allowed users to query the model",
    "modelPermission": "read",
    "tablePermissions": [
      {
        "name": "Product",
        "metadataPermission": "none"
      }
    ]
  }
```

## <a name="column-level-security"></a>Segurança em nível de coluna

Semelhante à segurança em nível de tabela, com segurança em nível de coluna pode não apenas restringir o acesso a dados de coluna, mas também nomes de colunas confidenciais, ajudando a impedir que usuários mal-intencionados descubram uma coluna.

 Segurança em nível de coluna é definida nos metadados JSON com base no Model. BIM, [linguagem de script de modelo Tabular (TMSL)](https://docs.microsoft.com/bi-reference/tmsl/tabular-model-scripting-language-tmsl-reference), ou [objeto modelo de TOM (Tabular)](https://docs.microsoft.com/bi-reference/tom/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo). Defina o **metadataPermission** propriedade do **columnPermissions** classe no [objeto funções](https://docs.microsoft.com/bi-reference/tmsl/roles-object-tmsl) para **nenhum**.

Neste exemplo, a propriedade metadataPermission da classe columnPermissions para a coluna taxa Base da tabela de funcionários é definida como none:

```
"roles": [
  {
    "name": "Users",
    "description": "All allowed users to query the model",
    "modelPermission": "read",
    "tablePermissions": [
      {
        "name": "Employee",
        "columnPermissions": [
          {
            "name": "Base Rate",
            "metadataPermission": "none"
          }
        ]
      }
    ]
  }
```

## <a name="restrictions"></a>Restrictions

*  Segurança em nível de tabela não pode ser definida para um modelo se ele divide uma cadeia de relações. É gerado um erro em tempo de design.
 Por exemplo, se houver relações entre as tabelas A e B e B e C, você não pode proteger a tabela B. Se a tabela B estiver protegida, uma consulta na tabela A não pode transitar as relações entre a tabela A e B e B e C. Nesse caso, uma relação separada pode ser configurada entre as tabelas A e B.

    ![Segurança em nível de tabela](../../analysis-services/tabular-models/media/ssas-ols.png)  


*  Segurança em nível de linha e segurança em nível de objeto não podem ser combinados das funções diferentes porque ela poderia introduzir acesso involuntário aos dados protegidos. Um erro será gerado no momento da consulta para os usuários que são membros de uma combinação de funções.

*  Cálculos dinâmicos (medidas, KPIs, DetailRows) são restritos automaticamente se fizerem referência a uma tabela protegida ou coluna. Embora não haja nenhum mecanismo para proteger explicitamente uma medida, é possível proteger implicitamente uma medida, atualizando a expressão para se referir a uma tabela protegida ou coluna.

*  As relações que fazem referência a uma coluna protegida trabalhar desde a coluna está na tabela não é segura.




## <a name="see-also"></a>Consulte também  
[Roles](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
[Objeto Roles (TMSL)](https://docs.microsoft.com/bi-reference/tmsl/roles-object-tmsl)  
[TMSL (linguagem de script de modelo de tabela)](https://docs.microsoft.com/bi-reference/tmsl/tabular-model-scripting-language-tmsl-reference)  
[Modelo de objeto tabular (TOM)](https://docs.microsoft.com/bi-reference/tom/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo).

  
