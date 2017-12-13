---
title: "Banco de dados do espaço de trabalho (SSAS Tabular) | Microsoft Docs"
ms.custom: 
ms.date: 07/24/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 662daf08-a514-44a7-8675-44644aa454a2
caps.latest.revision: "24"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: ae2e26606a2f84abea1caed7032a80d2e2de7e45
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="workspace-database-ssas-tabular"></a>Banco de dados do espaço de trabalho (SSAS tabular)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]O banco de dados de espaço de trabalho do modelo de tabela, usado durante a criação do modelo, é criado quando você cria um novo projeto de modelo de tabela no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].
  
## <a name="specifying-a-workspace-instance"></a>Especificar uma instância do espaço de trabalho  
  Quando você cria um novo projeto de modelo de tabela no SSDT, você pode especificar uma instância do Analysis Services para usar ao criar seu projeto. Começando com a versão de setembro de 2016 (14.0.60918.0) de [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], introduz dois modos para especificar uma instância do espaço de trabalho quando você cria um novo projeto de modelo de tabela. 

**Espaço de trabalho integrado** – utiliza a própria instância interna do Analysis Services do SSDT.

**Servidor de espaço de trabalho** -um banco de dados do espaço de trabalho é criado em uma instância explícita do Analysis Services, normalmente no mesmo computador que o SSDT ou em outro computador na mesma rede.


  
### <a name="integrated-workspace"></a>Espaço de trabalho integrado
Com o espaço de trabalho integrado, um banco de dados de trabalho é criado na memória usando a própria instância implícita de Analysis Services do SSDT. Modo de espaço de trabalho integrado reduz significativamente a complexidade da criação de projetos de tabela no SSDT, pois uma instalação separada explícita do SQL Server Analysis Services não é necessária.

Usando o modo de espaço de trabalho integrado, SSDT Tabular dinamicamente inicia sua própria instância interna do SSAS em segundo plano e carrega o banco de dados. Você pode adicionar e exibir tabelas e dados no designer de modelo. Se você adicionar mais tabelas, colunas, relacionamentos, etc., estará alterando o banco de dados do espaço de trabalho. Modo de espaço de trabalho integrado não será alterado quando SSDT Tabular trabalhar com um servidor de espaço de trabalho e o banco de dados. O que muda é onde o SSDT Tabular hospeda o banco de dados do espaço de trabalho.

Você pode selecionar o modo do espaço de trabalho integrado ao criar um novo projeto de modelo de tabela no SSDT.

![Modo de espaço de trabalho integrado do SSAS](../../analysis-services/tabular-models/media/ssas-integrated-workspace-mode.png)

Usando as propriedades Banco de Dados do Espaço de Trabalho e Servidor de Espaço de Trabalho para model.bim, você pode descobrir o nome do banco de dados temporário e a porta TCP da instância interna de SSAS, na qual o SSDT Tabular hospeda o banco de dados. Você pode se conectar ao banco de dados de espaço de trabalho com o SSMS, contanto que SSDT Tabular tenha o banco de dados carregado. A configuração de Retenção do Espaço de Trabalho especifica que o SSDT Tabular mantém o banco de dados de espaço de trabalho no disco, e não mais na memória depois que um projeto de modelo é fechado. Isso garante que menos memória seja consumida do que se o modelo fosse mantido na memória em todos os momentos. Se você quiser controlar essas configurações, defina a propriedade de Modo de Espaço de Trabalho integrado como Falso e forneça um servidor de espaço de trabalho explícito. Um servidor de espaço de trabalho explícito também faz sentido se os dados que você está importando para um modelo de dados excede a capacidade de memória de sua estação de trabalho do SSDT.

> [!NOTE]  
>  Ao usar o modo integrado do espaço de trabalho, a instância local do Analysis Services é 64 bits, enquanto o SSDT é executado no ambiente de 32 bits do Visual Studio. Se você estiver se conectando a fontes de dados especiais, certifique-se de instalar ambas as versões de 32 bits e 64 bits dos provedores de dados correspondentes na estação de trabalho. O provedor de 64 bits é necessário para a instância do Analysis Services de 64 bits e a versão de 32 bits é necessária para o Assistente de importação de tabela no SSDT.

