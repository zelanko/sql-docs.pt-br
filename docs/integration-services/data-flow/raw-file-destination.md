---
title: Destino do Arquivo Bruto | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.rawfiledest.f1
- sql13.dts.designer.rawfiledestinationconnectionmanager.f1
- sql13.dts.designer.rawfiledestinationcolumns.f1
helpviewer_keywords:
- append options [Integration Services]
- destinations [Integration Services], Raw File
- raw data [Integration Services]
- writing raw data
- Raw File destination
ms.assetid: d311b458-aefc-4b4d-b1a1-4c0ebbb34214
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 417fce6637f17b428f0e4d45404760088a8c0e20
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488575"
---
# <a name="raw-file-destination"></a>Destino do Arquivo Bruto

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  O destino Arquivo Bruto grava dados brutos em um arquivo. Devido ao formato dos dados ser nativo para o destino, os dados não requerem nenhuma tradução e pouca análise. Isso significa que o destino do Arquivo Bruto pode gravar dados mais rápido que outros destinos, tais como o Arquivo Plano e os destinos de OLE DB.  
  
 Além de gravar dados brutos em um arquivo, você também pode usar o destino Arquivo Bruto para gerar um arquivo bruto vazio que contém somente as colunas (arquivo somente de metadados), sem ter que executar o pacote. Use a fonte Arquivo Bruto para recuperar dados brutos que foram escritos previamente pelo destino. Você também pode apontar a fonte Arquivo Bruto para o arquivo somente de metadados.  
  
 O formato de arquivo bruto contém informações de classificação. O destino Arquivo Bruto salva todas as informações de classificação incluindo os sinalizadores de comparação para as colunas de cadeia de caracteres. A fonte Arquivo Bruto lê e segue as informações de classificação. Você tem a opção de configurar fonte Arquivo Bruto para ignorar os sinalizadores de classificação no arquivo, usando o Editor Avançado. Para obter mais informações sobre os sinalizadores de comparação, consulte [Comparando dados de cadeia de caracteres](../../integration-services/data-flow/comparing-string-data.md).  
  
 Você pode configurar o destino de Arquivo Bruto das seguintes formas:  
  
-   Especifique um modo de acesso que seja o nome do arquivo ou uma variável que contenha o nome do arquivo para qual o destino do Arquivo Bruto grava.  
  
-   Indique se o destino do Arquivo Bruto anexa dados a um arquivo existente que tenha o mesmo nome ou cria um arquivo novo.  
  
 O destino do Arquivo Bruto frequentemente é usado para gravar resultados intermediários de dados parcialmente processados entre as execuções de pacotes. Armazenar dados brutos significa que os dados podem ser lidos rapidamente por uma fonte de Arquivo Bruto e posteriormente ser transformados antes que ele seja carregado em seu destino final. Por exemplo, um pacote poderia ser executado várias vezes e cada vez gravar dados brutos em arquivos. Depois, um pacote diferente pode usar a fonte do Arquivo Bruto para ler a partir de cada arquivo, utilizar uma transformação do Union All para intercalar os dados em um conjunto de dados e então aplicar transformações adicionais que resumam os dados antes de carregá-los em seu destino final, tais como uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  O destino do Arquivo Bruto aceita dados nulos, mas não dados de objeto binário grande (BLOB).  
  
> [!NOTE]  
>  O destino do Arquivo Bruto não usa um gerenciador de conexões.  
  
 Esta fonte tem uma entrada normal. Não dá suporte a uma saída de erro.  
  
## <a name="append-and-new-file-options"></a>Opções de acréscimo e arquivo novo  
 A propriedade WriteOption inclui opções para acrescentar dados a um arquivo existente ou criar um arquivo novo.  
  
 A tabela seguinte descreve as opções disponíveis para a propriedade WriteOption.  
  
|Opção|DESCRIÇÃO|  
|------------|-----------------|  
|Acrescentar|Acrescenta dados a um arquivo existente. Os metadados dos dados adicionados devem corresponder ao formato do arquivo.|  
|Criar sempre|Sempre cria um arquivo novo.|  
|Criar uma vez|Cria um arquivo novo. Se o arquivo já existir, o componente falha.|  
|Truncar e acrescentar|Trunca um arquivo existente e depois grava os dados no arquivo. Os metadados dos dados adicionados devem corresponder ao formato do arquivo.|  
  
 Os itens a seguir são importantes sobre como adicionar dados:  
  
-   Adicionar dados a um arquivo bruto existente não reclassifica os dados.  
  
     Você precisa verificar se as chaves classificadas permanecem na ordem correta.  
  
