---
title: Definir chaves primárias lógicas em uma exibição de fonte de dados (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- removing logical primary keys
- logical primary keys [SQL Server]
- deleting logical primary keys
- data source views [Analysis Services], logical primary keys
ms.assetid: 172bc267-c637-4caa-bf55-0ba198d30b1e
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ab45dd923ca3efd4f04504e2b309f4dda4f7bf58
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37255658"
---
# <a name="define-logical-primary-keys-in-a-data-source-view-analysis-services"></a>Definir chaves primárias lógicas em uma exibição da fonte de dados (Analysis Services)
  O Assistente de Exibição da Fonte de Dados e o Designer de Exibição da Fonte de Dados definem automaticamente uma chave primária para uma tabela que é adicionada a uma exibição da fonte de dados baseada na tabela do banco de dados subjacente.  
  
 De vez em quando, pode ser necessário definir manualmente uma chave primária na exibição da fonte de dados. Por exemplo, por questões de desempenho ou design, as tabelas da fonte de dados podem não ter colunas de chave primária definidas explicitamente. Consultas nomeadas e exibições também podem omitir a coluna da chave primária de um tabela. Se a tabela, exibição ou consulta nomeada não tiver uma chave primária física definida, é possível definir manualmente uma chave primária lógica na tabela, exibição ou consulta nomeada no Designer de Exibição da Fonte de Dados.  
  
## <a name="set-a-logical-primary-key"></a>Definir uma chave primária lógica  
 O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] requer chaves primárias para identificar com exclusividade os registros de uma tabela, identificar as colunas de chave das tabelas da dimensão e oferecer suporte às relações entre tabelas, exibições e consultas nomeadas. Essas relações são usadas na construção de consultas para recuperar dados e metadados de fontes de dados subjacentes e aproveitar os recursos avançados de business intelligence.  
  
 Qualquer coluna pode ser usada para a chave primária lógica, incluindo um cálculo nomeado. Quando você criar uma chave primária lógica, uma restrição exclusiva será criada na exibição da fonte de dados e marcada como restrição de chave primária. Qualquer outra chave primária lógica especificada na tabela selecionada será excluída.  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto ou conecte-se ao banco de dados que contém a exibição da fonte de dados na qual você deseja definir uma chave primária lógica.  
  
2.  No Gerenciador de Soluções, expanda a pasta **Exibições da Fonte de Dados** e clique duas vezes na exibição da fontes de dados.  
  
     Para localizar uma tabela ou exibição, use a opção **Localizar Tabela** clicando no menu **Exibição da Fonte de Dados**  ou clicando com o botão direito do mouse em qualquer área dos painéis **Tabelas** ou **Diagrama** .  
  
3.  No painel **Tabelas** ou **Diagrama** , clique com o botão direito do mouse na coluna ou nas colunas que você quer usar para definir uma chave primária lógica e clique em **Definir Chave Primária Lógica**.  
  
     A opção para configurar a chave primária lógica estará disponível somente para as tabelas que não possuem uma chave primária.  
  
     Observe que, depois que você define a chave, agora um ícone de chave identifica as colunas de chave primária.  
  
## <a name="see-also"></a>Consulte também  
 [Exibições da fonte de dados em modelos multidimensionais](data-source-views-in-multidimensional-models.md)   
 [Definir cálculos nomeados em uma exibição da fonte de dados &#40;Analysis Services&#41;](define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
  
