---
title: 'Tarefa 6: adicionando a origem do Excel ao fluxo de dados | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 0209055e-cb6b-4a07-909e-836596727a2c
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 92a4c3e650ce375a1e80079bbad83c5ab2b9bcd9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68495288"
---
# <a name="task-6-adding-excel-source-to-the-data-flow"></a>Tarefa 6: Adicionando a origem do Excel ao fluxo de dados
  Nesta tarefa, você adicionará uma Origem do Excel ao fluxo de dados para ler dados do fornecedor do arquivo de origem do Excel. A Origem do Excel extrai dados de planilhas ou intervalos em pastas de trabalho do Microsoft Excel. Consulte o tópico [Origem do Excel](../integration-services/data-flow/excel-source.md) para obter mais detalhes.  
  
1.  Arraste e solte **Origem do Excel** de **Outras Origens** na **Caixa de Ferramentas do SSIS** para a guia **Fluxo de Dados** .  
  
2.  Clique com o botão direito do mouse em **Origem do Excel** na guia **Fluxo de Dados** e clique em **Renomear**.  
  
3.  Digite **Ler Dados do Fornecedor de Arquivo do Excel** e pressione **ENTER**.  
  
4.  Clique duas vezes em **Ler Dados do Fornecedor de Arquivo do Excel** para iniciar a caixa de diálogo de **Editor de Origem do Excel** .  
  
5.  Na caixa de diálogo **Editor de Origem do Excel** , clique em **Novo** para criar uma conexão do Excel.  
  
6.  Na caixa de diálogo **Gerenciador de Conexões do Excel** , clique em **Procurar**e selecione o arquivo **Suppliers.xls** na pasta **Tutorial do EIM** . Confirme se a opção **Microsoft Excel 97-2003** está selecionada na caixa **Versão do Excel** e clique em **OK**.  
  
     ![Caixa de diálogo Gerenciador de Conexões do Excel](../../2014/tutorials/media/et-addingexcelsourcetothedataflow-01.jpg "Caixa de diálogo Gerenciador de Conexões do Excel")  
  
7.  Na caixa de diálogo **Editor de Origem do Excel** , selecione **IncomingSuppliers$** na caixa de listagem **Nome da planilha do Excel** .  
  
     ![Nome da planilha do Excel - Fornecedores de Entrada$](../../2014/tutorials/media/et-addingexcelsourcetothedataflow-02.jpg "Nome da planilha do Excel - Fornecedores de Entrada$")  
  
8.  Clique em **Visualizar** para visualizar os dados no arquivo do Excel.  
  
9. Clique em **OK** para fechar a caixa de diálogo.  
  
10. Arraste e solte a transformação **Limpeza DQS** em **Outras Transformações** na **Caixa de Ferramentas do SSIS** para a guia **Fluxo de Dados** em **Ler Dados do Fornecedor de Arquivo do Excel**. A transformação Limpeza DQS usa o DQS (Data Quality Services) para corrigir dados aplicando regras aprovadas na base de dados de conhecimento. Essa transformação, em runtime, cria um projeto de limpeza DQS no servidor DQS. Consulte o tópico [Transformação Limpeza DQS](https://msdn.microsoft.com/library/ee677619.aspx) para obter mais detalhes.  
  
## <a name="next-step"></a>Próxima etapa

[Tarefa 7: Adicionando a Transformação de Limpeza DQS ao fluxo de dados](task-7-adding-dqs-cleansing-transform-to-the-data-flow.md)  

### <a name="see-also"></a>Consulte Também

[Fluxo de Dados](../integration-services/data-flow/data-flow.md)  
