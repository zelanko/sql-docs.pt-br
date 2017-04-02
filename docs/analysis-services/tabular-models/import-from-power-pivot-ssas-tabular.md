---
title: "Importar do PowerPivot (SSAS de tabela) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
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
  - "sql13.asvs.bidtoolset.importfromppt.f1"
ms.assetid: ac1a6a79-bda3-4122-a717-8b1e2f77da02
caps.latest.revision: 25
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 25
---
# Importar do PowerPivot (SSAS de tabela)
  Este tópico descreve como criar um novo projeto de modelo tabular importando os metadados e dados de uma pasta de trabalho [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] usando o modelo de projeto Importar do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
## Criar um novo Modelo Tabular de um arquivo PowerPivot para Excel  
 Ao criar um novo projeto de modelo tabular importando de uma pasta de trabalho [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , os metadados que definem a estrutura da pasta de trabalho são usados para criar e definir a estrutura do projeto de modelo de tabela no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Objetos como tabelas, colunas, medidas e relações são mantidos e aparecerão no projeto de modelo tabular tal como estão na pasta de trabalho [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Nenhuma alteração é feita ao arquivo da pasta de trabalho .xlsx.  
  
> [!NOTE]  
>  Modelos tabulares não dão suporte a tabelas vinculadas. Ao importar de uma pasta de trabalho [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que contém uma tabela vinculada, os dados de tabela vinculada são tratados como dados copiados\colados e armazenados no arquivo Model.bim. Ao exibir as propriedades para uma tabela copiada\colada, a propriedade **Dados de Origem** é desabilitada e a caixa de diálogo **Propriedades da Tabela** no menu **Tabela** é desabilitada.  
>   
>  Há um limite de 10.000 linhas que podem ser adicionadas aos dados inseridos no modelo. Se você importar um modelo do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e o erro “Os dados estavam truncados. As tabelas coladas não podem conter mais de 10.000 linhas” surgir, revise o modelo do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] movendo os dados inseridos para outra fonte de dados, como uma tabela do SQL Server, e importe-os novamente.  
  
 Há considerações especiais dependendo se o banco de dados de espaço de trabalho está em uma instância do Analysis Services no mesmo computador (local) que o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ou está em uma instância remota do Analysis Services.  
  
 Se o banco de dados do espaço de trabalho estiver em uma instância local do Analysis Services, você poderá importar os metadados e os dados da pasta de trabalho [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Os metadados são copiados da pasta de trabalho e usados para criar o projeto de modelo tabular. Os dados são então copiados da pasta de trabalho e armazenados no banco de dados de espaço de trabalho do projeto (com exceção dos dados copiados/colados, que são armazenados no arquivo Model.bim).  
  
 Se o banco de dados de espaço de trabalho estiver em uma instância remota do Analysis Services, você não poderá importar os dados da pasta de trabalho [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para Excel. Você ainda poderá importar os metadados da pasta de trabalho; porém, isto fará um script ser executado na instância remota do Analysis Services. Você só deve importar metadados de uma pasta de trabalho confiável do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Os dados devem ser importados de origens definidas nas conexões da fonte de dados. Os dados copiados/colados e de tabela vinculada na pasta de trabalho [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] devem ser copiados e colados no projeto de modelo tabular.  
  
#### Para criar um novo projeto de modelo tabular de um arquivo PowerPivot para Excel  
  
1.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], no menu **Arquivo** , clique em **Novo**e, em seguida, em **Projeto**.  
  
2.  Na caixa de diálogo **Novo Projeto**, em **Modelos Instalados**, clique em **Business Intelligence** e clique em **Importar do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]**.  
  
3.  Em  **Nome**, digite um nome para o projeto e especifique um local e um nome para a solução e clique em **OK**.  
  
4.  Na caixa de diálogo **Abrir** , selecione o arquivo do [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] que contém os metadados e dados modelo que você deseja importar e clique em **Abrir**.  
  
## Consulte também  
 [Banco de dados de espaço de trabalho &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/workspace-database-ssas-tabular.md)   
 [Copiar e colar dados &#40;SSAS Tabular&#41;](../../analysis-services/tabular-models/copy-and-paste-data-ssas-tabular.md)  
  
  