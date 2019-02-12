---
title: Adicionar, editar e atualizar campos no painel de dados do relatório (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 2e36f0fe-8100-4513-b169-14d611646f81
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 87ee0ab32e605214674c2ee2a933f63cc4b66268
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56032377"
---
# <a name="add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs"></a>Adicionar, editar e atualizar campos no painel de dados do relatório (Construtor de Relatórios e SSRS)
  Campos do conjunto de dados são a coleção interna de nomes de campos que representam os dados retornados quando uma consulta de conjunto de dados é executado em uma fonte de dados externa.  
  
 Para um conjunto de dados interno, os campos do conjunto de dados são os campos criados após a conclusão da criação de uma consulta e o fechamento do painel Designer de Consulta, e campos calculados criados por você.  
  
 Para um conjunto de dados compartilhado, os campos do conjunto de dados são os campos da definição do conjunto de dados compartilhado depois que você o adicionou ao relatório. Embora a consulta do conjunto de dados compartilhado no servidor de relatório sempre seja usada quando você executa o relatório, a lista de campos do conjunto de dados no relatório é estática.  
  
 Use **Atualizar Campos** para atualizar a lista de campos no relatório para corresponder à lista atual de campos da consulta do conjunto de dados compartilhado. A atualização da lista de campos não afeta os campos calculados definidos no relatório.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-query-field"></a>Para adicionar um campo de consulta  
  
1.  No painel de dados do relatório, clique com o botão direito do mouse no conjunto de dados e clique em **Adicionar Campo de Consulta**.  
  
    > [!NOTE]  
    >  Se não conseguir ver o painel de dados do relatório, no menu **Exibir** , clique em **Dados do Relatório**.  
  
2.  Na página **Campos** da caixa de diálogo **Propriedades do Conjunto de Dados** , clique em **Adicionar**e em **Campo de Consulta**. Uma linha nova é adicionada ao final da grade.  
  
3.  Na caixa de texto **Nome do Campo** , digite o nome para o campo.  
  
    > [!NOTE]  
    >  Os nomes devem ser exclusivos no conjunto de dados.  
  
4.  Na caixa de texto **Origem do Campo** , digite o nome de um campo existente na fonte de dados.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-add-a-calculated-field"></a>Para adicionar um campo calculado  
  
1.  No painel de dados do relatório, clique com o botão direito do mouse no conjunto de dados e clique em **Adicionar Campo Calculado**.  
  
2.  Na página **Campos** da caixa de diálogo **Propriedades do Conjunto de Dados** , clique em **Adicionar**e em **Campo Calculado**. Uma linha nova é adicionada ao final da grade.  
  
3.  Na caixa de texto **Nome do Campo** , digite o nome para o campo.  
  
    > [!NOTE]  
    >  Os nomes devem ser exclusivos no conjunto de dados.  
  
4.  Na caixa de texto **Origem do Campo** , digite a expressão para o campo. Clique no botão de expressão (**fx**) para criar uma expressão.  
  
    > [!NOTE]  
    >  A expressão de um campo calculado não pode conter agregações ou referências a itens de relatório.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-edit-a-query-field-or-a-dataset-field"></a>Para editar um campo de consulta ou de conjunto de dados  
  
1.  No painel de dados do relatório, clique com o botão direito do mouse no campo e clique em **Propriedades do Campo**.  
  
2.  Na página **Campos** da caixa de diálogo **Propriedades do Conjunto de Dados** , clique em um campo existente para selecionar a linha.  
  
3.  Altere o nome ou o valor do campo.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-delete-a-query-field-or-a-calculated-field"></a>Para excluir um campo de consulta ou um campo calculado  
  
1.  No painel de dados do relatório, expanda o conjunto de dados para exibir a coleção de campos.  
  
2.  Clique com o botão direito do mouse no campo que você deseja remover e clique em **Excluir**.  
  
### <a name="to-refresh-the-field-collection-in-the-report-data-pane-for-a-shared-dataset"></a>Para atualizar a coleção de campos no Painel Dados do Relatório para um conjunto de dados compartilhado  
  
1.  No painel Dados do Relatório, clique com o botão direito do mouse no conjunto de dados e clique em **Consulta**.  
  
2.  Clique em **Atualizar Campos**.  
  
     No servidor de relatório, a consulta do banco de dados compartilhado é executada e retorna a coleção de campos atual.  
  
## <a name="see-also"></a>Consulte também  
 [Coleção de campos de conjuntos de dados &#40;Construtor de Relatórios e SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)   
 [Adicionar dados a um relatório &#40;relatórios e SSRS&#41;](report-datasets-ssrs.md)   
 [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Designers de Consulta do Reporting Services](../reporting-services-query-designers.md)   
 [Designers de Consultas &#40;Construtor de Relatórios&#41;](../query-designers-report-builder.md)  
  
  
