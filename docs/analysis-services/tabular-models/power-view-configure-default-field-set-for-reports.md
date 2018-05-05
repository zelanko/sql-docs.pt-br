---
title: Configurar conjunto de campo padrão para relatórios do Power View | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- ql12.asvs.bidtoolset.deffieldset.f1
ms.assetid: 6836b42f-28b8-4a98-a86d-2c3c109f0189
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 42504e139e0bcff171a61596b8c41a75e1da741f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="power-view---configure-default-field-set-for-reports"></a>Power View - Configure o conjunto de campo padrão para relatórios
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
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
 Depois que você criar um conjunto de campo padrão, pode influenciar ainda mais a experiência de design de relatório especificando rótulos padrão, imagens padrão, comportamento de grupo padrão, ou se as linhas que contêm o mesmo valor são agrupadas em uma linha ou listadas individualmente. Para obter mais informações, consulte [configurar propriedades de comportamento de tabela para relatórios do Power View](../../analysis-services/tabular-models/power-view-configure-table-behavior-properties-for-reports.md).  
  
  
