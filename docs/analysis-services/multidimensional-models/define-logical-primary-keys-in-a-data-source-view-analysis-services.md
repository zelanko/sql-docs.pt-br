---
title: Definir chaves primárias lógicas em uma exibição de fonte de dados (Analysis Services) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 90684f55414fa9e3f0d68a8ec90884fdae4d2c0a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68178734"
---
# <a name="define-logical-primary-keys-in-a-data-source-view-analysis-services"></a>Definir chaves primárias lógicas em uma exibição da fonte de dados (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
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
 [Exibições de fontes de dados em modelos multidimensionais](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [Definir cálculos nomeados em uma exibição da fonte de dados &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
  
