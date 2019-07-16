---
title: Importar do PowerPivot no Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 21abcfbec94808df6560af887ff0598d97fcb068
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68207670"
---
# <a name="import-from-power-pivot"></a>Importar do PowerPivot 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Este artigo descreve como criar um novo projeto de modelo tabular importando os metadados e dados de um [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] usando a importação da pasta de trabalho [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] modelo de projeto em [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
## <a name="create-a-new-tabular-model-from-a-power-pivot-for-excel-file"></a>Criar um novo Modelo Tabular de um arquivo PowerPivot para Excel  
 Ao criar um novo projeto de modelo tabular importando de uma pasta de trabalho [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , os metadados que definem a estrutura da pasta de trabalho são usados para criar e definir a estrutura do projeto de modelo de tabela no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Objetos como tabelas, colunas, medidas e relações são mantidos e aparecerão no projeto de modelo tabular tal como estão na pasta de trabalho [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Nenhuma alteração é feita ao arquivo da pasta de trabalho .xlsx.  
  
> [!NOTE]  
>  Modelos tabulares não dão suporte a tabelas vinculadas. Ao importar de uma pasta de trabalho [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que contém uma tabela vinculada, os dados de tabela vinculada são tratados como dados copiados\colados e armazenados no arquivo Model.bim. Ao exibir as propriedades para uma tabela copiada\colada, a propriedade **Dados de Origem** é desabilitada e a caixa de diálogo **Propriedades da Tabela** no menu **Tabela** é desabilitada.  
>   
>  Há um limite de 10.000 linhas que podem ser adicionadas aos dados inseridos no modelo. Se você importar um modelo de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e ver o erro "os dados estavam truncados. As tabelas coladas não podem conter mais de 10.000 linhas"surgir, revise o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] de modelo, movendo os dados inseridos para outra fonte de dados, como uma tabela no SQL Server e, em seguida, importe novamente.  
  
 Há considerações especiais dependendo se o banco de dados de workspace está em uma instância do Analysis Services no mesmo computador (local) que o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ou está em uma instância remota do Analysis Services.  
  
 Se o banco de dados do workspace estiver em uma instância local do Analysis Services, você poderá importar os metadados e os dados da pasta de trabalho [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]. Os metadados são copiados da pasta de trabalho e usados para criar o projeto de modelo tabular. Os dados, em seguida, são copiados da pasta de trabalho e armazenados no banco de dados de espaço de trabalho do projeto (com exceção de copiados/colados, que são armazenados no arquivo Model. BIM).  
  
 Se o banco de dados de workspace estiver em uma instância remota do Analysis Services, você não poderá importar os dados da pasta de trabalho [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para Excel. Você ainda poderá importar os metadados da pasta de trabalho; porém, isto fará um script ser executado na instância remota do Analysis Services. Você só deve importar metadados de uma pasta de trabalho confiável do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Os dados devem ser importados de origens definidas nas conexões da fonte de dados. Os dados copiados/colados e de tabela vinculada na pasta de trabalho [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] devem ser copiados e colados no projeto de modelo tabular.  
  
#### <a name="to-create-a-new-tabular-model-project-from-a-power-pivot-for-excel-file"></a>Para criar um novo projeto de modelo tabular de um arquivo PowerPivot para Excel  
  
1.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], no menu **Arquivo** , clique em **Novo**e, em seguida, em **Projeto**.  
  
2.  Na caixa de diálogo **Novo Projeto**, em **Modelos Instalados**, clique em **Business Intelligence** e clique em **Importar do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]** .  
  
3.  Em  **Nome**, digite um nome para o projeto e especifique um local e um nome para a solução e clique em **OK**.  
  
4.  Na caixa de diálogo **Abrir** , selecione o arquivo do [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] que contém os metadados e dados modelo que você deseja importar e clique em **Abrir**.  
  
## <a name="see-also"></a>Consulte também  
 [Banco de dados do espaço de trabalho](../../analysis-services/tabular-models/workspace-database-ssas-tabular.md)   
 [Copiar e colar dados](../../analysis-services/tabular-models/ssas-import-data-copy-and-paste-data.md)  
  
  
