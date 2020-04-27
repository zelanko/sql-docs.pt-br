---
title: Caixa de diálogo Filtrar (Suplemento MDS para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: b987b141-5abf-4161-a073-4cfc3e7f5aae
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 757c70398afe0f88d535b6853abe29b79e9617bc
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "65482562"
---
# <a name="filter-dialog-box-mds-add-in-for-excel"></a>Caixa de diálogo Filtrar (Suplemento do MDS para Excel)
  No [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], use a caixa de diálogo **Filtrar** para restringir a lista de dados gerenciados no MDS antes de carregá-la no Excel.  
  
 Essa caixa de diálogo contém três seções: **Colunas**, **Linhas**e **Resumo**.  
  
## <a name="columns"></a>Colunas  
 Use a seção **Colunas** para determinar quais atributos (colunas) você deseja exibir no Excel.  
  
|Nome do controle|Descrição|  
|------------------|-----------------|  
|Tipo de atributo|Um tipo de atributo descreve o tipo de membros com que você deseja trabalhar. Na maioria dos casos, o tipo é **Folha**. Para obter mais informações sobre tipos de membros, consulte [Membros &#40;Master Data Services&#41;](../members-master-data-services.md).|  
|Hierarquia explícita|Se você escolher o tipo de atributo **Consolidado** , escolha a hierarquia à qual os membros consolidados pertencem. Para obter mais informações, consulte [Hierarquias explícitas &#40;Master Data Services&#41;](../explicit-hierarchies-master-data-services.md).|  
|Grupos de atributos|Grupos de atributos são uma maneira de agrupar subconjuntos de atributos. Escolha um grupo de atributos se desejar mostrar um subconjunto de atributos disponíveis. Para obter mais informações sobre grupos de atributos, consulte [Grupos de atributos &#40;Master Data Services&#41;](../attribute-groups-master-data-services.md).|  
|Selecionar Tudo|Clique para selecionar todos os atributos exibidos na lista.|  
|Limpar Tudo|Clique para desmarcar todos os atributos selecionados exibidos na lista.<br /><br /> Observação: não é possível limpar o **nome** e o **código**.|  
|Seta para Cima|Clique para mover o atributo selecionado para cima na lista. A ordem de cima para baixo corresponde à ordem da esquerda para a direita em que as colunas são exibidas na planilha.|  
|Seta para Baixo|Clique para mover para baixo o atributo selecionado na lista. A ordem de cima para baixo corresponde à ordem da esquerda para a direita em que as colunas são exibidas na planilha.|  
  
## <a name="rows"></a>Linhas  
 Use a seção **Linhas** para determinar quais membros (linhas) você deseja exibir no Excel. Você faz isso definindo critérios para filtrar as linhas que serão exibidas.  
  
|Nome do controle|Descrição|  
|------------------|-----------------|  
|Atributo|Exibe um atributo pelo qual você deseja filtrar. Se nenhum atributo está listado, é porque eles não foram adicionados.<br /><br /> Observação: você pode filtrar por atributos que não planeja mostrar na planilha.|  
|Operador|Exibe operadores que correspondem ao tipo de atributo que foi selecionado. Para obter mais informações, consulte [Operadores de filtro &#40;Master Data Services&#41;](../filter-operators-master-data-services.md).|  
|Critérios|O critério pelo qual você deseja filtrar.|  
|Resumo da Atualização|Ao trabalhar com conjuntos de dados grandes, clique para atualizar a seção **Resumo** com detalhes da quantidade de dados que serão carregados.|  
|Adicionar|Quando você clica em um atributo na seção **Colunas** e em **Adicionar**, um atributo é adicionado à lista de filtros.|  
|Remover Tudo|Remove todos os filtros da lista.|  
|Remover|Remove o filtro selecionado da lista.|  
  
## <a name="summary"></a>Resumo  
 Use a seção **Resumo** para exibir detalhes sobre a quantidade de dados que serão carregados, antes de carregá-los.  
  
|Nome do controle|Descrição|  
|------------------|-----------------|  
|Modelo|O nome do modelo.|  
|Versão|O nome da versão.|  
|Entidade|Nome da entidade.|  
|Linhas|O número de linhas que serão carregadas no Excel, com base nos filtros aplicados na seção **Linhas** .|  
|Colunas|O número de colunas que serão carregadas no Excel, com base nos atributos selecionados na seção **Colunas** .|  
  
## <a name="see-also"></a>Consulte Também  
 [Filtrar dados antes de carregar &#40;Suplemento MDS para Excel&#41;](filter-data-before-exporting-mds-add-in-for-excel.md)   
 [Carregando dados &#40;Suplemento MDS para Excel&#41;](overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
  
