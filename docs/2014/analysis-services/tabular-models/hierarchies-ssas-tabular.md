---
title: Hierarquias (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: e3e50e89-f85d-485b-a271-1e0550520212
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2301f57d97c42ef2887824d2acd092e2a78aee7a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48133436"
---
# <a name="hierarchies-ssas-tabular"></a>Hierarquias (SSAS tabular)
  Hierarquias, em modelos de tabela, são metadados que definem relações entre duas ou mais colunas em uma tabela. As hierarquias podem parecer separadas de outras colunas em uma lista de campo de cliente de relatório, facilitando para usuários clientes navegarem e incluírem em um relatório.  
  
 Seções neste tópico:  
  
-   [Benefícios](#bkmk_benefits)  
  
-   [Definindo hierarquias](#bkmk_define)  
  
-   [Tarefas relacionadas](#bkmk_related_tasks)  
  
##  <a name="bkmk_benefits"></a> Benefícios  
 As tabelas podem incluir dúzias ou até mesmo centenas de colunas com nomes de coluna incomuns em nenhuma ordem aparente. Isto pode levar a uma aparência não ordenada ao reportar listas de campo de cliente, dificultando aos usuários localizarem e incluírem dados em um relatório. As hierarquias podem fornecer uma exibição simples e intuitiva de uma estrutura de dados que, de outra maneira, seria complexa.  
  
 Por exemplo, em uma tabela de Data, você pode criar uma hierarquia de Calendário. O Ano civil é usado como o nível pai mais alto, com Mês, Semana e Dia incluídos como níveis filho (Ano civil->Mês->Semana->Dia). Esta hierarquia mostra uma relação lógica de Ano civil a Dia. Um usuário de cliente pode selecionar Ano Civil de uma Lista de campos para incluir todos os níveis em uma Tabela Dinâmica ou expandir a hierarquia e selecionar somente níveis específicos para serem incluídos na Tabela Dinâmica.  
  
 Como cada nível em uma hierarquia é uma representação de uma coluna em uma tabela, o nível pode ser renomeado. Embora não seja exclusivo para hierarquias (qualquer coluna pode ser renomeada em um modelo de tabela), a renomeação de níveis de hierarquia pode facilitar a localização e a inclusão de níveis em um relatório por usuários. Renomear um nível não renomeia a coluna que a referencia; simplesmente torna o nível mais identificável. Em nosso exemplo de hierarquia de Ano Civil, na tabela de Data em Exibição de Dados, as colunas: CalendarYear, CalendarMonth, CalendarWeek e CalendarDay foram renomeadas para Ano Civil, Mês, Semana e Dia para torná-las mais identificáveis. Renomear os níveis tem o benefício adicional de fornecer consistência em relatórios, já que os usuários não precisarão alterar nomes de coluna para torná-los mais legíveis em Tabelas Dinâmicas, gráficos, etc.  
  
 As hierarquias podem ser incluídas em perspectivas. As perspectivas definem subconjuntos visíveis de um modelo que fornece pontos de vista concentrados, específicos à empresa ou específicos ao aplicativo. Por exemplo, uma perspectiva pode fornecer aos usuários uma lista visível (hierarquia) de apenas os itens de dados necessários para os seus requisitos específicos de relatório. Para obter mais informações, consulte [Perspectives &#40;SSAS Tabular&#41;](perspectives-ssas-tabular.md).  
  
 As hierarquias não se destinam a serem usadas como um mecanismo de segurança, mas como uma ferramenta para fornecer uma melhor experiência. Toda a segurança de uma determinada hierarquia é herdada do modelo subjacente. As hierarquias não podem fornecer acesso a objetos de modelo aos quais o usuário ainda não tem acesso. A segurança para o banco de dados modelo deve ser resolvida antes que o acesso a objetos no modelo possa ser fornecido por meio de uma hierarquia. As funções de segurança podem ser usadas para proteger metadados e dados do modelo. Para obter mais informações, consulte [Roles &#40;SSAS Tabular&#41;](roles-ssas-tabular.md).  
  
##  <a name="bkmk_define"></a> Definindo hierarquias  
 Você cria e gerencia hierarquias usando o designer de modelo em Exibição de Diagrama. Não há suporte para a criação e o gerenciamento de hierarquias no designer de modelos na Exibição de Dados. Para exibir o designer de modelos na Exibição de Diagrama, clique no menu **Modelo** , aponte para **Exibição de Modelo**e clique em **Exibição de Diagrama**.  
  
 Para criar uma hierarquia, clique com o botão direito do mouse em uma coluna que você deseja especificar como o nível pai e clique em **Criar Hierarquia**. Você pode fazer seleções múltiplas de qualquer número de colunas (dentro de uma única tabela) para incluir ou pode adicionar colunas posteriormente como níveis filho clicando e arrastando colunas para o nível pai. Quando são selecionadas várias colunas, elas são colocadas automaticamente em uma ordem com base na cardinalidade. Você pode alterar a ordem clicando e arrastando uma coluna (nível) para uma ordem diferente ou usando controles de navegação Para cima e Para baixo no menu de contexto. Ao adicionar uma coluna como um nível filho, você pode usar detecção automática arrastando e removendo a coluna no nível pai.  
  
 Uma coluna pode aparecer em mais de uma hierarquia. Hierarquias não podem incluir objetos que não sejam colunas como medidas ou KPIs. Uma hierarquia pode ser baseada em colunas de dentro de somente uma única tabela. Se você fizer multisseleção de uma medida junto com uma ou mais colunas, ou se você selecionar colunas de várias tabelas, o comando **Criar Hierarquia** estará desabilitado no menu de contexto. Para adicionar uma coluna de uma tabela diferente, use a função RELATED DAX para adicionar uma coluna calculada que faz referência à coluna da tabela relacionada. A função usa a seguinte sintaxe: `=RELATED(TableName[ColumnName])`. Para obter mais informações, consulte a função RELATED.  
  
 Por padrão, as novas hierarquias são chamadas de hierarquia 1, hierarquia 2 etc. Você deve alterar os nomes das hierarquias para refletir a natureza da relação pai-filho, tornando-os mais identificáveis a usuários.  
  
 Depois de criar hierarquias, você pode testar a sua eficácia usando o recurso Analisar no Excel. Para obter mais informações, consulte [Analisar no Excel &#40;SSAS tabular&#41;](analyze-in-excel-ssas-tabular.md).  
  
##  <a name="bkmk_related_tasks"></a> Tarefas relacionadas  
  
|Tarefa|Description|  
|----------|-----------------|  
|[Criar e gerenciar hierarquias &#40;Tabular do SSAS&#41;](hierarchies-ssas-tabular.md)|Descreve como criar e gerenciar hierarquias usando o designer de modelo em Exibição de Diagrama.|  
  
## <a name="see-also"></a>Consulte também  
 [Designer de modelo de tabela &#40;Tabular do SSAS&#41;](../tabular-model-designer-ssas-tabular.md)   
 [Perspectivas &#40;Tabular do SSAS&#41;](perspectives-ssas-tabular.md)   
 [As funções &#40;Tabular do SSAS&#41;](roles-ssas-tabular.md)  
  
  
