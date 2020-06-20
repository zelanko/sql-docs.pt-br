---
title: 'Etapa 6: Adicionando e configurando a transformação Pesquisa | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5c59f723-9707-4407-80ae-f05f483cf65f
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 53e12d2be6cc4829fd9fc983ca5a24e2057da4e8
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84966136"
---
# <a name="step-6-adding-and-configuring-the-lookup-transformations"></a>Etapa 6: Adicionar e configurar a transformação Pesquisa
  Depois de configurar a fonte de Arquivo Simples para extrair dados do arquivo de origem, a próxima tarefa será definir as transformações Pesquisa necessárias para obter os valores de **CurrencyKey** e **DateKey**. Uma transformação Pesquisa executa uma pesquisa ao unir dados na entrada coluna para uma coluna especificada em um conjunto de dados referenciado. O conjunto de dados de referência pode ser uma tabela existente ou visualização, uma nova tabela ou o resultado de uma instrução SQL. Neste tutorial, a transformação Pesquisa usa um gerenciador de conexões OLE DB para conectar-se ao banco de dados que contém os dados que é a fonte do conjunto de dados de referência.  
  
> [!NOTE]  
>  Você também pode configurar a transformação Pesquisa para conectar-se a um cache que contém o conjunto de dados de referência. Para obter mais informações, consulte [Lookup Transformation](data-flow/transformations/lookup-transformation.md).  
  
 Para este tutorial, você irá adicionar e configurar os dois componentes de transformações Pesquisa a seguir para o pacote:  
  
-   Uma transformação para executar uma pesquisa de valores na coluna **CurrencyKey** da tabela de dimensões **DimCurrency** baseada nos valores da coluna **CurrencyID** correspondentes do arquivo simples.  
  
-   Uma transformação para executar uma pesquisa de valores na coluna **DateKey** da tabela de dimensões **DimDate** baseada nos valores da coluna **CurrencyDate** correspondentes do arquivo simples.  
  
 Em ambos os casos, a transformação Pesquisa utilizará o gerenciador de conexões OLE DB que você criou anteriormente.  
  
### <a name="to-add-and-configure-the-lookup-currency-key-transformation"></a>Para adicionar e configurar a transformação Código de Moeda da Pesquisa  
  
1.  Na **caixa de ferramentas do SSIS**, expanda **comum**e, em seguida, arraste **pesquisa** para a superfície de design da guia **fluxo de dados** . Coloque a pesquisa diretamente abaixo da fonte de **dados extrair exemplo de moeda** .  
  
2.  Clique na fonte de arquivo simples **Extrair Dados de Exemplo de Moeda** e arraste a seta verde para a transformação **Pesquisa** recém-adicionada, para poder conectar assim os dois componentes.  
  
3.  Na superfície de design de **Fluxo de Dados** , clique em **Pesquisa** na transformação **Pesquisa** e altere o nome para **Pesquisa de Código de Moeda**.  
  
4.  Clique duas vezes na transformação **Chave de Moeda de Pesquisa** para exibir o Editor de Transformação Pesquisa.  
  
5.  Na página **Geral** , faça as seguintes seleções:  
  
    1.  Selecione **Cache cheio**.  
  
    2.  Na área **Tipo de conexão** , selecione **Gerenciador de conexões OLE DB**.  
  
6.  Na página **Conexão** , faça as seguintes seleções:  
  
    1.  Na caixa de diálogo **Gerenciador de Conexões OLE DB** , verifique se **localhost.AdventureWorksDW2012** está exibido.  
  
    2.  Selecione **Usar os resultados de uma consulta SQL**e digite ou copie a seguinte instrução SQL:  
  
        ```  
        select * from (select * from [dbo].[DimCurrency]) as refTable  
        where [refTable].[CurrencyAlternateKey] = 'ARS'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'AUD'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'BRL'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'CAD'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'CNY'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'DEM'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'EUR'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'FRF'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'GBP'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'JPY'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'MXN'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'SAR'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'USD'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'VEB'  
        ```  
  
7.  Na página **Colunas** , faça as seguintes seleções:  
  
    1.  No painel **Colunas de Entrada Disponíveis** , arraste **CurrencyID** para o painel **Colunas de Pesquisa Disponíveis** e solte em **CurrencyAlternateKey**.  
  
    2.  Na lista **Colunas de Pesquisa Disponíveis** , marque a caixa de seleção à esquerda de **CurrencyKey**.  
  
8.  Clique em **OK** para retornar à superfície de design **Fluxo de Dados** .  
  
9. Clique com o botão direito do mouse na transformação Chave de Moeda de Pesquisa e clique em **Propriedades**.  
  
10. No janela Propriedades, verifique se a `LocaleID` propriedade está definida como **inglês (Estados Unidos)** e se a propriedade **DefaultCodePage** está definida como **1252**.  
  
### <a name="to-add-and-configure-the--lookup-datekey-transformation"></a>Para adicionar e configurar a transformação Pesquisa de Chave de Data  
  
1.  Na **Caixa de Ferramentas do SSIS**, arraste **Pesquisa** até a superfície de design **Fluxo de Dados** . Coloque Pesquisa diretamente abaixo da transformação **Pesquisa de Códigos de Moeda** .  
  
2.  Clique na transformação **Pesquisa de Código de Moeda** e depois arraste a seta verde para a transformação **Pesquisa** recém-adicionada para conectar os dois componentes.  
  
3.  Na caixa de diálogo **Seleção de Saída e Entrada** , clique em **Saída de Correspondência de Pesquisa** na caixa de listagem **Saída** e clique em **OK**.  
  
4.  Na superfície de design **Fluxo de Dados** , clique em **Pesquisa** na transformação **Pesquisa** recém-adicionada e altere o nome para **Pesquisa de Códigos de Data**.  
  
5.  Clique duas vezes na transformação **Chave de Data de Pesquisa** .  
  
6.  Na página **Geral** , selecione **Cache parcial**.  
  
7.  Na página **Conexão** , faça as seguintes seleções:  
  
    1.  Na caixa de diálogo **Gerenciador de conexões OLE DB** , verifique se **localhost.AdventureWorksDW2012** é exibido.  
  
    2.  Na caixa **Usar uma tabela ou exibição** , digite ou selecione **[dbo].[DimDate]**.  
  
8.  Na página **Colunas** , faça as seguintes seleções:  
  
    1.  No painel **Colunas de Entrada Disponíveis** , arraste **CurrencyDate** para o painel **Colunas de Pesquisa Disponíveis** e solte em **FullDateAlternateKey**.  
  
    2.  Na lista **Colunas de Pesquisa Disponíveis** , marque a caixa de seleção à esquerda de **DateKey**.  
  
9. Na página **Avançado** , examine as opções de cache.  
  
10. Clique em **OK** para retornar à superfície de design **Fluxo de Dados** .  
  
11. Clique com o botão direito do mouse na transformação Chave de Data de Pesquisa e clique em **Propriedades**.  
  
12. No janela Propriedades, verifique se a `LocaleID` propriedade está definida como **inglês (Estados Unidos)** e se a propriedade **DefaultCodePage** está definida como **1252**.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Etapa 7: Adicionar e configurar o destino OLE DB](lesson-1-7-adding-and-configuring-the-ole-db-destination.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Transformação pesquisa](data-flow/transformations/lookup-transformation.md)  
  
  
