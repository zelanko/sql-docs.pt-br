---
title: Carregar dados por meio do destino OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- loading data
- OLE DB destination [Integration Services]
- destinations [Integration Services], OLE DB
ms.assetid: 78899498-725e-4300-a7af-f983f4ea384b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: dd23184f25ff8083bdfffbb46ef8c5b5f5f91eae
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58281230"
---
# <a name="load-data-by-using-the-ole-db-destination"></a>Carregar dados por meio do destino OLE DB
  Para adicionar e configurar um destino OLE DB, o pacote já deve incluir pelo menos uma tarefa de Fluxo de Dados e uma fonte.  
  
### <a name="to-load-data-using-an-ole-db-destination"></a>Para carregar dados usando um destino OLE DB  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Dados** e em seguida, da **Caixa de Ferramentas**arraste o destino OLE DB para a superfície de design.  
  
4.  Conecte o destino OLE DB a um fluxo de dados arrastando um conector de uma fonte de dados, ou de uma transformação anterior, para o destino.  
  
5.  Clique duas vezes sobre o destino OLE DB.  
  
6.  Na caixa de diálogo **Editor de Destino OLE DB** , na página **Gerenciador de Conexões** , selecione um gerenciador de conexões OLE DB existente ou clique em **Novo** para criar um gerenciador de conexões novo. Para obter mais informações, consulte [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
7.  Selecione o método de acesso de dados:  
  
    -   **Tabela ou exibição** Selecione uma tabela ou exibição no banco de dados que contém os dados.  
  
    -   **Tabela ou exibição – carregamento rápido** Selecione uma tabela ou exibição no banco de dados que contém os dados, depois defina as opções de carregamento rápido: **Manter identidade**, **Manter nulos**, **Bloqueio de tabela**, **Restrição de verificação**, **Linhas por lote** ou **Tamanho máximo de confirmação de inserção**.  
  
    -   **Variável de nome da tabela ou exibição** Selecione a variável definida pelo usuário que contém o nome da tabela ou da exibição no banco de dados.  
  
    -   **Variável de nome da tabela ou exibição – carregamento rápido** Selecione a variável definida pelo usuário que contém o nome de uma tabela ou exibição no banco de dados que contém os dados e em seguida defina as opções de carregamento rápido.  
  
    -   **Comando SQL** Digite um comando SQL ou clique em **Construir Consulta** para escrever um comando SQL usando o **Construtor de Consultas**.  
  
8.  Clique em **Mapeamentos** e mapeie as colunas da lista **Colunas de Entrada Disponíveis** para as colunas da lista **Colunas de Destino Disponíveis** arrastando as colunas de uma lista para outra.  
  
    > [!NOTE]  
    >  O destino OLE DB mapeia automaticamente as colunas de mesmo nome.  
  
9. Para configurar a saída de erro, clique em **Saída de Erro**. Para obter mais informações, consulte [Debugging Data Flow](../../integration-services/troubleshooting/debugging-data-flow.md).  
  
10. Clique em **OK**.  
  
11. Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
## <a name="see-also"></a>Consulte Também  
 [Destino OLE DB](../../integration-services/data-flow/ole-db-destination.md)   
 [Transformações do Integration Services](../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Caminhos do Integration Services](../../integration-services/data-flow/integration-services-paths.md)   
 [Tarefa de Fluxo de Dados](../../integration-services/control-flow/data-flow-task.md)  
  
  
