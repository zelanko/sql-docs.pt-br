---
title: Selecionar tabelas e exibições (Assistente de exibição de fonte de dados) (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.datasourceviewwizard.selecttablesandviews.f1
ms.assetid: ea7d1232-f213-46e9-90d9-0fd616ca003d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f4b940d5cb3c91cc8257ef1a3e6828286bc1c240
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66069247"
---
# <a name="select-tables-and-views-data-source-view-wizard-analysis-services"></a>Selecionar Tabelas e Exibições (Assistente de Exibição da Fonte de Dados) (Analysis Services)
  Use a página **Selecionar Tabelas e Exibições** para selecionar as tabelas ou exibições da fonte de dados que você deseja incluir na exibição da fonte de dados.  
  
## <a name="options"></a>Opções  
 **Objetos disponíveis**  
 Lista as tabelas e exibições no esquema da fonte de dados. O nome do esquema será usado como um prefixo do nome de todos os objetos se mais de um esquema for listado. Se apenas um esquema for listado, o nome do objeto não terá o nome do esquema como prefixo.  
  
 Para reordenar a lista em ordem crescente ou decrescente, clique em **Nome** ou em **Tipo**.  
  
 **Objetos incluídos**  
 Lista as tabelas e exibições a serem incluídas na exibição da fonte de dados.  
  
 Para reordenar a lista em ordem crescente ou decrescente, clique em **Nome** ou em **Tipo**.  
  
 **Filter**  
 Filtra os objetos listados em **Objetos disponíveis**. Digite uma cadeia de caracteres e, em seguida, clique em **Filtro** para listar apenas os nomes que contêm uma cadeia de caracteres especificada. Para localizar uma cadeia de caracteres exata, inclua a cadeia de caracteres entre aspas duplas. O filtro não diferencia maiúsculas de minúsculas.  
  
 É possível incluir os caracteres curinga listados na tabela a seguir em qualquer lugar na cadeia de caracteres do filtro.  
  
|Caractere curinga|Valor|  
|------------------------|-----------|  
|**\***|Qualquer cadeia de caracteres|  
|**%**|Qualquer cadeia de caracteres|  
|**?**|Um único caractere|  
|**"** *string* **"**|Uma cadeia de caracteres literal. Este caractere curinga corresponderá a qualquer subcadeia de caracteres dentro do nome do objeto.|  
  
 **Mostrar objetos do sistema**  
 Exibe objetos do sistema em **Objetos disponíveis**. Essa opção estará disponível apenas se o provedor da fonte de dados expuser objetos do sistema. A remoção de um objeto do sistema da lista **Objetos incluídos** seleciona automaticamente essa opção.  
  
 **Adicionar tabelas relacionadas**  
 Adiciona todas as tabelas que estão relacionadas às tabelas listadas em **Objetos incluídos**. Essa opção não adiciona exibições. No entanto ela adiciona tabelas particionadas. Se você selecionar critérios de correspondência de nomes na página **Correspondência de Nomes** do assistente, essa opção também incluirá tabelas relacionadas lógicas de acordo com os critérios selecionados. Tabelas também serão incluídas se estiverem relacionadas a tabelas relacionadas recém-adicionadas e se tiverem uma estrutura idêntica a da tabela original.  
  
## <a name="see-also"></a>Consulte também  
 [Ajuda de F1 do Assistente de exibição de fonte de dados &#40;Analysis Services&#41;](data-source-view-wizard-f1-help-analysis-services.md)   
 [Exibições de fontes de dados em modelos multidimensionais](multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
