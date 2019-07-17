---
title: Propriedades de modelo de tabela do Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d9251a09039d93d473963ced235669c66f99431b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68207605"
---
# <a name="model-properties"></a>Propriedades do modelo 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Este artigo descreve as propriedades do modelo de tabela. Cada projeto de modelo tabular tem propriedades modelo que afetam o modo como o modelo que você está criando no SQL Server Development Tools é compilado, como o backup é feito e como o banco de dados de workspace é armazenado. As propriedades do modelo descritas aqui não se aplicam a modelos que já foram implantados.  
  
 Seções neste tópico:  
  
-   [Propriedades do modelo](#bkmk_model_properties)  
  
-   [Definir configurações de propriedades do modelo](#bkmk_conf_model_prop)  
  
##  <a name="bkmk_model_properties"></a> Propriedades do modelo  
 **Avançado**  
  
|Propriedade|Configuração padrão|Descrição|  
|--------------|---------------------|-----------------|  
|**Criar ação**|Compilar|Esta propriedade especifica como o arquivo se relaciona ao processo de criação e implantação. Essa configuração de propriedade tem as seguintes opções:<br /><br /> **Compilar** -ocorre uma ação de criação normal. As definições para objetos de modelo serão gravadas no arquivo .asdatabase.<br /><br /> **Nenhum** -a saída para o arquivo. asdatabase será vazia.|  
|**Copiar para o diretório de saída**|Não copiar|Esta propriedade especifica o arquivo de origem que será copiado no diretório de saída. Essa configuração de propriedade tem as seguintes opções:<br /><br /> **Não copie** – nenhuma cópia é criada no diretório de saída.<br /><br /> **Copiar sempre** -uma cópia é sempre criada no diretório de saída.<br /><br /> **Copiar se mais recente** – Uma cópia será criada somente no diretório de saída se houver alterações ao arquivo model.bim.|  
  
 **Diversos**  
  
> [!NOTE]  
>  Algumas propriedades são definidas automaticamente na criação do modelo e não podem ser alteradas.  
  
> [!NOTE]  
>  As propriedades Servidor de Workspace, Retenção de Workspace e Backup de Dados têm configurações padrão aplicadas quando você cria um novo projeto de modelo. Você pode alterar as configurações padrão para novos modelos na página Modelagem de Dados nas configurações do Analysis Server na caixa de diálogo Ferramentas\Opções. Estas propriedades, assim como outras, também podem ser definidas para cada modelo na janela Propriedades. Para obter mais informações, consulte [configurar propriedades de implantação e modelagem de dados padrão](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md).  
  
|Propriedade|Configuração padrão|Descrição|  
|--------------|---------------------|-----------------|  
|**Ordenação**|A ordenação padrão para o computador no qual o Visual Studio está instalado.|O designador de ordenação para o modelo.|  
|**Nível de Compatibilidade**|Opção padrão ou outra selecionada ao criar o projeto.|Aplica-se ao SQL Server 2012 Analysis Services SP1 ou posterior. Especifica os recursos e as configurações disponíveis para este modelo. Para obter mais informações, consulte [Nível de compatibilidade para modelos de tabela no Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md).|  
|**Backup de Dados**|Não fazer backup em disco|Especifica se o backup dos dados do modelo é mantido em um arquivo de backup. Essa configuração de propriedade tem as seguintes opções:<br /><br /> **Fazer backup em disco** – Especifica para manter um backup de dados do modelo em disco. Quando o modelo for salvo, os dados também serão salvos no arquivo de backup (ABF). A seleção dessa opção pode tornar o salvamento e os tempos de carregamento do modelo mais lentos.<br /><br /> **Não fazer backup em disco** – Especifica para não manter um backup de dados do modelo em disco. Essa opção minimizará o tempo de salvamento e carregamento do modelo.<br /><br /> <br /><br /> A configuração padrão para essa propriedade pode ser alterada na página Modelagem de Dados nas configurações do Analysis Server na caixa de diálogo Ferramentas\Opções.| 
|**Direção do filtro padrão**|Direção única|Determina a direção do filtro padrão para novas relações.| 
|**Modo DirectQuery**|Desativado|Especifica se este modelo opera em Modo DirectQuery ou não. Para obter mais informações, consulte [o modo DirectQuery](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md).|  
|**Nome do Arquivo**|Model.bim|Especifica o nome do arquivo .bim. O nome do arquivo não deve ser alterado.|  
|**Caminho completo**|Caminho especificado quando o projeto foi criado.|O local do arquivo model.bim. Essa propriedade não pode ser configurada na janela Propriedades.|  
|**Idioma**|Inglês|O idioma padrão do modelo. O idioma padrão é determinado pelo idioma do Visual Studio. Essa propriedade não pode ser configurada na janela Propriedades.|  
|**Banco de dados do workspace**|O nome de projeto, seguido por um sublinhado, seguido por um GUID.|O nome do banco de dados de workspace usado por armazenar e editar o modelo de memória temporário para o arquivo model.bim selecionado. Esse banco de dados será exibido na instância do Analysis Services especificada na propriedade de Servidor de Workspace. Essa propriedade não pode ser configurada na janela Propriedades. Para obter mais informações, consulte [banco de dados do espaço de trabalho](../../analysis-services/tabular-models/workspace-database-ssas-tabular.md).|  
|**Retenção de Workspace**|Descarregar da memória|Especifica como um banco de dados de workspace é retido depois que um modelo é fechado. Um banco de dados de workspace inclui metadados modelo, os dados importados em um modelo e credenciais de representação (criptografadas). Em alguns casos, o banco de dados de workspace pode ser muito grande e consumir uma quantidade significativa de memória. Por padrão, os bancos de dados de workspace são descarregados da memória. Ao alterar essa configuração, é importante considerar os recursos de memória disponíveis, bem como a frequência na qual você planeja trabalhar no modelo. Essa configuração de propriedade tem as seguintes opções:<br /><br /> **Manter na memória** - Especifica manter o banco de dados de workspace na memória depois que um modelo é fechado. Essa opção consumirá mais memória. No entanto, ao abrir um modelo, menos recursos serão consumidos e o banco de dados do workspace será carregado mais rapidamente.<br /><br /> **Descarregar da memória** - Especifica manter banco de dados de workspace em disco, e não mais na memória depois que um modelo é fechado. Essa opção consumirá menos memória. No entanto, ao abrir um modelo, recursos adicionais serão consumidos e o modelo será carregado mais lentamente do que se o banco de dados de workspace estivesse mantido na memória. Use essa opção quando os recursos de memória forem limitados ou ao trabalhar em um banco de dados de workspace remoto.<br /><br /> **Excluir workspace** - Especifica excluir o banco de dados de workspace da memória e não manter banco de dados de workspace em disco depois que o modelo é fechado. Essa opção consumirá menos memória e espaço de armazenamento, No entanto, ao abrir um modelo, serão consumidos recursos adicionais e o modelo será carregado mais lentamente do que se o banco de dados de workspace estivesse mantido na memória ou no disco. Use essa opção apenas ao trabalhar ocasionalmente em modelos.<br /><br /> <br /><br /> A configuração padrão para essa propriedade pode ser alterada na página Modelagem de Dados nas configurações do Analysis Server na caixa de diálogo Ferramentas\Opções.|  
|**Servidor de workspace**|localhost|Essa propriedade especifica o servidor fora-de-processo padrão que será usado para hospedar o banco de dados de workspace enquanto o modelo é criado. Todas as instâncias disponíveis do Analysis Services que executam no computador local são incluídas na caixa de listagem.<br /><br /> A configuração padrão para essa propriedade pode ser alterada na página Modelagem de Dados nas configurações do Analysis Server na caixa de diálogo Ferramentas\Opções.<br /><br /> <br /><br /> Observação: É recomendável sempre especificar um servidor do Analysis Services local como o servidor de espaço de trabalho. Para bancos de dados de workspaces em um servidor remoto, não há suporte para a importação do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)], o backup dos dados não pode ser feito localmente e a interface do usuário pode experimentar latência durante consultas.|  
  
##  <a name="bkmk_conf_model_prop"></a> Definir configurações de propriedades do modelo  
  
1.  No SSDT, em **Gerenciador de Soluções**, clique no arquivo **Model.bim** .  
  
2.  Na janela **Propriedades** , clique em uma propriedade e digite um valor ou clique na seta para baixo para selecionar uma opção de configuração.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar as propriedades de implantação e modelagem de dados padrão](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)   
 [Propriedades do projeto](../../analysis-services/tabular-models/project-properties-ssas-tabular.md)  
  
  
