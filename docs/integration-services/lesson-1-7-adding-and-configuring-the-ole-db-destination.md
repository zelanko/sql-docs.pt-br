---
description: 'Lição 1-7: Adicionar e configurar o destino OLE DB'
title: 'Etapa 7: Adicionar e configurar o destino OLE DB | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 442c841d-d528-4bf0-8724-7156f909ee50
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8c30d9c27550913f5c83334ff33ff3a1cc08e1bc
ms.sourcegitcommit: c74bb5944994e34b102615b592fdaabe54713047
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90990400"
---
# <a name="lesson-1-7-add-and-configure-the-ole-db-destination"></a>Lição 1-7: Adicionar e configurar o destino OLE DB

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



Seu pacote agora pode extrair dados de uma fonte de arquivo simples e transforma esses dados em um formato compatível com o destino. A próxima tarefa é carregar os dados transformados no destino. Para carregar os dados, adicione um destino OLE DB ao fluxo de dados. O destino do OLE DB pode usar uma tabela, exibição de banco de dados ou um comando SQL para carregar os dados em uma diversidade de bancos de dados em conformidade com o OLE DB.  
  
Nesta tarefa, você adiciona e configura um destino OLE DB para usar o gerenciador de conexões OLE DB criado anteriormente.  
  
## <a name="add-and-configure-the-sample-ole-db-destination"></a>Adicionar e configurar a amostra de destino do OLE DB  
  
1.  Na **Caixa de Ferramentas do SSIS**, expanda **Outros Destinos**e arraste **Destino OLE DB** até a superfície de design da guia **Fluxo de Dados** . Coloque o **Destino de OLE DB** diretamente abaixo da transformação **Chave de Data de Pesquisa**.  
  
2.  Selecione a transformação **Chave de Data de Pesquisa** e arraste a seta azul sobre o novo **Destino OLE DB** para conectar os dois componentes.  
  
3.  Na caixa de diálogo **Seleção de Saída e Entrada**, na caixa de listagem **Saída**, selecione **Saída de Correspondência de Pesquisa** e selecione **OK**.  
  
4.  Na superfície de design de **Fluxo de Dados**, selecione o nome **Destino OLE DB** no novo componente **Destino de OLE DB** e altere o nome para **Destino OLE DB de Exemplo**.  
  
5.  Clique duas vezes em **Destino OLE DB de Exemplo**.  
  
6.  Na caixa de diálogo **Editor de Destino do OLE DB**, verifique se **localhost.AdventureWorksDW2012** está selecionado na caixa **Gerenciador de Conexões OLE DB**.  
  
7.  Na caixa **Nome da tabela ou da exibição**, insira ou selecione **[dbo].[FactCurrencyRate]**.  
 
8.  Se existe uma tabela chamada **NewFactCurrencyRate**, você precisa excluí-la agora. Você criará a tabela na próxima etapa.
 
9.  Selecione o botão **Novo** para criar uma nova tabela.  Altere o nome da tabela no script de **Destino OLE DB de Exemplo** para **NewFactCurrencyRate**.  Selecione **OK**.  
 
10. Ao selecionar **OK**, a caixa de diálogo é fechada e o **nome da tabela ou exibição** muda automaticamente para **NewFactCurrencyRate**.  
  
11. Selecione **Mapeamentos**.  
  
12. Verifique se as colunas de entrada **AverageRate**, **CurrencyKey**, **EndOfDayRate**e **DateKey** estão mapeadas corretamente para as colunas de destino. Se forem mapeadas colunas com o mesmo nome, o mapeamento estará correto.  
  
13. Selecione **OK**.  
  
14. Clique com o botão direito do mouse no **Destino OLE DB de Exemplo** e selecione **Propriedades**.  
  
15. Na janela **Propriedades**, verifique se a propriedade **LocaleID** está definida como **Inglês (Estados Unidos)** e se a propriedade **DefaultCodePage** está definida como **1252**.  
  
## <a name="go-to-next-task"></a>Ir para a próxima tarefa
[Etapa 8: Anotar e formatar o pacote da Lição 1](../integration-services/lesson-1-8-making-the-lesson-1-package-easier-to-understand.md)  
  
## <a name="see-also"></a>Confira também  
[Destino OLE DB](../integration-services/data-flow/ole-db-destination.md)  
  
  
  
