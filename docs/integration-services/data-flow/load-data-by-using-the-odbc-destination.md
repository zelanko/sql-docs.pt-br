---
description: Carregar dados por meio do destino ODBC
title: Carregar dados por meio do destino ODBC | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 339ec0a8-922e-48c0-97b3-fc5ee34f95e3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6ea049a657b5d0392841f8bd6e44954d2774c13c
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92193219"
---
# <a name="load-data-by-using-the-odbc-destination"></a>Carregar dados por meio do destino ODBC

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Este procedimento mostra como carregar dados usando o destino ODBC. Para adicionar e configurar um destino ODBC, o pacote já deve incluir pelo menos uma tarefa de Fluxo de Dados e uma fonte.  
  
### <a name="to-load-data-using-an-odbc-destination"></a>Para carregar dados usando um destino ODBC  
  
1.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra o pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] desejado.  
  
2.  Clique na guia **Fluxo de Dados** , e então, na **Caixa de Ferramentas**, arraste o destino ODBC para a superfície de design.  
  
3.  Arraste uma saída disponível para um componente de fluxo de dados para a entrada do destino ODBC.  
  
4.  Clique duas vezes no destino ODBC.  
  
5.  Na caixa de diálogo **Editor de Destino ODBC** , na página **Gerenciador de Conexões** , selecione um gerenciador de conexões ODBC existente ou clique em **Novo** para criar um gerenciador de conexões novo.  
  
6.  Selecione o método de acesso de dados.  
  
    -   **Nome da Tabela – Lote**: selecione esta opção para configurar o destino ODBC para funcionar no modo em lote. Quando você selecionar essa opção, poderá definir o **Tamanho do lote**.  
  
    -   **Nome da Tabela – Linha a Linha**: selecione esta opção para configurar o destino ODBC para inserir cada uma das linhas na tabela de destino, uma de cada vez. Quando você selecionar essa opção, os dados serão carregados na tabela uma linha de cada vez.  
  
7.  No campo **Nome da tabela ou exibição** , selecione uma tabela ou exibição disponível do banco de dados na lista ou digite uma expressão regular para identificar a tabela. Essa lista contém apenas as primeiras 1.000 tabelas. Se o banco de dados contiver mais de 1.000 tabelas, você poderá digitar o início do nome de uma tabela ou usar o curinga (*) para inserir qualquer parte do nome para exibir a tabela ou tabelas desejadas.  
  
8.  Você pode clicar em **Visualizar** para exibir até 200 linhas dos dados da tabela selecionada no destino ODBC.  
  
9. Clique em **Mapeamentos** e mapeie as colunas da lista **Colunas de Entrada Disponíveis** para as colunas da lista **Colunas de Destino Disponíveis** arrastando as colunas de uma lista para outra.  
  
10. Para configurar a saída de erro, clique em **Saída de Erro**.  
  
11. Clique em **OK**.  
  
12. Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
## <a name="see-also"></a>Consulte Também  
 [Editor do Destino ODBC &#40;Página Gerenciador de Conexões&#41;](./odbc-destination.md)   
 [Editor de Destinos ODBC &#40;Página Mapeamentos&#41;](./odbc-destination.md)   
 [Editor de Fonte ODBC &#40;Página Saída de Erro&#41;](./odbc-source.md)  
  