-   Adicionar dados a um arquivo bruto existente não altera os metadados do arquivo (informações de classificação).  
  
 Por exemplo, um pacote lê os dados classificados no PK (ProductKey). O fluxo de dados de pacote adiciona os dados a um arquivo bruto existente. Na primeira vez que o pacote é executado, três linhas são recebidas (PK 1000, 1100, 1200). O arquivo bruto agora contém os seguintes dados.  
  
-   1000, produtoA  
  
-   1100, produtoB  
  
-   1200, produtoC  
  
 Na segunda vez que o pacote é executado, duas novas linhas são recebidas (PK 1001, 1300). O arquivo bruto agora contém os seguintes dados.  
  
-   1000, produtoA  
  
-   1100, produtoB  
  
-   1200, produtoC  
  
-   1001, produtoD  
  
-   1300, produtoE  
  
 Os novos dados são adicionados no final do arquivo bruto e as chaves classificadas (PK) estão fora de ordem. Além disso, a operação de acrescentar não alterou os metadados do arquivo (informações de classificação). Se você ler o arquivo usando a fonte Arquivo Bruto, o componente indicará que o arquivo ainda está classificado em PK, embora os dados no arquivo não estejam mais na ordem correta.  
  
 Para manter as chaves classificadas na ordem correta enquanto adiciona dados, você pode criar o fluxo de dados de pacote da seguinte maneira:  
  
1.  Recupere novas linhas usando a Origem A.  
  
2.  Recupere linhas existentes de RawFile1 usando a Origem B.  
  
3.  Combine as entradas de Origem A e Origem B usando a transformação Union All.  
  
4.  Classifique em PK.  
  
5.  Grave no RawFile2 usando o destino Arquivo Bruto.  
  
     RawFile1 está bloqueado porque está sendo lido no fluxo de dados.  
  
6.  Substitua RawFile1 por RawFile2.  
  
### <a name="using-the-raw-file-destination-in-a-loop"></a>Usando o destino do Arquivo Bruto em um loop  
 Se o fluxo de dados que usa o destino do Arquivo Bruto estiver em um loop, talvez você precise criar o arquivo uma vez e, em seguida, acrescentar dados ao arquivo quando o loop se repetir. Para acrescentar dados ao arquivo, os dados que são acrescentados devem corresponder ao formato do arquivo existente.  
  
 Para criar o arquivo na primeira iteração do loop e então acrescentar filas nas iterações subsequentes do loop, você precisa fazer o seguinte na hora do design:  
  
1.  Defina a propriedade WriteOption como **CreateOnce** ou **CreateAlways**e execute uma iteração do loop. O arquivo é criado. Isto assegura que os metadados de dados acrescentados e o arquivo correspondam.  
  
2.  Redefina a propriedade WriteOption como **Append** e defina a propriedade ValidateExternalMetadata como **False**.  
  
 Se você usar a opção **TruncateAppend** em vez da opção **Append** , truncará filas que foram adicionadas a qualquer iteração anterior e então acrescentará novas filas. Usar a opção **TruncateAppend** também requer que os dados correspondam ao formato do arquivo.  
  
## <a name="configuration-of-the-raw-file-destination"></a>Configuração do destino Arquivo Bruto  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propriedades personalizadas de arquivo bruto](../../integration-services/data-flow/raw-file-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter informações sobre como definir as propriedades do componente, consulte [Definir as propriedades de um componente de fluxo de dados](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Entrada de blog, [Raw Files Are Awesome](https://www.sqlservercentral.com/blogs/31-days-of-ssis-%e2%80%93-raw-files-are-awesome-131)(Arquivos brutos são incríveis), em sqlservercentral.com.  
  
## <a name="raw-file-destination-editor-connection-manager-page"></a>Editor de destino Arquivo Bruto (página Gerenciador de Conexões)
  Use o Editor de Destino Arquivo Bruto para configurar o destino Arquivo Bruto para gravar dados brutos em um arquivo.  
  
 **O que você deseja fazer?**  
  
