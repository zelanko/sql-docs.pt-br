---
title: "N&#237;vel de compatibilidade para modelos de tabela no Analysis Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.asvs.bidtoolset.versioncompat.f1"
ms.assetid: 8943d78d-4a73-4be8-ad14-3d428f5abd06
caps.latest.revision: 27
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 27
---
# N&#237;vel de compatibilidade para modelos de tabela no Analysis Services
  O *nível de compatibilidade* de um modelo ou banco de dados se refere a um conjunto de comportamentos específicos à versão no mecanismo do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Você pode criar modelos em qualquer nível de compatibilidade com suporte a fim de obter comportamentos de uma determinada versão. Por exemplo, o DirectQuery e os metadados de objeto de tabela têm implementações diferentes dependendo da atribuição de nível de compatibilidade.  
  
 **SQL Server 2016 RTM (1200)**, ou o nível de compatibilidade 1200 para abreviar, é uma novidade no SQL Server 2016 e aplica-se somente aos modelos de tabela.  Modelos de tabela no nível de compatibilidade 1200 serão executados somente em uma instância de tabela do [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] .  
  
 Para criar ou atualizar um modelo de tabela, use o SSDT (SQL Server Data Tools) e defina a propriedade **Nível de Compatibilidade** ao criar o projeto ou o arquivo **model.bim** após a criação do projeto.  
  
> [!NOTE]  
>  Modelos multidimensionais seguem um caminho de versão independente em termos de níveis de compatibilidade. Quando os números são iguais, como é o caso com o 1103, é uma coincidência. Consulte [Nível de compatibilidade de um banco de dados multidimensional &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md) para obter mais informações.  
  
## Níveis de compatibilidade com suporte para bancos de dados de modelo de tabela  
 O Analysis Services oferece suporte aos seguintes níveis de compatibilidade, aplicáveis aos modelos e bancos de dados:  A versão da ferramenta usada para criar um modelo determina se os níveis mais altos de compatibilidade estão disponíveis.  
  
||||  
|-|-|-|  
|nível de compatibilidade|Versão do servidor __|Versão da ferramenta de modelagem|  
|1200|É executado em apenas instâncias do SQL Server 2016|[Somente SQL Server Data Tools para Visual Studio 2015](http://go.microsoft.com/fwlink/?LinkID=690931) <sup>1</sup><br /><br /> [What's New in Analysis Services](../../analysis-services/what-s-new-in-analysis-services.md) descreve a funcionalidade disponível neste nível.|  
|1103|SQL Server 2016<br /><br /> SQL Server 2014<br /><br /> SQL Server 2012 SP1|[SQL Server Data Tools para Visual Studio 2015](http://go.microsoft.com/fwlink/?LinkID=690931) <sup>2</sup><br /><br /> [SQL Server Data Tools para Business Intelligence (Visual Studio 2013)](https://www.microsoft.com/en-us/download/details.aspx?id=42313)<br /><br /> [SQL Server Data Tools para Business Intelligence (Visual Studio 2012)](http://www.microsoft.com/en-us/download/details.aspx?id=36843)|  
|1100|SQL Server 2016<br /><br /> SQL Server 2014<br /><br /> SQL Server 2012 SP1<br /><br /> SQL Server 2012|[SQL Server Data Tools para Visual Studio 2015](http://go.microsoft.com/fwlink/?LinkID=690931) <sup>1</sup><br /><br /> [SQL Server Data Tools para Business Intelligence (Visual Studio 2013)](https://www.microsoft.com/en-us/download/details.aspx?id=42313)<br /><br /> [SQL Server Data Tools para Business Intelligence (Visual Studio 2012)](http://www.microsoft.com/en-us/download/details.aspx?id=36843)<br /><br /> Business Intelligence Development Studio (executado no shell do Visual Studio 2010 e instalado por meio da Configuração do SQL Server)|  
  
 <sup>1</sup> Você pode usar o SQL Server Data Tools para Visual Studio 2015 para implantar um modelo de tabela 1103 ou 1100 em versões anteriores do Analysis Services.  
  
 <sup>2</sup> Os níveis de compatibilidade 1100, 1103 e 1200 são válidos para projetos de modelo de tabela no SQL Server Data Tools para Visual Studio 2015, mas você só pode implantar e executar um modelo 1200 em uma instância do SQL Server 2016 do Analysis Services.  
  
## Definir o nível de compatibilidade ao criar ou atualizar uma tabela no SSDT  
 Ao criar um novo projeto de modelo de tabela no SSDT (SQL Server Data Tools), na caixa de diálogo de opções **Novo projeto de tabela**, você pode especificar o nível de compatibilidade:  
  
 ![ssas_tabularproject_compat1200](../../analysis-services/tabular-models/media/ssas-tabularproject-compat1200.jpg "ssas_tabularproject_compat1200")  
  
 Você também pode especificar um nível de compatibilidade padrão selecionando a opção **Não mostrar esta mensagem novamente** . Todos os projetos subsequentes usarão o nível de compatibilidade especificado. É possível alterar o nível de compatibilidade padrão no SSDT em **Ferramentas** > **Opções**.  
  
 Para atualizar um projeto de modelo de tabela, defina a propriedade **Nível de Compatibilidade** na janela **Propriedades** do modelo como **SQL Server 2016 RTM (1200)**.  Consulte [Upgrade Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md) para obter mais informações.  
  
> [!NOTE]  
>  Uma maneira de criar um modelo de tabela é baseá-lo em uma pasta de trabalho importada do Power Pivot. Por padrão, o Power BI Desktop cria automaticamente os modelos de tabela no nível de compatibilidade 1200. No entanto, versões anteriores de pastas de trabalho do Power Pivot podem estar no nível 1100. Ao usar uma pasta de trabalho mais antiga, lembre-se de alterar a propriedade **Nível de Compatibilidade** para atualizá-la.  
  
## Verificar o nível de compatibilidade de um banco de dados no SSMS  
 No SSMS, clique com o botão direito do mouse no nome do banco de dados > **Propriedades** > **propriedade Nível de Compatibilidade**.  
  
## Verificar o nível de compatibilidade com suporte para um servidor no SSMS  
 No SSMS, clique com o botão direito do mouse no nome do servidor > **Propriedades** > **Nível de Compatibilidade com Suporte**.  
  
 Essa propriedade especifica o mais alto nível de compatibilidade de um banco de dados que será executados no servidor.  O nível de compatibilidade com suporte é somente leitura e não pode ser alterado.  
  
## Consulte também  
 [Nível de compatibilidade de um banco de dados multidimensional &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)   
 [Novidades do Analysis Services](../../analysis-services/what-s-new-in-analysis-services.md)   
 [Importar do PowerPivot &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/import-from-power-pivot-ssas-tabular.md)   
 [Criar um novo projeto de modelo de tabela &#40;Analysis Services&#41;](../../analysis-services/tabular-models/create-a-new-tabular-model-project-analysis-services.md)  
  
  