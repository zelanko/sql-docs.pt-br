---
title: Perspectivas (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 1f78c3a1-ce2c-4e7f-a277-71a657692bea
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 957657e71103b248cdafb645bf44a68a9b486a53
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62756848"
---
# <a name="perspectives-ssas-tabular"></a>Perspectivas (SSAS tabular)
  As perspectivas, em modelos tabulares, definem subconjuntos visíveis de um modelo que fornece pontos de vista concentrados, específicos à empresa ou específicos ao aplicativo.  
  
 Seções neste tópico:  
  
-   [Benefícios](#bkmk_understanding)  
  
-   [Testando perspectivas](#bkmk_testpersp)  
  
-   [Tarefas relacionadas](#bkmk_related_tasks)  
  
##  <a name="bkmk_understanding"></a> Benefícios  
 Os modelos tabulares podem ser muito complexos para usuários explorarem. Um único modelo pode representar o conteúdo de um data warehouse completo com muitas tabelas, medidas e dimensões. Essa complexidade pode ser difícil para usuários que precisam apenas interagir com uma pequena parte do modelo para satisfazer seus requisitos de Business Intelligence e geração de relatórios.  
  
 Em uma perspectiva, tabelas, colunas e medidas (inclusive KPIs) são definidas como objetos de campo. Você pode selecionar os campos exibíveis para cada perspectiva. Por exemplo, um único modelo pode conter dados de produto, de vendas, financeiros, de funcionários e geográficos. Enquanto um departamento de vendas precisa de dados de produto, vendas, promoções e geografia, não precisa de dados de funcionário e financeiros. De maneira semelhante, um departamento de recursos humanos não precisa de dados sobre promoções de vendas e geografia.  
  
 Quando um usuário se conectar a um modelo (como uma fonte de dados) com perspectivas definidas, o usuário poderá selecionar a perspectiva que deseja usar. Por exemplo, ao conectar-se a uma fonte de dados de modelo no Excel, os usuários de Recursos Humanos podem selecionar a perspectiva de Recursos Humanos na página Selecionar Tabelas e Exibições do Assistente de Conexão de dados. Somente campos (tabelas, colunas e medidas) definidos para a perspectiva de Recursos Humanos serão visíveis na Lista de Campos de Tabela Dinâmica.  
  
 As perspectivas não se destinam a serem usadas como um mecanismo de segurança, mas como uma ferramenta para fornecer uma melhor experiência. Toda a segurança de uma determinada perspectiva é herdada do modelo subjacente. As perspectivas não podem fornecer acesso a objetos de modelo aos quais o usuário ainda não tem acesso. A segurança para o banco de dados modelo deve ser resolvida antes que o acesso a objetos no modelo possa ser fornecido por meio de uma perspectiva. As funções de segurança podem ser usadas para proteger metadados e dados do modelo. Para obter mais informações, consulte [Funções &#40;SSAS de Tabela&#41;](roles-ssas-tabular.md).  
  
##  <a name="bkmk_testpersp"></a> Testando perspectivas  
 Ao criar um modelo, você pode usar o recurso Analisar no Excel no designer de modelo para testar a eficácia das perspectivas que você definiu. No menu **Modelo** no designer de modelo, quando você clica em **Analisar no Excel**, antes de o Excel abrir, a caixa de diálogo **Escolher Credenciais e Perspectiva** é aberta. Nesta caixa de diálogo, você pode especificar o usuário atual, um nome de usuário diferente, uma função e uma perspectiva que você usará para se conectar ao banco de dados do workspace modelo como uma fonte de dados e exibir os dados.  
  
##  <a name="bkmk_related_tasks"></a> Tarefas relacionadas  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Criar e gerenciar perspectivas &#40;SSAS de Tabela&#41;](perspectives-ssas-tabular.md)|Descreve como criar e gerenciar perspectivas usando a caixa de diálogo Perspectivas no designer de modelo.|  
  
## <a name="see-also"></a>Consulte também  
 [Funções &#40;SSAS de Tabela&#41;](roles-ssas-tabular.md)   
 [Hierarquias &#40;SSAS de Tabela&#41;](hierarchies-ssas-tabular.md)  
  
  
