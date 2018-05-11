---
title: Propriedades do projeto | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 874f1b6cf24633070935a70425f1dc873aebc7dc
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="project-properties"></a>Propriedades do projeto 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Este artigo descreve as propriedades do projeto de modelo. Cada projeto de modelo tabular tem opções de implantação e propriedades de servidor de implantação que especificam como o projeto e o modelo são implantados. Por exemplo, o servidor em que o modelo será implantado e o nome do banco de dados modelo implantado. Essas configurações são diferentes das propriedades do modelo, o que afeta o banco de dados de espaço de trabalho do modelo. As propriedades de projeto descritas aqui estão em uma caixa de diálogo de propriedades modal, diferente na janela de propriedades usada para exibir outros tipos de propriedades. Para exibir as propriedades de projeto modal, no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], no **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto e clique em **Propriedades**.  
  
 Seções neste tópico:  
  
-   [Propriedades do projeto](#bkmk_proj_properties)  
  
-   [Definir as configurações de propriedade Opções de Implantação e Servidor de Implantação](#bkmk_conf_proj_settings)  
  
##  <a name="bkmk_proj_properties"></a> Propriedades do projeto  
 **Opções de implantação**  
  
|Propriedade|Configuração padrão|Description|  
|--------------|---------------------|-----------------|  
|**Opção de Processamento**|**Default**|Por padrão, o Analysis Services determinará o tipo de processamento necessário quando as alterações em objetos forem implantadas. Geralmente, resulta em tempo menor de implantação. No entanto, você também pode optar pelo processamento completo ou por não fazer o processamento a cada implantação.|  
|**Implantação Transacional**|**False**|Especifica se a implantação do modelo é transacional ou não. Por padrão, a implantação de todos os objetos ou dos objetos alterados não é transacional com o processamento desses objetos implantados. A implantação pode ser bem-sucedida e persistir mesmo em caso de falha do processamento. É possível alterar esse padrão para incorporar a implantação e o processamento em uma única transação.|  
|**Modo de Consulta**|**Na Memória**|Especifica a origem da qual os resultados da consulta são retornados. Para obter mais informações, consulte [o modo DirectQuery](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md).|  
  
 **Servidor de Implantação**  
  
|Propriedade|Configuração padrão|Description|  
|--------------|---------------------|-----------------|  
|**Servidor**|**localhost**|Especifica uma instância do Analysis Services. Por padrão, os modelos são implantados na instância padrão do Analysis Services no computador local. É possível alterar essas configuração para especificar uma instância nomeada no computador local ou uma instância em qualquer outro computador remoto no qual você tenha permissão para criar objetos do Analysis Services. Geralmente, as permissões de administrador.<br /><br /> A configuração padrão para essa propriedade pode ser alterada usando a propriedade Servidor de Implantação Padrão na página Implantação nas configurações do Analysis Server na caixa de diálogo Ferramentas\Opções. Para obter mais informações, consulte [configurar propriedades de implantação e modelagem de dados padrão](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md).|  
|**Edição**|**Desenvolvedor**|Especifica a edição do servidor do Analysis Services para o qual o modelo será implantado. A edição do servidor define vários recursos que podem ser incorporados no projeto.|  
|**Banco de dados**|**Modelo**|Especifica o nome do banco de dados do Analysis Services no qual os objetos modelo serão instanciados na implantação. Esse nome será especificado em uma conexão de dados ou em um arquivo .rsds de conexão de dados. É recomendável que o nome reflita o tipo de análise que será executada por meio do modelo, por exemplo, AdventureWorksSalesModel.<br /><br /> Para impedir nomes duplicados para modelos implantados, você deve alterar a configuração do nome de propriedade **Banco de dados** para refletir o propósito do modelo. Quando os usuários se conectarem ao modelo como uma fonte de dados, este é o nome que eles verão.|  
|**Nome do Cubo**|**Modelo**|Especifica o nome do cubo de banco de dados como mostrado em uma conexão de dados de cliente de relatório.|  
|**Versão**|**13.0**|A versão da instância do Analysis Services no qual o projeto será implantado.|  
  
 **Opções de DirectQuery**  
  
|Propriedade|Configuração padrão|Description|  
|--------------|---------------------|-----------------|  
|**Configurações da representação**|**Default**|Especifica as credenciais que são usadas para conectar-se a fontes de dados para um modelo executando em Modo DirectQuery. Estas credenciais são diferentes de credenciais de representação que são usados no modo Na Memória padrão. Para obter mais informações, consulte [representação](../../analysis-services/tabular-models/impersonation-ssas-tabular.md).|  
  
##  <a name="bkmk_conf_proj_settings"></a> Definir as configurações de propriedade Opções de Implantação e Servidor de Implantação  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], no **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto e clique em **Propriedades**.  
  
2.  Na janela **Propriedades** , clique em uma propriedade e digite um valor ou clique na seta para baixo para selecionar uma opção de configuração.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar propriedades de implantação e modelagem de dados padrão](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)   
 [Propriedades do modelo](../../analysis-services/tabular-models/model-properties-ssas-tabular.md)   
 [Implantação de solução de modelo tabular](../../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md)  
  
  
