---
title: Segurança de nível de objeto de modelo de tabela | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a52b94dc7056b52892e744485be979a19808f6a1
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/08/2018
---
# <a name="object-level-security"></a>Segurança em nível de objeto
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
Segurança do modelo de dados começa com efetivamente implementando [funções](../../analysis-services/tabular-models/roles-ssas-tabular.md) e filtros de nível de linha para definir permissões de usuário nos dados e objetos de modelo de dados. Começando com modelos de tabela 1400, você também pode definir segurança em nível de objeto, que inclui a segurança em nível de tabela e segurança em nível de coluna a [objeto funções](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md).

## <a name="table-level-security"></a>Segurança em nível de tabela

Com segurança em nível de tabela, você pode não apenas restringir o acesso a dados de tabela, mas também os nomes de tabela confidenciais, ajudando a impedir que usuários mal-intencionados descobrir se uma tabela existe. 

 Segurança em nível de tabela é definida nos metadados do JSON com base no Model.bim, [linguagem de script de modelo Tabular (TMSL)](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md), ou [modelo de objeto de tabela (TOM)](../../analysis-services/tabular-model-programming-compatibility-level-1200/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo.md). Definir o **metadataPermission** propriedade do **tablePermissions** classe no [objeto funções](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md) para **nenhum**.

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

Semelhante a segurança em nível de tabela, com segurança em nível de coluna pode não apenas restringir o acesso para dados de coluna, mas também os nomes de coluna confidencial, ajudando a impedir que usuários mal-intencionados descobrir uma coluna.

 Segurança em nível de coluna é definida nos metadados do JSON com base no Model.bim, [linguagem de script de modelo Tabular (TMSL)](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md), ou [modelo de objeto de tabela (TOM)](../../analysis-services/tabular-model-programming-compatibility-level-1200/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo.md). Definir o **metadataPermission** propriedade do **columnPermissions** classe no [objeto funções](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md) para **nenhum**.

Neste exemplo, a propriedade metadataPermission da classe columnPermissions para a coluna na tabela de funcionários de taxa de Base é definida como none:

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

## <a name="restrictions"></a>Restrições

*  Segurança em nível de tabela não pode ser definida para um modelo se ele divide uma cadeia de relações. É gerado um erro em tempo de design.
 Por exemplo, se houver relações entre as tabelas A e B e B e C, você não pode proteger tabela B. Se a tabela B estiver protegida, de uma consulta na tabela A não pode trânsito as relações entre a tabela A e B e B e C. Nesse caso, uma relação separada pode ser configurada entre as tabelas A e B.

    ![Segurança em nível de tabela](../../analysis-services/tabular-models/media/ssas-ols.png)  


*  Segurança em nível de linha e segurança em nível de objeto não podem ser combinados das funções diferentes porque ele poderia introduzir não intencional do acesso aos dados protegidos. Um erro será gerado no momento da consulta para os usuários que são membros de uma combinação de funções.

*  Cálculos dinâmicos (medidas, KPIs, DetailRows) são automaticamente restritos se eles fazem referência a uma tabela protegida ou coluna. Embora não haja nenhum mecanismo para proteger explicitamente uma medida, é possível proteger implicitamente uma medida, atualizando a expressão para fazer referência a uma tabela protegida ou coluna.

*  Funcionam as relações que fazem referência a uma coluna protegida desde que a tabela que contém a não coluna é segura.




## <a name="see-also"></a>Consulte também  
[Roles](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
[Objeto Roles (TMSL)](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md)  
[TMSL (linguagem de script de modelo de tabela)](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
[Modelo de objeto de tabela (TOM)](../../analysis-services/tabular-model-programming-compatibility-level-1200/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo.md).

  
