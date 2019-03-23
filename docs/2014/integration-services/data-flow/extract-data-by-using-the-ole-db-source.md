---
title: Extrair dados por meio da origem OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- extracting data [Integration Services]
- sources [Integration Services], OLE DB
- OLE DB source [Integration Services]
ms.assetid: 4ca6eeb5-b60e-4b81-86dd-0674be8ae8d8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8303cc8e30a9099a11a43cc2b4bfac341873a044
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58388844"
---
# <a name="extract-data-by-using-the-ole-db-source"></a>Extrair dados por meio da origem OLE DB
  Para adicionar e configurar uma origem OLE DB, o pacote já deve incluir pelo menos uma tarefa de Fluxo de Dados.  
  
### <a name="to-extract-data-using-an-ole-db-source"></a>Para extrair dados usando uma Origem OLE DB  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Dados** e, na **Caixa de Ferramentas**, arraste a fonte OLE DB para a superfície de design.  
  
4.  Clique duas vezes na origem OLE DB.  
  
5.  Na caixa de diálogo **Editor de Origem OLE DB** , na página **Gerenciador de Conexões** , selecione um gerenciador de conexões OLE DB existente ou clique em **Novo** para criar um gerenciador de conexões novo. Para obter mais informações, consulte [OLE DB Connection Manager](../connection-manager/ole-db-connection-manager.md).  
  
6.  Selecione o método de acesso de dados:  
  
    -   **Tabela ou exibição** Selecione uma tabela ou uma exibição no banco de dados com a qual o gerenciador de conexões OLE DB se conecta.  
  
    -   **Variável de nome da tabela ou exibição** Selecione a variável definida pelo usuário que contém o nome da tabela ou da exibição no banco de dados com a qual o gerenciador de conexões OLE DB se conecta.  
  
    -   **Comando SQL** Digite um comando SQL ou clique em **Construir Consulta** para escrever um comando SQL usando o **Construtor de Consultas**.  
  
        > [!NOTE]  
        >  O comando pode incluir parâmetros. Para obter mais informações, consulte [Mapear parâmetros de consulta para variáveis em um componente de fluxo de dados](map-query-parameters-to-variables-in-a-data-flow-component.md).  
  
    -   **Comando SQL da variável** Selecione a variável definida pelo usuário que contém o comando SQL.  
  
        > [!NOTE]  
        >  As variáveis devem ser definidas no escopo da mesma tarefa Fluxo de Dados que contém a origem OLE DB ou no escopo do mesmo pacote, além disso, a variável deve ter um tipo de dados de cadeia de caracteres.  
  
7.  Para atualizar o mapeamento entre colunas externas e de saída, clique em **Colunas** e selecione colunas diferentes na lista **Coluna Externa** .  
  
8.  Como opção, atualize os nomes de colunas de saída editando valores na lista **Coluna de Saída** .  
  
9. Para configurar a saída de erro, clique em **Saída de Erro**. Para obter mais informações, consulte [Configurar uma saída de erro em um componente de fluxo de dados](../configure-an-error-output-in-a-data-flow-component.md).  
  
10. É possível clicar em **Visualizar** para exibir até 200 linhas dos dados extraídos pela origem OLE DB.  
  
11. Clique em **OK**.  
  
12. Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
## <a name="see-also"></a>Consulte também  
 [Origem de OLE DB](ole-db-source.md)   
 [Transformações do Integration Services](transformations/integration-services-transformations.md)   
 [Caminhos do Integration Services](integration-services-paths.md)   
 [Tarefa de Fluxo de Dados](../control-flow/data-flow-task.md)  
  
  
