---
title: 'Etapa 2: Adicionar e configurar um gerenciador de conexões de Arquivo Simples | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 9a77dd32-d8c2-4961-ad37-2a971f9d6043
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2a412235a3eaeb18f32e820460b82ab238c7c0e8
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71296113"
---
# <a name="lesson-1-2-add-and-configure-a-flat-file-connection-manager"></a>Lição 1-2: Adicionar e configurar um gerenciador de conexões de Arquivo Simples

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Nesta tarefa, você adiciona um gerenciador de conexões de Arquivos Simples ao pacote que acabou de criar. Um gerenciador de conexões de Arquivos Simples habilita um pacote para extrair dados de um arquivo simples. Com o gerenciador de conexões de Arquivos Simples, você pode especificar o nome e o local do arquivo, a localidade e a página de códigos e o formato do arquivo, incluindo os delimitadores de coluna, a serem aplicados quando o pacote extrai os dados do arquivo simples. Além disso, é possível especificar manualmente o tipo de dados das colunas individuais ou usar a caixa de diálogo **Sugerir Tipos de Coluna** para mapear automaticamente as colunas de dados extraídos para os tipos de dados [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
Você deve criar um novo gerenciador de conexões de Arquivo Simples para cada formato de arquivo com o qual você está trabalhando. Como este tutorial extrai dados de vários arquivos simples que apresentam todos o mesmo formato de dados, será preciso apenas adicionar e configurar um gerenciador de conexões de Arquivo Simples para seu pacote de exemplo.  
  
Nesta lição, você pode configurar as propriedades a seguir no seu gerenciador de conexão de Arquivo Simples:  
  
-   **Nomes de coluna:** uma vez que o arquivo simples não tem nomes de colunas, o gerenciador de conexões de Arquivo Simples cria nomes de colunas padrão. Estes nomes padrões não são úteis para identificar o que cada coluna representa. Altere os nomes padrão para nomes que correspondem à tabela de fatos para a qual os dados de arquivo simples devem ser carregados.  
  
-   **Mapeamentos de dados:** os mapeamentos de tipo de dados especificados no gerenciador de conexões de Arquivo Simples são usados por todos os componentes de fonte de dados de arquivo simples que fazem referência ao gerenciador de conexões. Os tipos de dados podem ser mapeados manualmente usando o gerenciador de conexões de Arquivos Simples ou a caixa de diálogo **Sugerir Tipos de Coluna** . Nesta tarefa, você exibirá os mapeamentos sugeridos na caixa de diálogo **Sugerir Tipos de Coluna** e criará manualmente os mapeamentos necessários na caixa de diálogo **Editor do Gerenciador de Conexões de Arquivo Simples**.  
  
> [!NOTE]
> O gerenciador de conexões de Arquivos Simples fornece informações de localidade sobre o arquivo de dados. Se o computador não estiver configurado para usar a opção regional **Inglês (Estados Unidos)** , será preciso definir propriedades adicionais na caixa de diálogo Editor do Gerenciador de Conexões de **Arquivo Simples**.  
  
## <a name="add-a-flat-file-connection-manager-to-the-ssis-package"></a>Adicionar um gerenciador de conexões de Arquivo Simples ao pacote SSIS  
  
1.  No painel do **Gerenciador de Soluções**, clique com o botão direito do mouse em **Gerenciadores de Conexão** e selecione **Novo Gerenciador de Conexão**.
1. Na caixa de diálogo **Adicionar Gerenciador de Conexão do SSIS**, selecione **FLATFILE** e, em seguida, **Adicionar**.
  
2.  Na caixa de diálogo **Editor do Gerenciador de Conexões de Arquivo Simples**, em **Nome do gerenciador de conexões**, insira **Dados de Origem de Arquivo Simples de Exemplo**.  
  
3.  Selecione **Procurar**.  
  
4.  Na caixa de diálogo **Abrir**, localize o arquivo **SampleCurrencyData.txt** no computador.  
  
5.  Desmarque os nomes de coluna na caixa de seleção da primeira linha de dados.  
  
### <a name="set-locale-sensitive-properties"></a>Definir propriedades que diferenciam localidade  
  
1.  Na caixa de diálogo **Editor do Gerenciador de Conexões de Arquivo Simples**, selecione **Geral**.  
  
2.  Defina **Localidade** como **Inglês (Estados Unidos)** e **Página de código** como **1252**.  
  
### <a name="rename-columns-in-the-flat-file-connection-manager"></a>Renomear colunas no gerenciador de conexões de Arquivo Simples  
  
1.  Na caixa de diálogo **Editor do Gerenciador de Conexões de Arquivo Simples**, selecione **Avançado**.  
  
2.  No painel de propriedade, faça as seguintes alterações:  
  
    -   Altere a propriedade de nome da **Coluna 0** para **AverageRate**.  
  
    -   Altere a propriedade de nome da **Coluna 1** para **CurrencyID**.  
  
    -   Altere a propriedade de nome da **Coluna 2** para **CurrencyDate**.  
  
    -   Altere a propriedade de nome da **Coluna 3** para **EndOfDayRate**.  
  
### <a name="remap-column-data-types"></a>Remapear tipos de dados de coluna  
  
Por padrão, as quatro colunas são definidas inicialmente como um tipo de dados String [DT_STR] com uma **OutputColumnWidth** de 50.  

1.  Na caixa de diálogo **Editor do Gerenciador de Conexões de Arquivo Simples**, selecione **Sugerir Tipos**.  
  
    [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] sugere automaticamente os tipos de dados apropriados com base nas primeiras 200 linhas de dados. Também é possível alterar essas opções de sugestão para mostrar mais ou menos dados, para especificar o tipo de dados padrão para dados inteiro ou booliano, ou para adicionar espaços como preenchimento das colunas de cadeia de caracteres.  
  
    Por enquanto, não faça alterações nas opções na caixa de diálogo **Sugerir Tipos de Coluna** e selecione **OK** para que o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] sugira os tipos de dados para as colunas. Essa ação o leva de volta ao painel **Avançado** da caixa de diálogo **Editor do Gerenciador de Conexões de Arquivo Simples**, em que é possível exibir os tipos de dados de coluna sugeridos pelo [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Como alternativa, se você selecionar **Cancelar**, nenhuma sugestão será indicada para os metadados da coluna e o tipo de dados da cadeia de caracteres padrão (DT_STR) será usado.  
  
    Neste tutorial, [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] sugere os tipos de dados mostrados na segunda coluna da tabela a seguir referentes aos dados do arquivo SampleCurrencyData.txt. A quarta coluna fornece os tipos de dados necessários para as colunas no destino, que são definidas em uma etapa posterior.  
  
    |Coluna de Arquivo Simples|Tipo sugerido|Coluna de destino|Tipo de destino|  
    |--------------------|------------------|----------------------|--------------------|  
    |AverageRate|float [DT_R4]|FactCurrencyRate.AverageRate|FLOAT|  
    |CurrencyID|string [DT_STR]|DimCurrency.CurrencyAlternateKey|nchar(3)|  
    |CurrencyDate|date [DT_DATE]|DimDate.FullDateAlternateKey|date|  
    |EndOfDayRate|float [DT_R4]|FactCurrencyRate.EndOfDayRate|FLOAT|  
  
    O tipo de dados sugerido para a coluna **CurrencyID** não é compatível com o tipo de dados do campo na tabela de destino. Como o tipo de dados de `DimCurrency.CurrencyAlternateKey` é nchar (3), **CurrencyID** deve ser alterado de cadeia de caracteres [DT_STR] para a cadeia de caracteres Unicode [DT_WSTR]. Além disso, o campo `DimDate.FullDateAlternateKey` é definido como um tipo de dados de data; assim, o tipo para **CurrencyDate** deve ser alterado da data [DT_Date] para a data do banco de dados [DT_DBDATE].  
  
2.  Na lista, selecione a coluna **CurrencyID** e, no painel Propriedade, altere o Tipo de Dados de coluna **CurrencyID** de cadeia de caracteres [DT_STR] para cadeia de caracteres de Unicode [DT_WSTR].  
  
3.  No painel Propriedade, altere o tipo de dados de coluna **CurrencyDate** da data [DT_DATE] para a data do banco de dados [DT_DBDATE].  
  
4.  Selecione **OK**.  
  
## <a name="go-to-next-task"></a>Ir para a próxima tarefa
[Etapa 3: Adicionar e configurar um gerenciador de conexões OLE DB](../integration-services/lesson-1-3-adding-and-configuring-an-ole-db-connection-manager.md)  
  
## <a name="see-also"></a>Confira também  
[Gerenciador de conexões de arquivo simples](../integration-services/connection-manager/flat-file-connection-manager.md)  
[Tipos de dados do Integration Services](../integration-services/data-flow/integration-services-data-types.md)  
  
  
  
