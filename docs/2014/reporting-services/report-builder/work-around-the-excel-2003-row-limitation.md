---
title: Solução alternativa a limitação de linhas do Excel | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: a4c8700b-bef5-4440-a99c-bba5dcc46bfd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d78406155e9d2fb808664ce1377d0aba9d52dc84
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59951772"
---
# <a name="work-around-the-excel-row-limitation"></a>Solução do problema de limitação de linhas do Excel
  Este tópico explica como resolver a limitação de linhas do Excel 2003 quando você exporta relatórios para o Excel. A solução alternativa é para um relatório que contém apenas uma tabela.  
  
 O Excel 2003 oferece suporte a um máximo de 65.536 linhas por planilha. Você pode solucionar essa limitação forçando uma quebra de página explícita depois de um determinado número de linhas. O renderizador do Excel cria uma nova planilha para cada quebra de página explícita.  
  
### <a name="to-create-an-explicit-page-break"></a>Para criar uma quebra de página explícita  
  
1.  Abra o relatório no [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] ou no Gerenciador de Relatórios.  
  
2.  Clique com o botão direito do mouse na linha Dados da tabela e clique em **Adicionar Grupo** > **Grupo Pai** para adicionar um grupo de tabelas externo.  
  
     ![Selecionar o grupo pai](../media/datarow-selectparentgroup.png "Selecionar o grupo pai")  
  
3.  Digite a fórmula a seguir na caixa de expressão **Agrupar por** e clique em **OK** para adicionar o grupo pai.  
  
     =Int((RowNumber(Nothing)-1)/65000)  
  
     A fórmula atribui um número a cada conjunto de 65000 linhas no conjunto de dados. Quando uma quebra de página é definida para o grupo, a expressão resulta em uma quebra de página a cada 65000 linhas.  
  
     A adição do grupo de tabelas externo adiciona uma coluna de grupo ao relatório.  
  
4.  Exclua a coluna de grupo clicando com o botão direito do mouse no cabeçalho de coluna, clicando em **Excluir Colunas**, selecionando **Excluir colunas apenas**e clicando em **OK**.  
  
     ![Excluir uma coluna de grupo](../media/groupcolumn-delete-updated.png "Excluir uma coluna de grupo")  
  
5.  Clique com o botão direito do mouse em **Grupo 1** na seção **Grupos de Linhas** e clique em **Propriedades do Grupo**.  
  
     ![Exibir as propriedades do grupo](../media/groupproperties-updated.png "Exibir as propriedades do grupo")  
  
6.  Na página **Classificação** da caixa de diálogo **Propriedades do Grupo** , selecione a opção de classificação padrão e clique em **Excluir**.  
  
     ![Excluir classificação padrão](../media/groupproperties-sorting-updated.png "Excluir classificação padrão")  
  
7.  Na página **Quebras de Página** , clique em **Entre cada instância de um grupo** e clique em **OK**.  
  
     ![Definir quebras de página](../media/groupproperties-pagebreaks-updated.png "Definir quebras de página")  
  
8.  Salve o relatório. Quando você exportá-lo para o Excel, a exportação será realizada para várias planilhas, e cada planilha conterá um máximo de 65000 linhas.  
  
  
