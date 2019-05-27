---
title: Propriedades (SSAS Tabular) do projeto | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.depservconfig.f1
- sql12.asvs.bidtoolset.semmodelprojprop.f1
ms.assetid: 333c1fc0-361c-415a-bd68-4e057f67bcb7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a050c8eecadec138341ffe2f64a791eb198beebf
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66066738"
---
# <a name="project-properties-ssas-tabular"></a>Propriedades de projetos (SSAS tabular)
  Este tópico descreve as propriedades do projeto de modelo. Cada projeto de modelo tabular tem opções de implantação e propriedades de servidor de implantação que especificam como o projeto e o modelo são implantados. Por exemplo, o servidor em que o modelo será implantado e o nome do banco de dados modelo implantado. Essas configurações são diferentes das propriedades do modelo, o que afeta o banco de dados de workspace do modelo. As propriedades de projeto descritas aqui estão em uma caixa de diálogo de propriedades modal, diferente na janela de propriedades usada para exibir outros tipos de propriedades. Para exibir as propriedades de projeto modal, no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], no **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto e clique em **Propriedades**.  
  
 Seções neste tópico:  
  
-   [Propriedades de projeto](#bkmk_proj_properties)  
  
-   [Para definir as configurações de propriedades Opções de implantação e servidor de implantação](#bkmk_conf_proj_settings)  
  
##  <a name="bkmk_proj_properties"></a> Propriedades de projeto  
 **Opções de implantação**  
  
|Propriedade|Configuração padrão|Descrição|  
|--------------|---------------------|-----------------|  
|**Opção de Processamento**|**Default**|Por padrão, o Analysis Services determinará o tipo de processamento necessário quando as alterações em objetos forem implantadas. Geralmente, resulta em tempo menor de implantação. No entanto, você também pode optar pelo processamento completo ou por não fazer o processamento a cada implantação.|  
|**Implantação Transacional**|**False**|Especifica se a implantação do modelo é transacional ou não. Por padrão, a implantação de todos os objetos ou dos objetos alterados não é transacional com o processamento desses objetos implantados. A implantação pode ser bem-sucedida e persistir mesmo em caso de falha do processamento. É possível alterar esse padrão para incorporar a implantação e o processamento em uma única transação.|  
|**Modo de Consulta**|**Na Memória**|Especifica a origem da qual os resultados da consulta são retornados. Para obter mais informações, consulte [Modo DirectQuery &#40;SSAS Tabular&#41;](directquery-mode-ssas-tabular.md).|  
  
 **Servidor de Implantação**  
  
|Propriedade|Configuração padrão|Descrição|  
|--------------|---------------------|-----------------|  
|**Servidor**|**localhost**|Especifica uma instância do Analysis Services. Por padrão, os modelos são implantados na instância padrão do Analysis Services no computador local. É possível alterar essas configuração para especificar uma instância nomeada no computador local ou uma instância em qualquer outro computador remoto no qual você tenha permissão para criar objetos do Analysis Services. Geralmente, as permissões de administrador.<br /><br /> A configuração padrão para essa propriedade pode ser alterada usando a propriedade Servidor de Implantação Padrão na página Implantação nas configurações do Analysis Server na caixa de diálogo Ferramentas\Opções. Para obter mais informações, consulte [Configurar propriedades padrão de implantação e modelagem de dados &#40;SSAS de Tabela&#41;](properties-ssas-tabular.md).|  
|**Edição**|**Desenvolvedor**|Especifica a edição do servidor do Analysis Services para o qual o modelo será implantado. A edição do servidor define vários recursos que podem ser incorporados no projeto.|  
|**Backup de banco de dados**|**Modelo**|Especifica o nome do banco de dados do Analysis Services no qual os objetos modelo serão instanciados na implantação. Esse nome será especificado em uma conexão de dados ou em um arquivo .rsds de conexão de dados. É recomendável que o nome reflita o tipo de análise que será executada por meio do modelo, por exemplo, AdventureWorksSalesModel.<br /><br /> **\*\* Importante \* \***  para impedir nomes duplicados para modelos implantados, você deve alterar a **banco de dados** configuração de nome de propriedade para refletir o propósito do modelo. Quando os usuários se conectarem ao modelo como uma fonte de dados, este é o nome que eles verão.|  
|**Nome do Cubo**|**Modelo**|Especifica o nome do cubo de banco de dados como mostrado em uma conexão de dados de cliente de relatório.|  
|**Versão**|**11.0**|A versão da instância do Analysis Services no qual o projeto será implantado.|  
  
 **Opções de DirectQuery**  
  
|Propriedade|Configuração padrão|Descrição|  
|--------------|---------------------|-----------------|  
|**Configurações da representação**|**Default**|Especifica as credenciais que são usadas para conectar-se a fontes de dados para um modelo executando em Modo DirectQuery. Estas credenciais são diferentes de credenciais de representação que são usados no modo Na Memória padrão. Para obter mais informações, consulte [Representação &#40;SSAS de Tabela&#41;](impersonation-ssas-tabular.md).|  
  
###  <a name="bkmk_conf_proj_settings"></a> Para definir as configurações de propriedades Opções de implantação e servidor de implantação  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], no **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto e clique em **Propriedades**.  
  
2.  Na janela **Propriedades** , clique em uma propriedade e digite um valor ou clique na seta para baixo para selecionar uma opção de configuração.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar propriedades padrão de implantação e modelagem de dados &#40;SSAS de Tabela&#41;](properties-ssas-tabular.md)   
 [Propriedades de modelo &#40;SSAS de Tabela&#41;](model-properties-ssas-tabular.md)   
 [Implantação de uma solução de modelo de tabela &#40;SSAS de Tabela&#41;](tabular-model-solution-deployment-ssas-tabular.md)  
  
  
