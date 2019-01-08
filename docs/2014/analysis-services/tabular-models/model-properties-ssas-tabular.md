---
title: Propriedades (SSAS Tabular) de modelo | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.fileprop.f1
- sql12.asvs.bidtoolset.wspacedbconfig.f1
ms.assetid: 8ab04656-75a5-485c-9687-7b1ca49f7f80
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d87af32662b9b971d3ba983d38f3df39b5a3202c
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52502569"
---
# <a name="model-properties-ssas-tabular"></a>Model Properties (SSAS Tabular)
  Este tópico descreve as propriedades do modelo tabular. Cada projeto de modelo tabular no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] tem propriedades modelo que afetam o modo como o modelo que você está criando é criado, como o backup é feito e como o banco de dados de workspace é armazenado. As propriedades do modelo descritas aqui não se aplicam a modelos que já foram implantados.  
  
 Seções neste tópico:  
  
-   [Propriedades de modelo](#bkmk_model_properties)  
  
-   [Para definir as configurações de propriedade do modelo](#bkmk_conf)  
  
##  <a name="bkmk_model_properties"></a> Propriedades de modelo  
 **Avançado**  
  
|Propriedade|Configuração padrão|Descrição|  
|--------------|---------------------|-----------------|  
|**Criar ação**|Compilar|Esta propriedade especifica como o arquivo se relaciona ao processo de criação e implantação. Essa configuração de propriedade tem as seguintes opções:<br /><br /> **Compilar** -ocorre uma ação de criação normal. As definições para objetos de modelo serão gravadas no arquivo .asdatabase.<br /><br /> **Nenhum** -a saída para o arquivo. asdatabase será vazia.|  
|**Copiar para o diretório de saída**|Não copiar|Esta propriedade especifica o arquivo de origem que será copiado no diretório de saída. Essa configuração de propriedade tem as seguintes opções:<br /><br /> **Não copie** – nenhuma cópia é criada no diretório de saída.<br /><br /> **Copiar sempre** -uma cópia é sempre criada no diretório de saída.<br /><br /> **Copiar se mais recente** – Uma cópia será criada somente no diretório de saída se houver alterações ao arquivo model.bim.|  
  
 **Diversos**  
  
> [!NOTE]  
>  Algumas propriedades são definidas automaticamente na criação do modelo e não podem ser alteradas.  
  
> [!NOTE]  
>  As propriedades Servidor de Workspace, Retenção de Workspace e Backup de Dados têm configurações padrão aplicadas quando você cria um novo projeto de modelo. Você pode alterar as configurações padrão para novos modelos na página Modelagem de Dados nas configurações do Analysis Server na caixa de diálogo Ferramentas\Opções. Estas propriedades, assim como outras, também podem ser definidas para cada modelo na janela Propriedades. Para obter mais informações, consulte [Configurar propriedades padrão de implantação e modelagem de dados &#40;SSAS de Tabela&#41;](properties-ssas-tabular.md).  
  
|Propriedade|Configuração padrão|Descrição|  
|--------------|---------------------|-----------------|  
|**Ordenação**|A ordenação padrão para o computador no qual o Visual Studio está instalado.|O designador de ordenação para o modelo.|  
|**Nível de Compatibilidade**|Opção padrão ou outra selecionada ao criar o projeto.|Aplica-se ao SQL Server 2012 Analysis Services SP1 ou posterior. Especifica os recursos e as configurações disponíveis para este modelo. Para obter mais informações, consulte [nível de compatibilidade &#40;SP1 de tabela SSAS&#41;](compatibility-level-for-tabular-models-in-analysis-services.md).|  
|**Backup de Dados**|Não fazer backup em disco|Especifica se o backup dos dados do modelo é mantido em um arquivo de backup. Observe que a configuração padrão para essa propriedade pode ser alterada na página modelagem de dados nas configurações do Analysis Server na caixa de diálogo Ferramentas \ Opções. Essa configuração de propriedade tem as seguintes opções:<br /><br /> **Fazer backup em disco** – Especifica para manter um backup de dados do modelo em disco. Quando o modelo for salvo, os dados também serão salvos no arquivo de backup (ABF). A seleção dessa opção pode tornar o salvamento e os tempos de carregamento do modelo mais lentos.<br /><br /> **Não fazer backup em disco** – Especifica para não manter um backup de dados do modelo em disco. Essa opção minimizará o tempo de salvamento e carregamento do modelo.|  
|**Modo DirectQuery**|Desativado|Especifica se este modelo opera em Modo DirectQuery ou não. Para obter mais informações, consulte [Modo DirectQuery &#40;SSAS Tabular&#41;](directquery-mode-ssas-tabular.md).|  
|**Nome do Arquivo**|Model.bim|Especifica o nome do arquivo .bim. O nome do arquivo não deve ser alterado.|  
|**Caminho completo**|Caminho especificado quando o projeto foi criado.|O local do arquivo model.bim. Essa propriedade não pode ser configurada na janela Propriedades.|  
|**Idioma**|Inglês|O idioma padrão do modelo. O idioma padrão é determinado pelo idioma do Visual Studio. Essa propriedade não pode ser configurada na janela Propriedades.|  
|**Banco de dados do workspace**|O nome de projeto, seguido por um sublinhado, seguido por um GUID.|O nome do banco de dados de workspace usado por armazenar e editar o modelo de memória temporário para o arquivo model.bim selecionado. Esse banco de dados será exibido na instância do Analysis Services especificada na propriedade de Servidor de Workspace. Essa propriedade não pode ser configurada na janela Propriedades. Para obter mais informações, consulte [Banco de dados do workspace &amp;#40;SSAS tabular&amp;#41;](workspace-database-ssas-tabular.md).|  
|**Retenção de Workspace**|Descarregar da memória|Especifica como um banco de dados de workspace é retido depois que um modelo é fechado. Um banco de dados de workspace inclui metadados modelo, os dados importados em um modelo e credenciais de representação (criptografadas). Em alguns casos, o banco de dados de workspace pode ser muito grande e consumir uma quantidade significativa de memória. Por padrão, os bancos de dados de workspace são descarregados da memória. Ao alterar essa configuração, é importante considerar os recursos de memória disponíveis, bem como a frequência na qual você planeja trabalhar no modelo. Observe que a configuração padrão para essa propriedade pode ser alterada na página modelagem de dados nas configurações do Analysis Server na caixa de diálogo Ferramentas \ Opções. Essa configuração de propriedade tem as seguintes opções:<br /><br /> **Manter na memória** - Especifica manter o banco de dados de workspace na memória depois que um modelo é fechado. Essa opção consumirá mais memória. No entanto, ao abrir um modelo no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], menos recursos serão consumidos e o banco de dados do workspace será carregado mais rapidamente.<br /><br /> **Descarregar da memória** - Especifica manter banco de dados de workspace em disco, e não mais na memória depois que um modelo é fechado. Essa opção consumirá menos memória. No entanto, ao abrir um modelo no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], recursos adicionais serão consumidos e o modelo será carregado mais lentamente do que se o banco de dados de workspace estivesse mantido na memória. Use essa opção quando os recursos de memória forem limitados ou ao trabalhar em um banco de dados de workspace remoto.<br /><br /> **Excluir workspace** - Especifica excluir o banco de dados de workspace da memória e não manter banco de dados de workspace em disco depois que o modelo é fechado. Essa opção consumirá menos memória e espaço de armazenamento, No entanto, ao abrir um modelo no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], serão consumidos recursos adicionais e o modelo será carregado mais lentamente do que se o banco de dados de workspace estivesse mantido na memória ou no disco. Use essa opção apenas ao trabalhar ocasionalmente em modelos.|  
|**Servidor de workspace**|localhost|Essa propriedade especifica o servidor fora-de-processo padrão que será usado para hospedar o banco de dados de workspace enquanto o modelo é criado no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Todas as instâncias disponíveis do Analysis Services que executam no computador local são incluídas na caixa de listagem.<br /><br /> Observação: É recomendável especificar sempre um servidor do Analysis Services local como o servidor de workspace. Para bancos de dados de workspaces em um servidor remoto, não há suporte para a importação do PowerPivot, o backup dos dados não pode ser feito localmente e a interface do usuário pode experimentar latência durante consultas.<br /><br /> A configuração padrão para essa propriedade pode ser alterada na página Modelagem de Dados nas configurações do Analysis Server na caixa de diálogo Ferramentas\Opções.|  
  
##  <a name="bkmk_conf_model_prop"></a>   
###  <a name="bkmk_conf"></a> Para definir as configurações de propriedade do modelo  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], em **Gerenciador de Soluções**, clique no arquivo **Model.bim** .  
  
2.  Na janela **Propriedades** , clique em uma propriedade e digite um valor ou clique na seta para baixo para selecionar uma opção de configuração.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar propriedades padrão de implantação e modelagem de dados &#40;SSAS de Tabela&#41;](properties-ssas-tabular.md)   
 [Propriedades de projeto &#40;SSAS de Tabela&#41;](project-properties-ssas-tabular.md)  
  
  
