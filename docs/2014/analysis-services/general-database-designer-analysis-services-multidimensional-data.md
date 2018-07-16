---
title: Geral (Designer de banco de dados) (Analysis Services - dados multidimensionais) | Microsoft Docs
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
- sql12.asvs.databasedesigner.dbconfigurationpane.f1
helpviewer_keywords:
- Database Designer
ms.assetid: 00c9c42b-db2b-4620-8fb6-1e165ff0cbdd
caps.latest.revision: 25
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8a2af00d2dcdb6d28ab311067172e808e49539a0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37234266"
---
# <a name="general-database-designer-analysis-services---multidimensional-data"></a>Geral (Designer de Banco de Dados) (Analysis Services - Dados Multidimensionais)
  Use a guia **Geral** para alterar as propriedades de um banco de dados do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
 **Para exibir a guia Geral**  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra um projeto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
2.  No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , clique em **Editar Banco de Dados**e na guia **Geral** .  
  
## <a name="basic-options"></a>Opções básicas  
 Expanda a seção **Básico** para modificar informações básicas sobre o banco de dados. Essa seção contém as seguintes opções:  
  
 **Nome do banco de dados**  
 Exibe o nome do banco de dados.  
  
> [!NOTE]  
>  Para renomear o banco de dados, no **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto e clique em **Propriedades**. Na caixa de diálogo **Páginas de Propriedades** , na página **Implantação** , altere o valor da propriedade **Banco de Dados** para o novo nome do banco de dados.  
  
 **Descrição**  
 Digite a descrição do banco de dados.  
  
## <a name="translations-options"></a>Opções de traduções  
 Expanda a seção **Traduções** para criar e modificar traduções da legenda e da descrição do banco de dados. Essa seção contém uma grade com as seguintes colunas:  
  
 **Idioma**  
 Selecione o idioma para a transação especificada.  
  
 Para adicionar uma nova tradução à grade, clique em  **\<adicionar nova tradução >**.  
  
 **Legenda traduzida**  
 Digite a legenda do banco de dados no idioma adequado para a tradução. Se estiver em branco, será usada a legenda padrão do banco de dados.  
  
 **Descrição traduzida**  
 Digite a descrição do banco de dados no idioma adequado para a tradução. Se estiver em branco, será usada a descrição padrão do banco de dados.  
  
## <a name="account-type-mapping-options"></a>Opções de Mapeamento de Tipo de Conta  
 Expanda a seção **Mapeamento de Tipo de Conta** para modificar a função de agregação padrão associada a cada **tipo** de conta do banco de dados selecionado.  
  
> [!NOTE]  
>  Essa opção é aplicável apenas a cubos nos quais uma ou mais medidas usam a função de agregação *ByAccount* .  
  
 Essa seção contém uma grade com as seguintes colunas:  
  
 **Nome**  
 Digite o nome do tipo da conta.  
  
 Para adicionar um novo tipo de conta, clique em  **\<adicionar novo tipo de conta >**.  
  
 **Alias**  
 Define o nome padrão do tipo de conta para uso pelo Assistente de Business Intelligence. Se essa coluna for deixada em branco, o padrão na coluna **Nome** será usado.  
  
 **Função de agregação**  
 Selecione a função de agregação que será usada para o tipo de conta selecionado.  
  
## <a name="see-also"></a>Consulte também  
 [Designers e caixas de diálogo do Analysis Services &#40;dados multidimensionais&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Bancos de dados modelo multidimensionais &#40;SSAS&#41;](multidimensional-models/multidimensional-model-databases-ssas.md)   
 [Avisos &#40;Designer de banco de dados&#41; &#40;Analysis Services - dados multidimensionais&#41;](warnings-database-designer-analysis-services-multidimensional-data.md)  
  
  
