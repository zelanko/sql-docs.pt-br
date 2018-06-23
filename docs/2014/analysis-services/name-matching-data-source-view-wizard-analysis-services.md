---
title: Correspondência de nomes (dados fonte exibição Assistente) (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.datasourceviewwizard.namematchingcriteria.f1
ms.assetid: 7f811e02-0fe6-45c9-a7b7-29c61032d96b
caps.latest.revision: 24
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: fcb6d01f55b450326efdea81d48135088d57fc3d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36012384"
---
# <a name="name-matching-data-source-view-wizard-analysis-services"></a>Correspondência de Nomes (Assistente de Exibição da Fonte de Dados) (Analysis Services)
  Use a página **Correspondência de Nomes** para selecionar o critério a ser usado para detectar possíveis relações entre as tabelas selecionadas para a exibição da fonte de dados e as outras tabelas no esquema. Se não existir nenhuma relação de chave estrangeira entre as tabelas, esse critério ajudará a identificar e adicionar tabelas relacionadas à exibição da fonte de dados. As relações lógicas identificadas pela correspondência de nomes também são adicionadas à exibição da fonte de dados.  
  
> [!NOTE]  
>  Essa página será exibida apenas se você selecionar uma fonte de dados que tem várias tabelas, mas nenhuma relação de chave estrangeira entre qualquer uma da tabelas.  
  
## <a name="options"></a>Opções  
 **Criar relações lógicas correspondendo colunas**  
 Selecione para usar um critério de correspondência de nomes para detectar possíveis dependências e relações lógicas entre as tabelas que você seleciona para inclusão na exibição da fonte de dados e nas outras tabelas do esquema. Se você desmarcar esta caixa de seleção, nenhum critério de correspondência de nomes será usado para identificar relações lógicas entre tabelas na fonte de dados.  
  
 **Correspondências de chave estrangeira**  
 Selecione o critério a ser usado para criar relações lógicas entre tabelas e exibições na fonte de dados. Caracteres não alfanuméricos são ignorados na correspondência de cadeias de caracteres. Por exemplo, todas as cadeias de caracteres "ID de Cliente", "ID_Cliente", "IDCliente" são correspondentes. Selecione uma das opções na tabela a seguir para criar relações sob as condições especificadas.  
  
|Select (selecionar)|Para criar|  
|------------|---------------|  
|**Mesmo nome que a chave primária**|Uma relação lógica com qualquer tabela com um nome de coluna que corresponda ao nome da coluna de chave primária em uma tabela selecionada.|  
|**Mesmo nome que a tabela de destino**|Uma relação lógica com qualquer tabela com um nome de coluna que corresponda ao nome de uma tabela selecionada.|  
|**Nome da tabela de destino + nome de chave primária**|Uma relação lógica com qualquer tabela na qual um nome de coluna corresponde ao nome da tabela selecionada concatenado com o nome da coluna de chave primária da tabela selecionada, nessa ordem. Caracteres não alfanuméricos dentro da concatenação são ignorados (por exemplo, "ID Produto", "ID_Produto" e "IDProduto", todos correspondem).|  
  
 **Descrição e exemplo**  
 Exiba uma descrição e um exemplo do critério selecionado.  
  
  