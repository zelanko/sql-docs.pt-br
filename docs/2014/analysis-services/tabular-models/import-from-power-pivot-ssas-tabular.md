---
title: Importar do PowerPivot (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.importfromppt.f1
ms.assetid: ac1a6a79-bda3-4122-a717-8b1e2f77da02
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 867d476c0132bedf39f709497e035b8264f2b022
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52390601"
---
# <a name="import-from-powerpivot-ssas-tabular"></a>Importar do PowerPivot (SSAS tabular)
  Este tópico descreve como você pode criar um novo projeto de modelo de tabela importando os metadados e dados de uma pasta de trabalho PowerPivot usando o modelo de projeto Importar do PowerPivot no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
## <a name="create-a-new-tabular-model-from-a-powerpivot-for-excel-file"></a>Crie um novo Modelo Tabular de um arquivo PowerPivot para Excel  
 Ao criar um novo projeto de modelo tabular importando de uma pasta de trabalho PowerPivot, os metadados que definem a estrutura da pasta de trabalho são usados para criar e definir a estrutura do projeto de modelo tabular no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Objetos como tabelas, colunas, medidas e relações são mantidos e aparecerão no projeto de modelo tabular como estão na pasta de trabalho PowerPivot. Nenhuma alteração é feita ao arquivo da pasta de trabalho .xlsx.  
  
> [!NOTE]  
>  Modelos tabulares não dão suporte a tabelas vinculadas. Ao importar de uma pasta de trabalho PowerPivot que contém uma tabela vinculada, os dados de tabela vinculada são tratados como dados copiados\colados e armazenados no arquivo Model.bim. Ao exibir as propriedades para uma tabela copiada\colada, a propriedade **Dados de Origem** é desabilitada e a caixa de diálogo **Propriedades da Tabela** no menu **Tabela** é desabilitada.  
>   
>  Há um limite de 10.000 linhas que podem ser adicionadas aos dados inseridos no modelo. Se você importar um modelo do PowerPivot e o erro "os dados estavam truncados. As tabelas coladas não podem conter mais de 10.000 linhas"você deve revisar o modelo do PowerPivot movendo os dados inseridos para outra fonte de dados, como uma tabela no SQL Server e, em seguida, importe novamente.  
  
 Há considerações especiais dependendo se o banco de dados de workspace está em uma instância do Analysis Services no mesmo computador (local) que o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ou está em uma instância remota do Analysis Services.  
  
 Se o banco de dados de workspace estiver em uma instância local do Analysis Services, você poderá importar os metadados e os dados da pasta de trabalho PowerPivot. Os metadados são copiados da pasta de trabalho e usados para criar o projeto de modelo tabular. Os dados, em seguida, são copiados da pasta de trabalho e armazenados no banco de dados de espaço de trabalho do projeto (com exceção de copiados/colados, que são armazenados no arquivo Model. BIM).  
  
 Se o banco de dados de workspace estiver em uma instância remota do Analysis Services, você não poderá importar os dados da pasta de trabalho PowerPivot para Excel. Você ainda poderá importar os metadados da pasta de trabalho; porém, isto fará um script ser executado na instância remota do Analysis Services. Você só deve importar metadados de uma pasta de trabalho confiável do PowerPivot. Os dados devem ser importados de origens definidas nas conexões da fonte de dados. Os dados copiados/colados e de tabela vinculada na pasta de trabalho PowerPivot devem ser copiados e colados no projeto de modelo tabular.  
  
#### <a name="to-create-a-new-tabular-model-project-from-a-powerpivot-for-excel-file"></a>Para criar um novo projeto de modelo tabular de um arquivo PowerPivot para Excel  
  
1.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], no menu **Arquivo** , clique em **Novo**e, em seguida, em **Projeto**.  
  
2.  No **novo projeto** caixa de diálogo **modelos instalados**, clique em **Business Intelligence**e, em seguida, clique em **importar do PowerPivot**.  
  
3.  Em  **Nome**, digite um nome para o projeto e especifique um local e um nome para a solução e clique em **OK**.  
  
4.  Na caixa de diálogo **Abrir** , selecione o arquivo do [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] que contém os metadados e dados modelo que você deseja importar e clique em **Abrir**.  
  
## <a name="see-also"></a>Consulte também  
 [Banco de dados de workspace &amp;#40;SSAS de Tabela&amp;#41;](workspace-database-ssas-tabular.md)   
 [Copiar e colar dados &#40;SSAS Tabular&#41;](../copy-and-paste-data-ssas-tabular.md)  
  
  
