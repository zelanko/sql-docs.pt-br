---
title: 'Etapa 2: adicionar e configurar um gerenciador de conexões de arquivo simples | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 9a77dd32-d8c2-4961-ad37-2a971f9d6043
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e2d22c652ce63bfc3069756251ff554a5d13c186
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48197346"
---
# <a name="step-2-adding-and-configuring-a-flat-file-connection-manager"></a>Etapa 2: adicionando e configurando um gerenciador de conexões de arquivo simples
  Nesta tarefa, você adiciona um gerenciador de conexões de Arquivos Simples ao pacote que acabou de criar. Um gerenciador de conexões de Arquivos Simples habilita um pacote para extrair dados de um arquivo simples. Com o gerenciador de conexões de Arquivos Simples, você pode especificar o nome e o local do arquivo, a localidade e a página de códigos e o formato do arquivo, incluindo os delimitadores de coluna, a serem aplicados quando o pacote extrai os dados do arquivo simples. Além disso, é possível especificar manualmente o tipo de dados das colunas individuais ou usar a caixa de diálogo **Sugerir Tipos de Coluna** para mapear automaticamente as colunas de dados extraídos para os tipos de dados [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
 Você deve criar um novo gerenciador de conexões de Arquivos Simples para cada formato de arquivo com os quais você trabalha. Como este tutorial extrai dados de vários arquivos simples que apresentam exatamente o mesmo formato de dados, será preciso adicionar e configurar apenas um gerenciador de conexões de Arquivos Simples para seu pacote.  
  
 Neste tutorial, serão configuradas as seguintes propriedades em seu gerenciador de conexões de Arquivos Simples:  
  
-   **Nomes de coluna:** como o arquivo simples não tem nomes de colunas, o gerenciador de conexões de Arquivos Simples cria nomes de colunas padrão. Estes nomes padrões não são úteis para identificar o que cada coluna representa. Para tornar esses nomes mais úteis, altere os nomes padrão para nomes que correspondam à tabela de fatos à qual os dados do arquivo simples serão carregados.  
  
-   **Mapeamentos de dados:** os mapeamentos de tipo de dados especificados no gerenciador de conexões de Arquivos Simples serão usados por todos os componentes de fonte de dados de arquivos simples que fazem referência ao gerenciador de conexões. Os tipos de dados podem ser mapeados manualmente usando o gerenciador de conexões de Arquivos Simples ou a caixa de diálogo **Sugerir Tipos de Coluna** . Neste tutorial, você exibirá os mapeamentos sugeridos na caixa de diálogo **Sugerir Tipos de Coluna** e fará manualmente os mapeamentos necessários na caixa de diálogo **Editor do Gerenciador de Conexões de Arquivos Simples** .  
  
 O gerenciador de conexões de Arquivos Simples fornece informações de localidade sobre o arquivo de dados. Se seu computador não estiver configurado para usar a opção regional Inglês (Estados Unidos), será preciso definir propriedades adicionais na caixa de diálogo **Editor do Gerenciador de Conexões de Arquivos Simples** .  
  
### <a name="to-add-a-flat-file-connection-manager-to-the-ssis-package"></a>Para adicionar um gerenciador de conexões de arquivos simples ao pacote SSIS  
  
1.  Clique com o botão direito do mouse em qualquer lugar da área **Gerenciadores de Conexões** e clique em **Nova Conexão de Arquivos Simples**.  
  
2.  Na caixa de diálogo **Editor do Gerenciador de Conexões de Arquivos Simples** , em **Nome do gerenciador de conexões**, digite **Dados de Origem de Arquivos Simples de Exemplo**.  
  
3.  Clique em **Procurar**.  
  
4.  Na caixa de diálogo **Abrir** , localize o arquivo SampleCurrencyData.txt no computador.  
  
     Os dados de exemplo estão incluídos com os pacotes de lição do [!INCLUDE[ssIS](../includes/ssis-md.md)] . Para baixar os dados de exemplo e os pacotes de lição, faça o seguinte.  
  
    1.  Navegue para os [Exemplos de Produtos do Integration Services](http://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  Clique na guia **DOWNLOADS** .  
  
    3.  Clique no arquivo SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
5.  Desmarque os nomes de coluna na caixa de seleção da primeira linha de dados.  
  
### <a name="to-set-locale-sensitive-properties"></a>Definir propriedades com distinção de localidade  
  
1.  Na caixa de diálogo **Editor do Gerenciador de Conexões de Arquivos Simples** , clique em **Geral**.  
  
2.  Defina **Localidade** como Inglês (Estados Unidos) e **Página de código** como 1252.  
  
### <a name="to-rename-columns-in-the-flat-file-connection-manager"></a>Renomear colunas no gerenciador de conexões de Arquivos Simples  
  
1.  Na caixa de diálogo **Editor do Gerenciador de Conexões de Arquivos Simples** , clique em **Avançado**.  
  
2.  No painel de propriedade, faça as seguintes alterações:  
  
    -   Alterar o **coluna 0** nome da propriedade a ser `AverageRate`.  
  
    -   Alterar o **coluna 1** nome da propriedade a ser `CurrencyID`.  
  
    -   Alterar o **coluna 2** nome da propriedade a ser `CurrencyDate`.  
  
    -   Alterar o **coluna 3** nome da propriedade a ser `EndOfDayRate`.  
  
    > [!NOTE]  
    >  Por padrão, as quatro colunas são definidas inicialmente como um tipo de dados de cadeia de caracteres [DT_STR] com uma `OutputColumnWidth` de 50.  
  
### <a name="to-remap-column-data-types"></a>Remapear tipos de dados de coluna  
  
1.  Na caixa de diálogo **Editor do Gerenciador de Conexões de Arquivos Simples** , clique em **Sugerir Tipos**.  
  
     [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] sugere automaticamente os tipos de dados mais apropriados com base nas primeiras 200 linhas de dados. Também é possível alterar essas opções de sugestão para mostrar mais ou menos dados, para especificar o tipo de dados padrão para dados inteiro ou booliano, ou para adicionar espaços como preenchimento das colunas de cadeia de caracteres.  
  
     Por enquanto, não faça alterações nas opções na caixa de diálogo **Sugerir Tipos de Coluna** e clique em **OK** para que o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] sugira os tipos de dados para as colunas. Esse procedimento retornará o painel **Avançado** da caixa de diálogo **Editor do Gerenciador de Conexões de Arquivos Simples** , em que é possível exibir os tipos de dados de coluna sugeridos pelo [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. (Se você clicar em **Cancelar**, nenhuma sugestão será indicada para os metadados da coluna e o tipo de dados da cadeia de caracteres padrão [DT_STR] será usado.)  
  
     Neste tutorial, [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] sugere os tipos de dados mostrados na segunda coluna da tabela a seguir referentes aos dados do arquivo SampleCurrencyData.txt. Entretanto, os tipos de dados que forem necessários para as colunas no destino, que serão definidos em uma etapa futura, serão mostrados na última coluna da tabela a seguir.  
  
    |Coluna de Arquivos Simples|Tipo Sugerido|Coluna de Destino|Tipo de Destino|  
    |----------------------|--------------------|------------------------|----------------------|  
    |AverageRate|float [DT_R4]|FactCurrency.AverageRate|FLOAT|  
    |CurrencyID|string [DT_STR]|DimCurrency.CurrencyAlternateKey|nchar(3)|  
    |CurrencyDate|date [DT_DATE]|DimDate.FullDateAlternateKey|Data|  
    |EndOfDayRate|float [DT_R4]|FactCurrency.EndOfDayRate|FLOAT|  
  
     O tipo de dados sugerido para o `CurrencyID` coluna é incompatível com o tipo de dados do campo na tabela de destino. Porque o tipo de dados `DimCurrency.CurrencyAlternateKey` é nchar (3), `CurrencyID` deve ser alterado de cadeia de caracteres [DT_STR] para cadeia de caracteres [DT_WSTR]. Além disso, o campo `DimDate.FullDateAlternateKey` é definido como um tipo de dados de data; portanto, `CurrencyDate` precisa ser alterado da data [DT_Date] para a data do banco de dados [DT_DBDATE].  
  
2.  Na lista, selecione a coluna CurrencyID e no painel de propriedade, altere o tipo de dados da coluna `CurrencyID` de cadeia de caracteres [DT_STR] para Unicode da cadeia de caracteres [DT_WSTR].  
  
3.  No painel de propriedade, altere o tipo de dados da coluna `CurrencyDate` da data [DT_DATE] para a data do banco de dados [DT_DBDATE].  
  
4.  Clique em **OK**.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Etapa 3: Adicionando e configurando um gerenciador de conexões OLE DB](lesson-1-3-adding-and-configuring-an-ole-db-connection-manager.md)  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciador de Conexão de arquivo simples](connection-manager/file-connection-manager.md)   
 [Tipos de dados do Integration Services](data-flow/integration-services-data-types.md)  
  
  
