---
title: Referências de coleções DataSources e DataSets (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f951a4aa-da55-4e43-8579-4a5d4480d11f
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 099d9f8ccb24e2675f61c89f277d82984901cd4e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37168147"
---
# <a name="datasources-and-datasets-collection-references-report-builder-and-ssrs"></a>Referências de coleções DataSources e DataSets (Construtor de Relatórios e SSRS)
  A coleção `DataSources` representa todas as fontes de dados usadas em um relatório. Da mesma forma, o `DataSets` coleção representa todos os conjuntos de dados para todas as fontes de dados em um relatório. Use o painel **Dados do Relatório** para obter uma exibição hierárquica dos conjuntos de dados do relatório organizados sob a fonte de dados a qual eles fazem referência. Se você incluir referências nessas coleções, não poderá ver os valores ao visualizar o relatório. Essas coleções estão disponíveis apenas após o relatório ter sido publicado em um servidor de relatório.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="datasources"></a>DataSources  
 A coleção de `DataSources` representa as fontes de dados referenciadas em uma definição de relatório publicada. É possível optar por incluir essas informações no relatório para documentar a origem dos dados do relatório. Essa coleção não está disponível no modo **Visualização** . A tabela a seguir descreve as variáveis dentro da coleção de `DataSources`.  
  
|**Variável**|`Type`|**Descrição**|  
|------------------|--------------|---------------------|  
|`DataSourceReference`|`String`|O caminho completo da definição da fonte de dados no servidor de relatório. Por exemplo, você pode incluir uma lista de todas as fontes de dados que um relatório usou como parte de um histórico de relatório. O exemplo a seguir mostra o caminho completo da fonte de dados denominada AdventureWorks2012:<br /><br /> `/DataSources/AdventureWorks2012`.|  
|`Type`|`String`|O tipo de provedor de dados para a fonte de dados. Por exemplo, `SQL`.|  
  
## <a name="datasets"></a>DataSets  
 A coleção de `DataSets` representa os conjuntos de dados referenciados em uma definição de relatório. É possível optar por incluir a consulta no relatório em uma caixa de texto, de modo que um usuário interessado exatamente nos dados que estão no relatório possa ver o texto do comando original. Essa coleção não está disponível no modo **Visualização** . A tabela a seguir descreve os membros do `DataSets` coleção.  
  
|**Membro**|`Type`|**Descrição**|  
|----------------|--------------|---------------------|  
|`CommandText`|`String`|Para fontes de dados do banco de dados, esta é a consulta usada para recuperar dados da fonte de dados. Se a consulta for uma expressão, essa será a expressão avaliada.|  
|`RewrittenCommandText`|`String`|O valor de CommandText expandido do provedor de dados. Geralmente isso é usado para relatórios com parâmetros de consulta mapeados para parâmetros de relatório. O provedor de dados define essa propriedade ao expandir as referências do parâmetro do texto do comando nos valores constantes selecionados para os parâmetros de relatório mapeados.|  
  
### <a name="using-query-expressions"></a>Usando expressões de consulta  
 É possível usar expressões para definir a consulta contida em um conjunto de dados. É possível usar esse recurso para projetar relatórios em que a consulta é alterada com base na entrada do usuário, dos dados em outros conjuntos de dados ou outras variáveis. Para obter mais informações sobre consultas, consulte [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](../report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte também  
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)  
  
  
