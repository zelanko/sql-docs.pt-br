---
title: 'Etapa 6: Adicionar e configurar as transformações de Pesquisa | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 5c59f723-9707-4407-80ae-f05f483cf65f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 82db40d3b3fd61129823b3e745d097b47bd6973b
ms.sourcegitcommit: dd794633466b1da8ead9889f5e633bdf4b3389cd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54143372"
---
# <a name="lesson-1-6-add-and-configure-the-lookup-transformations"></a>Lição 1-6: Adicionar e configurar as transformações de Pesquisa

Depois de configurar a fonte de Arquivo Simples para extrair dados do arquivo de origem, você define as transformações Pesquisa necessárias para obter os valores de **CurrencyKey** e **DateKey**. Uma transformação Pesquisa executa uma pesquisa ao unir dados na entrada coluna para uma coluna especificada em um conjunto de dados referenciado. O conjunto de dados de referência pode ser uma tabela existente ou visualização, uma nova tabela ou o resultado de uma instrução SQL. Neste tutorial, a transformação Pesquisa usa um gerenciador de conexões OLE DB para conectar-se ao banco de dados que contém os dados de origem do conjunto de dados de referência.  
  
> [!NOTE]  
> Você também pode configurar a transformação Pesquisa para conectar-se a um cache que contém o conjunto de dados de referência. Para obter mais informações, confira [transformação de Pesquisa](../integration-services/data-flow/transformations/lookup-transformation.md).  
  
Nesta tarefa, você adiciona e configura os dois componentes de transformações Pesquisa a seguir para o pacote:  
  
-   Uma transformação que executa uma pesquisa de valores na coluna **CurrencyKey** da tabela de dimensões **DimCurrency** baseada nos valores da coluna **CurrencyID** correspondentes do arquivo simples.  
  
-   Uma transformação que executa uma pesquisa de valores na coluna **DateKey** da tabela de dimensões **DimDate** baseada nos valores da coluna **CurrencyDate** correspondentes do arquivo simples.  
  
Em ambos os casos, a transformação Pesquisa utilizará o gerenciador de conexões OLE DB que você criou anteriormente.  
  
## <a name="add-and-configure-the-lookup-currency-key-transformation"></a>Adicionar e configurar a transformação Pesquisar Chave de Moeda  
  
1.  Na **Caixa de Ferramentas do SSIS**, expanda **Comum**e arraste **Pesquisa** para a superfície de design da guia **Fluxo de Dados** . Coloque **Pesquisa** diretamente abaixo da fonte **Extrair Dados de Exemplo de Moeda**.  
  
2.  Selecione a fonte de arquivo simples **Extrair Dados de Exemplo de Moeda** e arraste a seta azul para a transformação **Pesquisa** recém-adicionada, para poder conectar assim os dois componentes.  
  
3.  Na superfície de design de **Fluxo de Dados**, selecione **Pesquisa** na transformação **Pesquisa** e altere o nome para **Pesquisar Chave de Moeda**.  
  
4.  Clique duas vezes na transformação **Pesquisar Chave de Moeda** para exibir o **Editor de Transformação Pesquisa**.  
  
5.  Na página **Geral** , faça as seguintes seleções:  
  
    1.  Selecione **Cache cheio**.  
  
    2.  Na área **Tipo de conexão** , selecione **Gerenciador de conexões OLE DB**.  
  
6.  Na página **Conexão** , faça as seguintes seleções:  
  
    1.  Na caixa de diálogo **Gerenciador de Conexões OLE DB** , verifique se **localhost.AdventureWorksDW2012** está exibido.  
  
    2.  Selecione **Usar resultados de uma consulta SQL** e insira ou cole a seguinte instrução SQL:  
  
        ```sql
        SELECT * FROM [dbo].[DimCurrency]
        WHERE [CurrencyAlternateKey]
        IN ('ARS', 'AUD', 'BRL', 'CAD', 'CNY',
            'DEM', 'EUR', 'FRF', 'GBP', 'JPY',
            'MXN', 'SAR', 'USD', 'VEB')
        ```  
    3.  Selecione **Visualizar** para verificar os resultados da consulta.
  
7.  Na página **Colunas** , faça as seguintes seleções:  
  
    1.  No painel **Colunas de Entrada Disponíveis** , arraste **CurrencyID** para o painel **Colunas de Pesquisa Disponíveis** e solte em **CurrencyAlternateKey**.  
  
    2.  Na lista **Colunas de Pesquisa Disponíveis** , marque a caixa de seleção à esquerda de **CurrencyKey**.  
  
8.  Selecione **OK** para retornar à superfície de design **Fluxo de Dados**.  
  
9. Clique com o botão direito do mouse na transformação Pesquisar Chave de Moeda e selecione **Propriedades**.  
  
10. Na janela **Propriedades**, verifique se a propriedade **LocaleID** é **Inglês (Estados Unidos)** e se a propriedade **DefaultCodePage** é **1252**.  
  
## <a name="add-and-configure-the-lookup-date-key-transformation"></a>Adicionar e configurar a transformação Pesquisar Código de Data  
  
1.  Na **Caixa de Ferramentas do SSIS**, arraste **Pesquisa** até a superfície de design **Fluxo de Dados** . Coloque essa **Pesquisa** diretamente abaixo da transformação **Pesquisar Chave de Moeda**.  
  
2.  Selecione a transformação **Pesquisar Chave de Moeda** e depois arraste a seta azul para a nova transformação **Pesquisa** para conectar os dois componentes.  
  
3.  Na caixa de diálogo **Seleção de Entrada e Saída**, selecione **Saída de Correspondência de Pesquisa** na caixa de listagem **Saída** e selecione **OK**.  
  
4.  Na superfície de design **Fluxo de Dados**, selecione o nome **Pesquisa** na transformação **Pesquisa** recém-adicionada e altere o nome para **Pesquisar Código de Data**.  
  
5.  Clique duas vezes na transformação **Chave de Data de Pesquisa** .  
  
6.  Na página **Geral** , selecione **Cache parcial**.  
  
7.  Na página **Conexão** , faça as seguintes seleções:  
  
    1.  Na caixa de diálogo **Gerenciador de conexões OLE DB**, verifique se **localhost.AdventureWorksDW2012** é exibido.  
  
    2.  Na caixa **Usar uma tabela ou exibição**, insira ou selecione **[dbo].[DimDate]**.  
  
8.  Na página **Colunas** , faça as seguintes seleções:  
  
    1.  No painel **Colunas de Entrada Disponíveis** , arraste **CurrencyDate** para o painel **Colunas de Pesquisa Disponíveis** e solte em **FullDateAlternateKey**.  
  
    2.  Na lista **Colunas de Pesquisa Disponíveis** , marque a caixa de seleção à esquerda de **DateKey**.  
  
9. Na página **Avançado** , examine as opções de cache.  
  
10. Selecione **OK** para retornar à superfície de design **Fluxo de Dados**.  
  
11. Clique com o botão direito do mouse na transformação **Chave de Data de Pesquisa** e selecione **Propriedades**.
  
12. Na janela **Propriedades**, verifique se a propriedade **LocaleID** é **Inglês (Estados Unidos)** e se a propriedade **DefaultCodePage** é **1252**.  
  
## <a name="go-to-next-task"></a>Ir para a próxima tarefa
[Etapa 7: Adicionar e configurar o destino OLE DB](../integration-services/lesson-1-7-adding-and-configuring-the-ole-db-destination.md)  
  
## <a name="see-also"></a>Confira também  
[Transformação de Pesquisa](../integration-services/data-flow/transformations/lookup-transformation.md)  
  
  
  
