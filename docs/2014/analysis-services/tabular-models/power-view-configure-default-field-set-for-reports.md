---
title: Configurar conjunto de campo padrão para relatórios do Power View (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- ql12.asvs.bidtoolset.deffieldset.f1
ms.assetid: 6836b42f-28b8-4a98-a86d-2c3c109f0189
caps.latest.revision: 6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0eba29031af4265c1850ed6a3ecf0241b60ac808
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37263262"
---
# <a name="configure-default-field-set-for-power-view-reports-ssas-tabular"></a>Configurar conjunto de campo padrão para relatórios de Power View (SSAS tabular)
  Um conjunto de campo padrão é uma lista predefinida de colunas e medidas que são adicionadas automaticamente a uma tela de relatório do [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] quando a tabela é selecionada na lista de campos de relatório. Os autores de modelo de tabela podem criar um campo padrão definido para eliminar etapas redundantes para autores de relatório que usam o modelo para os seus relatórios. Por exemplo, se você souber que a maioria dos autores de relatório que trabalham com informações de contato de cliente sempre querem ver um nome de contato, um número de telefone principal, um endereço de email e um nome de empresa, poderá pré-selecionar essas colunas para que elas sempre sejam adicionadas à tela de relatório quando o autor clicar na tabela Contato do Cliente.  
  
> [!NOTE]  
>  Um conjunto de campo padrão só se aplica a um modelo de tabela como um modelo de dados no [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]. Os conjuntos de campo padrão não têm suporte em relatórios dinâmicos do Excel.  
  
## <a name="creating-a-default-field-set"></a>Criando um conjunto de campo padrão  
 Você pode determinar quais campos, se houver, serão incluídos por padrão sempre que uma tabela específica for selecionada no [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]. Você também pode determinar a ordem na qual os campos aparecem na lista. Para especificar um conjunto de campo padrão, você define propriedades de relatório no projeto de modelo de tabela.  
  
#### <a name="to-add-a-default-field-set"></a>Para adicionar um conjunto de campo padrão  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], clique na tabela (guia) para a qual você está configurando uma lista de campos padrão.  
  
2.  Na janela **Propriedades** , na propriedade **Conjunto de Campo Padrão** , clique em **Clicar para editar**.  
  
3.  Na caixa de diálogo Conjunto de Campo Padrão, selecione um ou mais campos. Você pode escolher qualquer campo na tabela, inclusive medidas. Mantenha a tecla Shift pressionada para selecionar um intervalo ou a tecla Ctrl para selecionar campos individuais.  
  
4.  Clique em **Adicionar** para adicioná-los ao conjunto de campo padrão.  
  
5.  Use os botões Para cima e Para baixo para especificar uma ordem para a lista de campos. Os campos serão adicionados ao relatório na ordem definida para o conjunto de campo.  
  
6.  Repita estas etapas para outras tabelas em sua pasta de trabalho.  
  
## <a name="next-step"></a>Próxima etapa  
 Depois que você criar um conjunto de campo padrão, pode influenciar ainda mais a experiência de design de relatório especificando rótulos padrão, imagens padrão, comportamento de grupo padrão, ou se as linhas que contêm o mesmo valor são agrupadas em uma linha ou listadas individualmente. Para obter mais informações, consulte [Configurar propriedades de comportamento de tabela para relatórios de Power View &#40;SSAS Tabular&#41;](power-view-configure-table-behavior-properties-for-reports.md).  
  
  