-   [Abra o Editor de destino Arquivo Bruto](#open)  
  
-   [Definir as opções na guia de Gerenciador de Conexões](#connection)  
  
-   [Definir opções na guia Colunas](#mapping)  
  
###  <a name="open-the-raw-file-destination-editor"></a><a name="open"></a> Abra o Editor de destino Arquivo Bruto  
  
1.  Adicione o destino Arquivo Bruto a um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Clique com o botão direito do mouse no componente e clique em **Editar**.  
  
###  <a name="set-options-on-the-connection-manager-tab"></a><a name="connection"></a> Definir as opções na guia de Gerenciador de Conexões  
 **Modo de acesso**  
 Selecione o modo como o nome de arquivo é especificado. Selecione **Nome de arquivo** para inserir o nome do arquivo e o caminho diretamente de **Nome de arquivo de variável** para especificar uma variável que contenha o nome de arquivo.  
  
 **Nome do arquivo** ou **Nome de variável**  
 Insira o nome e o caminho do arquivo bruto ou selecione a variável que contém o nome de arquivo.  
  
 **Opção de gravação**  
 Selecione o método usado para criar e gravar no arquivo.  
  
 **Gerar arquivo bruto inicial**  
 Clique no botão para gerar um arquivo bruto vazio que contém somente as colunas (arquivo de somente metadados) sem precisar executar o pacote. O arquivo contém as colunas que você selecionou na página **Colunas** do **Editor de destino Arquivo Bruto**. Você pode apontar a fonte Arquivo Bruto para esse arquivo somente de metadados.  
  
 Quando você clica em **Gerar arquivo bruto inicial**, uma caixa de mensagem aparece. Clique em **OK** para continuar a criar o arquivo. Clique em **Cancelamento** para selecionar uma lista diferente de colunas na página de **Colunas** .  
  
###  <a name="set-options-on-the-columns-tab"></a><a name="mapping"></a> Definir opções na guia Colunas  
 **Colunas de Entrada Disponíveis**  
 Selecione uma ou mais colunas de entrada para gravar no arquivo bruto.  
  
 **Coluna de Entrada**  
 Uma coluna de entrada é adicionada automaticamente a essa tabela quando você a seleciona em **Colunas de Entrada Disponíveis**; se preferir, selecione a coluna de entrada diretamente nessa tabela.  
  
 **Alias de Saída**  
 Especifique um nome alternativo a ser usado para a coluna de saída.  
  
## <a name="raw-file-destination-editor-columns-page"></a>Editor de destino Arquivo Bruto (página Colunas)
  Use o Editor de Destino Arquivo Bruto para configurar o destino Arquivo Bruto para gravar dados brutos em um arquivo.  
  
 **O que você deseja fazer?**  
  
-   [Abra o Editor de destino Arquivo Bruto](#open)  
  
-   [Definir as opções na guia de Gerenciador de Conexões](#connection)  
  
-   [Definir opções na guia Colunas](#mapping)  
  
###  <a name="open-the-raw-file-destination-editor"></a><a name="open"></a> Abra o Editor de destino Arquivo Bruto  
  
1.  Adicione o destino Arquivo Bruto a um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Clique com o botão direito do mouse no componente e clique em **Editar**.  
  
###  <a name="set-options-on-the-connection-manager-tab"></a><a name="connection"></a> Definir as opções na guia de Gerenciador de Conexões  
 **Modo de acesso**  
 Selecione o modo como o nome de arquivo é especificado. Selecione **Nome de arquivo** para inserir o nome do arquivo e o caminho diretamente de **Nome de arquivo de variável** para especificar uma variável que contenha o nome de arquivo.  
  
 **Nome do arquivo** ou **Nome de variável**  
 Insira o nome e o caminho do arquivo bruto ou selecione a variável que contém o nome de arquivo.  
  
 **Opção de gravação**  
 Selecione o método usado para criar e gravar no arquivo.  
  
 **Gerar arquivo bruto inicial**  
 Clique no botão para gerar um arquivo bruto vazio que contém somente as colunas (arquivo de somente metadados) sem precisar executar o pacote. Você pode apontar a origem Arquivo Bruto para o arquivo somente de metadados.  
  
 Quando você clica no botão, uma lista das colunas é exibida. Você pode clicar em cancelar e modificar as colunas ou pode clicar em OK para continuar a criação do arquivo.  
  
###  <a name="set-options-on-the-columns-tab"></a><a name="mapping"></a> Definir opções na guia Colunas  
 **Colunas de Entrada Disponíveis**  
 Selecione uma ou mais colunas de entrada para gravar no arquivo bruto.  
  
 **Coluna de Entrada**  
 Uma coluna de entrada é adicionada automaticamente a essa tabela quando você a seleciona em **Colunas de Entrada Disponíveis**; se preferir, selecione a coluna de entrada diretamente nessa tabela.  
  
 **Alias de Saída**  
 Especifique um nome alternativo a ser usado para a coluna de saída.  
  
## <a name="see-also"></a>Consulte Também  
 [Origem do arquivo bruto](../../integration-services/data-flow/raw-file-source.md)   
 [Fluxo de Dados](../../integration-services/data-flow/data-flow.md)  
  
  
