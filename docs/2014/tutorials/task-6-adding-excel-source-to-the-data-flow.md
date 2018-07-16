---
title: 'Tarefa 6: Adicionando a origem do Excel ao fluxo de dados | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 0209055e-cb6b-4a07-909e-836596727a2c
caps.latest.revision: 6
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2ce6d1ec5ab2fc9c57bd56e12b56b13231e74606
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37279992"
---
# <a name="task-6-adding-excel-source-to-the-data-flow"></a>Tarefa 6: Adicionando a origem do Excel ao fluxo de dados
  Nesta tarefa, você adicionará uma Origem do Excel ao fluxo de dados para ler dados do fornecedor do arquivo de origem do Excel. A Origem do Excel extrai dados de planilhas ou intervalos em pastas de trabalho do Microsoft Excel. Consulte o tópico [Origem do Excel](http://msdn.microsoft.com/library/ms141683.aspx) para obter mais detalhes.  
  
1.  Arraste e solte **Origem do Excel** de **Outras Origens** na **Caixa de Ferramentas do SSIS** para a guia **Fluxo de Dados** .  
  
2.  Clique com o botão direito do mouse em **Origem do Excel** na guia **Fluxo de Dados** e clique em **Renomear**.  
  
3.  Digite **Ler Dados do Fornecedor de Arquivo do Excel** e pressione **ENTER**.  
  
4.  Clique duas vezes em **Ler Dados do Fornecedor de Arquivo do Excel** para iniciar a caixa de diálogo de **Editor de Origem do Excel** .  
  
5.  Na caixa de diálogo **Editor de Origem do Excel** , clique em **Novo** para criar uma conexão do Excel.  
  
6.  Na caixa de diálogo **Gerenciador de Conexões do Excel** , clique em **Procurar**e selecione o arquivo **Suppliers.xls** na pasta **Tutorial do EIM** . Confirme se a opção **Microsoft Excel 97-2003** está selecionada na caixa **Versão do Excel** e clique em **OK**.  
  
     ![Caixa de diálogo Gerenciador de Conexão do Excel](../../2014/tutorials/media/et-addingexcelsourcetothedataflow-01.jpg "caixa de diálogo Gerenciador de Conexão do Excel")  
  
7.  Na caixa de diálogo **Editor de Origem do Excel** , selecione **IncomingSuppliers$** na caixa de listagem **Nome da planilha do Excel** .  
  
     ![Nome da planilha do Excel - fornecedores de entrada $](../../2014/tutorials/media/et-addingexcelsourcetothedataflow-02.jpg "nome da planilha do Excel - fornecedores de entrada $")  
  
8.  Clique em **Visualizar** para visualizar os dados no arquivo do Excel.  
  
9. Clique em **OK** para fechar a caixa de diálogo.  
  
10. Arraste e solte a transformação **Limpeza DQS** em **Outras Transformações** na **Caixa de Ferramentas do SSIS** para a guia **Fluxo de Dados** em **Ler Dados do Fornecedor de Arquivo do Excel**. A transformação Limpeza DQS usa o DQS (Data Quality Services) para corrigir dados aplicando regras aprovadas na base de dados de conhecimento. Essa transformação, em tempo de execução, cria um projeto de limpeza DQS no servidor DQS. Consulte o tópico [Transformação Limpeza DQS](http://msdn.microsoft.com/library/ee677619.aspx) para obter mais detalhes.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 7: Adicionando a Transformação de Limpeza DQS ao fluxo de dados](../integration-services/data-flow/data-flow.md)  
  
  