###  <a name="bkmk_overview"></a> Servidor de espaço de trabalho  
 Um banco de dados de espaço de trabalho é criado na instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , especificada na propriedade de Servidor de Espaço de trabalho, quando você cria um novo projeto de Business Intelligence usando um dos modelos de projeto de modelo de tabela no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Cada projeto de modelo tabular terá seu próprio banco de dados de espaço de trabalho. Você pode usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para exibir o banco de dados de espaço de trabalho no servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . O nome de banco de dados de espaço de trabalho inclui o nome de projeto, seguido por um sublinhado, seguido pelo nome de usuário, seguido por um sublinhado, seguido por um GUID.  
  
 O banco de dados de espaço de trabalho reside na memória enquanto o projeto de modelo tabular está aberto no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Quando você fecha o projeto, o banco de dados de espaço de trabalho é mantido na memória, armazenado em disco e removido da memória (padrão), ou removido da memória e não armazenado em disco, como determinado pela propriedade de Retenção de Espaço de Trabalho. Para obter mais informações sobre a propriedade de Retenção de Espaço de Trabalho, consulte [Propriedades de Banco de Dados de Espaço de Trabalho](#bkmk_ws_prop) posteriormente neste tópico.  
  
 Depois que você adicionou dados a seu projeto de modelo usando o Assistente de Importação de Tabela ou usando copiar/colar, ao exibir as tabelas, colunas e dados no designer de modelo, você estará exibindo o banco de dados de espaço de trabalho. Se você adicionar mais tabelas, colunas, relacionamentos, etc., estará alterando o banco de dados do espaço de trabalho.  
  
 Quando você implantar um projeto de modelo tabular, o banco de dados modelo implantado, que é essencialmente uma cópia do banco de dados de espaço de trabalho, é criado na instância de servidor do Analysis Services especificada na propriedade de Servidor de Implantação. Para obter mais informações sobre a propriedade Servidor de Implantação, consulte [Propriedades de projeto &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/project-properties-ssas-tabular.md).  
  
 O banco de dados de espaço de trabalho modelo geralmente reside no host local ou uma instância nomeada local de um servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Você pode usar uma instância remota do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para hospedar o banco de dados de espaço de trabalho, no entanto, esta configuração não é recomendada devido à latência durante consulta de dados e outras restrições. Idealmente, a instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que hospedará os bancos de dados de espaço de trabalho está no mesmo computador que o [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Criar projetos de modelo no mesmo computador que a instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que hospeda o banco de dados de espaço de trabalho pode melhorar o desempenho.  
  
 Bancos de dados de espaço de trabalho remotos têm as seguintes restrições:  
  
-   Latência potencial durante consultas.  
  
-   A propriedade Backup de Dados não pode ser definida como **Backup em disco**.  
  
-   Você não pode importar dados de uma pasta de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ao criar um novo projeto de modelo tabular usando a Importação do modelo de projeto do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
  > [!IMPORTANT]  
>  O nível de compatibilidade do modelo e o Servidor de Espaço de Trabalho devem corresponder.
  
> [!NOTE]  
>  Se alguma das tabelas em seu modelo contiver um número grande de linhas, importe somente um subconjunto dos dados durante a criação do modelo. Ao importar um subconjunto dos dados, você poderá reduzir o tempo de processamento e o consumo de recursos do servidor de banco de dados do espaço de trabalho.  
  
> [!NOTE]  
>  A janela de visualização na página Selecionar tabelas e exibições no Assistente de Importação de Tabela, caixa de diálogo Editar Propriedades da Tabela e caixa de diálogo Gerenciador de Partições mostra tabelas, colunas e linhas à fonte de dados e pode não mostrar as mesmas tabelas, colunas e linhas que o banco de dados de espaço de trabalho.  
  
  
##  <a name="bkmk_ws_prop"></a> Propriedades de Banco de Dados de Espaço de Trabalho  
 As propriedades de banco de dados de espaço de trabalho são incluídas nas propriedades modelo. Para exibir propriedades de modelo, no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], no **Gerenciador de Soluções**, clique no arquivo **Model.bim** . As propriedades do modelo podem ser configuradas usando a janela **Propriedades** . As propriedades específicas do banco de dados de espaço de trabalho incluem:  
  
> [!NOTE]  
>  As propriedades **Modo de Espaço de Trabalho Integrado**, **Servidor do Espaço de Trabalho**, **Retenção do Espaço de Trabalho**, e **Backup de Dados** têm configurações padrão aplicadas quando você cria um novo projeto de modelo. Você pode alterar as configurações padrão para novos projetos de modelos na página **Modelagem de Dados** nas configurações do **Analysis Server** na caixa de diálogo Ferramentas\Opções. Estas propriedades, assim como outras, também podem ser definidas para cada projeto de modelo na janela **Propriedades** . Alterar as configurações padrão não se aplicará a projetos de modelo já criados. Para obter mais informações, consulte [Configurar propriedades padrão de implantação e modelagem de dados &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md).  
  
|Propriedade|Configuração padrão|Description|  
|--------------|---------------------|-----------------|  
|**Modo de Espaço de Trabalho Integrado**|Verdadeiro, Falso|Se o modo de trabalho integrado for selecionado para o banco de dados do espaço de trabalho quando o projeto for criado, essa propriedade será Verdadeira. Se o modo do **Servidor de Espaço de Trabalho** for selecionado quando o projeto for criado, essa propriedade será Falsa. | 
|**Banco de Dados do Espaço de Trabalho**|Nome|O nome do banco de dados de espaço de trabalho. Essa propriedade não pode ser editada quando o **Modo de Espaço de Trabalho Integrado** é **Verdadeiro**.|  
|**Retenção de Espaço de Trabalho**|Descarregar da memória|Especifica como um banco de dados de espaço de trabalho é retido depois que um projeto de modelo é fechado. Um banco de dados de espaço de trabalho inclui metadados modelo e dados importados. Em alguns casos, o banco de dados de espaço de trabalho pode ser muito grande e consumir uma grande quantidade de memória. Por padrão, quando você fecha um projeto de modelo no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], o banco de dados de espaço de trabalho é descarregado da memória. Ao alterar essa configuração, é importante considerar os recursos de memória disponíveis, bem como a frequência na qual você planeja trabalhar no projeto de modelo. Essa configuração de propriedade tem as seguintes opções:<br /><br /> **Manter na memória** – Especifica manter o banco de dados de espaço de trabalho na memória depois que um projeto de modelo é fechado. Essa opção consumirá mais memória. No entanto, ao abrir um projeto de modelo no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], menos recursos serão consumidos e o banco de dados do espaço de trabalho será carregado mais rapidamente.<br /><br /> **Descarregar da memória** – Especifica manter banco de dados de espaço de trabalho em disco, e não mais na memória depois que um projeto de modelo é fechado. Essa opção consumirá menos memória. No entanto, ao abrir um projeto de modelo no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], o banco de dados de espaço de trabalho deve ser reanexado; recursos adicionais serão consumidos e o projeto de modelo será carregado mais lentamente do que se o banco de dados de espaço de trabalho fosse mantido na memória. Use essa opção quando os recursos de memória forem limitados ou ao trabalhar em um banco de dados de espaço de trabalho remoto.<br /><br /> **Excluir espaço de trabalho** – Especifica excluir o banco de dados de espaço de trabalho da memória e não manter banco de dados de espaço de trabalho em disco depois que o projeto de modelo é fechado. Essa opção consumirá menos memória e espaço de armazenamento. No entanto, ao abrir um projeto de modelo no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], serão consumidos recursos adicionais e o projeto de modelo será carregado mais lentamente do que se o banco de dados de espaço de trabalho fosse mantido na memória ou no disco. Use essa opção apenas ao trabalhar ocasionalmente em projetos modelo.<br /><br /> A configuração padrão para essa propriedade pode ser alterada na página **Modelagem de Dados** nas configurações do **Analysis Server** na caixa de diálogo Ferramentas\Opções. Essa propriedade não pode ser editada quando o **Modo de Espaço de Trabalho Integrado** é **Verdadeiro**.|  
|**Workspace Server**|localhost|Essa propriedade especifica o servidor fora-de-processo padrão que será usado para hospedar o banco de dados de espaço de trabalho enquanto o projeto de modelo é criado no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Todas as instâncias disponíveis do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que executam no computador local são incluídas na caixa de listagem.<br /><br /> Para especificar um servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] diferente (executando em modo Tabular), digite o nome do servidor. O usuário conectado deve ser Administrador no servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .<br /><br /> Observe que é recomendado a especificação de um servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] local como o servidor de espaço de trabalho. Para bancos de dados de espaços de trabalho em um servidor remoto, não há suporte para a importação do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , o backup dos dados não pode ser feito localmente e a interface do usuário pode experimentar latência durante consultas.<br /><br /> A configuração padrão para essa propriedade pode ser alterada na página Modelagem de Dados nas configurações do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] na caixa de diálogo Ferramentas\Opções. Essa propriedade não pode ser editada quando o **Modo de Espaço de Trabalho Integrado** é **Verdadeiro**.|  
  
##  <a name="bkmk_use_ssms"></a> Usando SSMS para gerenciar o banco de dados de espaço de trabalho  
 Você pode usar o SQL Server Management Studio (SSMS) para se conectar a um servidor [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que hospeda um banco de dados do espaço de trabalho. Normalmente, não há gerenciamento do banco de dados de espaço de trabalho necessário; a exceção é desanexar ou excluir um banco de dados de espaço de trabalho, o que deve ser feito no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Não use o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para gerenciar o banco de dados de espaço de trabalho enquanto o projeto estiver aberto no designer de modelo. Fazer isso poderia causar a perda de dados.
   
## <a name="see-also"></a>Consulte também  
[Propriedades de modelo &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/model-properties-ssas-tabular.md) 
  
  
