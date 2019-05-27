---
title: Gerenciador de Conexões de Arquivo Simples | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.ffileconnection.general.f1
- sql13.dts.designer.ffileconnection.columns.f1
- sql13.dts.designer.ffileconnection.columnproperties.f1
- sql13.dts.designer.ffileconnection.preview.f1
helpviewer_keywords:
- connection managers [Integration Services], Flat File
- connections [Integration Services], flat files
- files [Integration Services], connections
- Flat File connection manager
- flat files
- flat file connections [Integration Services]
ms.assetid: 7830f80d-af32-4e8f-a6fc-f03af6bc1946
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2cf3156597035241398e354e8c80bfebb9c16d67
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65728268"
---
# <a name="flat-file-connection-manager"></a>Gerenciador de conexões de arquivos simples

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Um gerenciador de conexões de Arquivos Simples permite que um pacote acesse dados em um arquivo simples. Por exemplo, a origem e o destino dos Arquivos Simples podem usar gerenciadores de conexões de Arquivos Simples para extrair e carregar dados.  
  
 O gerenciador de conexões de arquivos simples pode acessar apenas um arquivo. Para consultar vários arquivos, utilize um gerenciador de conexões de vários arquivos simples em vez de um gerenciador de conexões de arquivos simples. Para obter mais informações, consulte [Gerenciador de conexões de vários arquivos simples](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md).  
  
## <a name="column-length"></a>Comprimento da coluna  
 Por padrão, o gerenciador de conexões de arquivos simples define o comprimento das colunas de cadeia de caracteres como 50 caracteres. Na caixa de diálogo **Editor do Gerenciador de Conexões de Arquivos Simples** , você pode avaliar dados de exemplo e redimensionar automaticamente o comprimento dessas colunas para evitar truncamento dos dados ou excesso de largura da coluna. Mesmo assim, a menos que você redimensione subsequentemente o comprimento de coluna em uma fonte de arquivo simples ou em uma transformação, o comprimento da coluna da coluna de cadeia de caracteres permanece o mesmo durante o fluxo de dados. Se essas colunas de cadeia de caracteres forem mapeadas para colunas de destino que sejam menores, serão exibidos avisos na interface do usuário. Além disso, durante no tempo de execução, podem ocorrer erros devido ao truncamento de dados. Para evitar erros ou truncamento, você pode redimensionar as colunas para que sejam compatíveis com as colunas de destino no gerenciador de conexões de arquivos simples, na origem do arquivo simples ou na transformação. Para modificar o comprimento de colunas de saída, você define a propriedade **Length** da coluna de saída na guia **Propriedades de Entrada e Saída** na caixa de diálogo **Editor Avançado** .  
  
 Se você atualizar os comprimentos da coluna no gerenciador de conexões de arquivos simples após adicionar e configurar a fonte de arquivo simples que utiliza o gerenciador de conexões, não será necessário redimensionar manualmente as colunas de saída na origem do arquivo simples. Quando você abre a caixa de diálogo **Origem de Arquivo Simples** , a origem de arquivo simples fornece uma opção para sincronizar os metadados da coluna.  
  
## <a name="configuration-of-the-flat-file-connection-manager"></a>Configuração do gerenciador de conexões de arquivo simples  
 Quando você adicionar um gerenciador de conexões de arquivos simples a um pacote, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] criará um gerenciador de conexões que determinará uma conexão de arquivo simples no momento da execução, definirá suas propriedades e adicionará o gerenciador de conexões de arquivos simples à coleção **Conexões** do pacote.  
  
 A propriedade **ConnectionManagerType** do gerenciador de conexões é definida como **FLATFILE**.  
  
 Por padrão, o gerenciador de conexões de arquivos simples sempre verifica se há um delimitador de linha em dados sem aspas e inicia uma nova linha quando um delimitador de linha é localizado. Isso permite que o gerenciador de conexões analise corretamente arquivos com linhas que não têm campos de coluna.  
  
 Em alguns casos, desabilitar esse recurso pode melhorar o desempenho do pacote. Você pode desabilitar esse recurso definindo a propriedade do gerenciador de conexões de arquivos simples, **AlwaysCheckForRowDelimiters**, como **False**.  
  
 Você pode configurar um gerenciador de conexões de arquivos simples dos seguintes modos:  
  
-   Especifique o arquivo, a localidade e a página de código que serão usados. A localidade é usada para interpretar dados confidenciais de localidade como datas, e a página de código é usada para converter dados de cadeia de caracteres para Unicode.  
  
-   Especifique o formato de arquivo. Você pode usar um formato delimitado, de largura fixa ou irregular à direita.  
  
-   Especifique uma linha de cabeçalho, fila de dados e delimitadores de coluna. Delimitadores de coluna podem ser definidos no nível de arquivo e ser sobrescritos no nível de coluna.  
  
-   Indique se a primeira linha nos arquivos contém nomes de coluna.  
  
-   Especifique um caractere de qualificador de texto. Cada coluna pode ser configurada para reconhecer um qualificador de texto.  
  
     O uso de um caractere qualificador para inserir um caractere qualificador em uma cadeia de caracteres qualificada tem suporte de um Gerenciador de Conexões de arquivo simples. A instância dupla de um qualificador de texto é interpretada como uma instância literal única daquela cadeia de caracteres. Por exemplo, se o qualificador de texto for uma aspa simples e os dados de entrada forem 'abc', 'def', 'g'hi', os dados de saída serão abc, def, g'hi. No entanto, uma instância de um qualificador inserida em uma cadeia de caracteres qualificada faz com que a fonte de arquivo simples falhe com o erro DTS_E_PRIMEOUTPUTFAILED.
  
-   Defina as propriedades, como o nome, o tipo de dados e a largura máxima em colunas individuais.  
  
 Você pode definir a propriedade ConnectionString para o gerenciador de conexões de arquivos simples especificando uma expressão na janela Propriedades do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Para evitar um erro de validação, siga as etapas abaixo.  
  
-   Quando você usa uma expressão para especificar o arquivo, adiciona um caminho de arquivo na caixa **Nome do Arquivo** em **Editor do Gerenciador de Conexões de Arquivos Simples**.  
  
-   Defina a propriedade **DelayValidation** no gerenciador de conexões de Arquivos Simples para **True**.  
  
 Você pode usar uma expressão para criar um nome de arquivo em tempo de execução usando o gerenciador de conexões de Arquivo Simples com o destino do Arquivo Simples.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter informações sobre como configurar um gerenciador de conexões programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Adicionando conexões programaticamente](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="flat-file-connection-manager-editor-general-page"></a>Editor do Gerenciador de Conexões de Arquivos Simples (página Geral)
  Use a página **Geral** da caixa de diálogo **Editor do Gerenciador de Conexões de Arquivos Simples** para selecionar um arquivo e formato de dados. Uma conexão de arquivos simples habilita um pacote a conectar-se com um arquivo de texto.  
  
 Para obter mais informações sobre o gerenciador de conexões de Arquivo Simples, consulte [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
### <a name="options"></a>Opções  
 **Nome do gerenciador de conexões**  
 Forneça um nome exclusivo para a conexão de arquivos simples no fluxo de trabalho. O nome fornecido será exibido no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Descrição**  
 Descreva a conexão. Como prática recomendável, descreva a conexão em termos de objetivo, para tornar os pacotes autodocumentados e mais fáceis de manter.  
  
 **Nome do arquivo**  
 Digite o caminho e o nome do arquivo a ser usado na conexão de arquivos simples.  
  
 **Procurar**  
 Localize o nome do arquivo a ser usado na conexão de arquivos simples.  
  
 **Localidade**  
 Especifique a localidade para fornecer informações de idioma específicas para solicitações e formatos de data e hora.  
  
 **Unicode**  
 Indique se deve ser usado o Unicode. Se você usar o Unicode, não poderá especificar uma página de código.  
  
 **Página de código**  
 Especifique a página de código do texto não Unicode.  
  
 **Formato**  
 Indique se o arquivo usa formatação delimitada, de largura fixa ou irregular à direita.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|Delimitado|As colunas são separadas por delimitadores, especificados na página **Colunas** .|  
|Largura fixa|As colunas têm uma largura fixa.|  
|Irregular à direita|Arquivos irregulares à direita são arquivos em que toda coluna tem uma largura fixa, à exceção da última coluna. Ela é delimitada pelo delimitador de linha.|  
  
 **Qualificador de texto**  
 Especifique o qualificador de texto a ser usado. Por exemplo, você pode especificar que os campos de texto fiquem entre aspas.  
  
> [!NOTE]  
>  Depois de selecionar um qualificador de texto, você não pode selecionar a opção **None** . Digite **None** para anular a seleção do qualificador de texto.  
  
 **Delimitador de linha de cabeçalho**  
 Selecione na lista de delimitadores de linhas de cabeçalho ou digite o texto do delimitador.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**{CR}{LF}**|A linha do cabeçalho é delimitada por uma combinação de retorno de carro e avanço de linha.|  
|**{CR}**|A linha do cabeçalho é delimitada por um retorno de carro.|  
|**{LF}**|A linha do cabeçalho é delimitada por um avanço de linha.|  
|**Ponto-e-vírgula {;}**|A linha do cabeçalho é delimitada por um ponto-e-vírgula.|  
|**Dois-pontos {:}**|A linha do cabeçalho é delimitada por dois-pontos.|  
|**Vírgula {,}**|A linha do cabeçalho é delimitada por uma vírgula.|  
|**Tabulação {t}**|A linha do cabeçalho é delimitada por uma tabulação.|  
|**Barra vertical {&#124;}**|A linha do cabeçalho é delimitada por uma barra vertical.|  
  
 **Linhas de cabeçalho a ignorar**  
 Especifique o número de linhas de cabeçalho ou linhas de dados iniciais a ignorar, caso existam.  
  
 **Nomes de coluna na primeira linha de dados**  
 Indique se deseja esperar ou fornecer nomes de coluna na primeira linha de dados.  
## <a name="flat-file-connection-manager-editor-columns-page"></a>Editor do Gerenciador de Conexões de Arquivos Simples (página Colunas)
  Use a página **Colunas** da caixa de diálogo **Editor do Gerenciador de Conexões de Arquivos Simples** para especificar a linha e informações da coluna, e visualizar o arquivo.  
  
 Para obter mais informações sobre o gerenciador de conexões de Arquivo Simples, consulte [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
### <a name="static-options"></a>Opções estáticas  
 **Nome do gerenciador de conexões**  
 Forneça um nome exclusivo para a conexão de Arquivo Simples no fluxo de trabalho. O nome fornecido será exibido no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Descrição**  
 Descreva a conexão. Como prática recomendável, descreva a conexão em termos de objetivo, para tornar os pacotes autodocumentados e mais fáceis de manter.  
  
### <a name="flat-file-format-dynamic-options"></a>Opções dinâmicas do formato de arquivo simples  
  
#### <a name="format--delimited"></a>Formato = Delimitado  
 **Delimitador de linha**  
 Selecione na lista de delimitadores de linha disponíveis ou digite o texto delimitador.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**{CR}{LF}**|As linhas são delimitadas por uma combinação de retorno de carro e avanço de linha.|  
|**{CR}**|As linhas são delimitadas por um retorno de carro.|  
|**{LF}**|As linhas são delimitadas por um avanço de linha.|  
|**Ponto-e-vírgula {;}**|As linhas são delimitadas por um ponto-e-vírgula.|  
|**Dois-pontos {:}**|As linhas são delimitadas por dois-pontos.|  
|**Vírgula {,}**|As linhas são delimitadas por uma vírgula.|  
|**Tabulação {t}**|As linhas são delimitadas por uma tabulação.|  
|**Barra vertical {&#124;}**|As linhas são delimitadas por uma barra vertical.|  
  
 **Delimitador de coluna**  
 Selecione na lista de delimitadores de coluna disponíveis ou digite o texto delimitador.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**{CR}{LF}**|As colunas são delimitadas por uma combinação de retorno de carro e alimentação de linha.|  
|**{CR}**|As colunas são delimitadas por um retorno de carro.|  
|**{LF}**|As colunas são delimitadas por uma alimentação de linha.|  
|**Ponto-e-vírgula {;}**|As colunas são delimitadas por um ponto-e-vírgula.|  
|**Dois-pontos {:}**|As colunas são delimitadas por dois-pontos.|  
|**Vírgula {,}**|As colunas são delimitadas por uma vírgula.|  
|**Tabulação {t}**|As colunas são delimitadas por uma tabulação.|  
|**Barra vertical {&#124;}**|As colunas são delimitadas por uma barra vertical.|  
  
 **Atualizar**  
 Exiba o efeito de alterar os delimitadores a serem ignorados clicando em **Atualizar**. Esse botão só ficará visível após você alterar outras opções de conexão.  
  
 **Visualizar linhas**  
 Exiba os dados de amostra do arquivo simples, dividido em colunas e linhas, usando as opções selecionadas.  
  
 **Redefinir Colunas**  
 Remova todas as colunas, exceto as originais, clicando em **Redefinir Colunas**.  
  
#### <a name="format--fixed-width"></a>Formato = Largura fixa  
 **Fonte**  
 Selecione a fonte em que os dados de visualização serão exibidos.  
  
 **Colunas de dados de origem**  
 Ajuste a largura da linha deslizando o marcador de linha vertical vermelho e ajuste a largura das colunas clicando na régua na parte superior da janela de visualização  
  
 **Largura da linha**  
 Especifique o comprimento da linha antes de adicionar delimitadores para colunas individuais. Você também pode arrastar a linha vermelha vertical na janela de visualização para marcar o fim da linha. O valor de largura da linha é atualizado automaticamente.  
  
 **Redefinir Colunas**  
 Remova todas as colunas, exceto as originais, clicando em **Redefinir Colunas**.  
  
#### <a name="format--ragged-right"></a>Formato = Irregular à direita  
  
> [!NOTE]  
>  Arquivos irregulares à direita são arquivos em que toda coluna tem uma largura fixa, à exceção da última coluna. Ela é delimitada pelo delimitador de linha.  
  
 **Fonte**  
 Selecione a fonte em que os dados de visualização serão exibidos.  
  
 **Colunas de dados de origem**  
 Ajuste a largura da linha deslizando o marcador de linha vertical vermelho e ajuste a largura das colunas clicando na régua na parte superior da janela de visualização  
  
 **Delimitador de linha**  
 Selecione na lista de delimitadores de linha disponíveis ou digite o texto delimitador.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**{CR}{LF}**|As linhas são delimitadas por uma combinação de retorno de carro e avanço de linha.|  
|**{CR}**|As linhas são delimitadas por um retorno de carro.|  
|**{LF}**|As linhas são delimitadas por um avanço de linha.|  
|**Ponto-e-vírgula {;}**|As linhas são delimitadas por um ponto-e-vírgula.|  
|**Dois-pontos {:}**|As linhas são delimitadas por dois-pontos.|  
|**Vírgula {,}**|As linhas são delimitadas por uma vírgula.|  
|**Tabulação {t}**|As linhas são delimitadas por uma tabulação.|  
|**Barra vertical {&#124;}**|As linhas são delimitadas por uma barra vertical.|  
  
 **Redefinir Colunas**  
 Remova todas as colunas, exceto as originais, clicando em **Redefinir Colunas**.  
## <a name="flat-file-connection-manager-editor-advanced-page"></a>Editor do Gerenciador de Conexões de Arquivos Simples (página Avançado)
  Use a página **Avançado** da caixa de diálogo **Editor do Gerenciador de Conexões de Arquivos Simples** para definir propriedades que especificam como o Integration Services lê e grava dados em arquivos simples. Você pode alterar os nomes das colunas no arquivo simples e definir propriedades que incluem tipo de dados e delimitadores em cada coluna no arquivo.  
  
 Por padrão, o tamanho da coluna de cadeia de caracteres é de 50 caracteres. Você pode redimensionar o tamanho dessas colunas para prevenir truncamento de dados ou excesso de largura nas colunas. Também é possível atualizar outros metadados para habilitar a compatibilidade com as colunas de destino. Por exemplo, você pode alterar o tipo de dados de uma coluna que contém apenas dados inteiros para um tipo de dados numérico, como DT_I2. Você pode fazer essas modificações manualmente ou clicar no botão **Selecionar Tipos** para usar a caixa de diálogo **Sugerir Tipos de Coluna** para avaliar dados de amostra e tornar automáticas algumas dessas alterações.  
  
 Para obter mais informações sobre o gerenciador de conexões de Arquivo Simples, consulte [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
### <a name="options"></a>Opções  
 **Nome do gerenciador de conexões**  
 Forneça um nome exclusivo para o gerenciador de conexões de arquivo simples no fluxo de trabalho. O nome fornecido será exibido no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Descrição**  
 Descreva o gerenciador de conexões. Como prática recomendável, descreva o gerenciador de conexões em termos de objetivo, para tornar os pacotes autodocumentados e mais fáceis de manter.  
  
 **Configurar as propriedades de cada coluna**  
 Selecione uma coluna no painel esquerdo para exibir suas propriedades no painel direito. Consulte a tabela a seguir para obter uma descrição das propriedades dos tipos de dados. Algumas das propriedades listadas são configuráveis apenas para alguns formatos de arquivo simples.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|**ColumnType**|Denota se a coluna é delimitada, de largura fixa ou com imperfeição à direita. Esta propriedade é somente leitura. Arquivos irregulares à direita são arquivos em que toda coluna tem uma largura fixa, à exceção da última coluna. Ela é delimitada pelo delimitador de linha.|  
|**OutputColumnWidth**|Especifique um valor a ser armazenado como contagem de bytes; para arquivos Unicode, esse valor corresponde a uma contagem de caracteres. Na tarefa Fluxo de Dados, esse valor é usado para definir a largura de coluna de saída para a fonte de Arquivo Simples. No modelo de objeto, o nome desta propriedade é MaximumWidth.|  
|**DataType**|Seleciona na lista de tipos de dados disponíveis. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).|  
|**TextQualified**|Indique se os dados de texto são delimitados por caracteres qualificadores de texto, como aspas.<br /><br /> True: os dados de texto no arquivo simples são qualificados. False: Os dados de texto no arquivo simples NÃO são qualificados.|  
|**Nome**|Forneça um nome de coluna descritivo. Se você não digitar um nome, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] criará um nome automaticamente, no formato Coluna 0, Coluna 1 e assim por diante.|  
|**DataScale**|Especifica a escala de dados numéricos. A escala se refere ao número de casas decimais. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).|  
|**ColumnDelimiter**|Seleciona na lista de delimitadores de coluna disponíveis. Escolha delimitadores com pouca probabilidade de ocorrer no texto. Esse valor é ignorado para colunas de largura fixa.<br /><br /> **{CR}{LF}**. As colunas são delimitadas por uma combinação de retorno de carro e alimentação de linha.<br /><br /> **{CR}**. As colunas são delimitadas por um retorno de carro.<br /><br /> **{LF}**. As colunas são delimitadas por uma alimentação de linha.<br /><br /> **Porto e vírgula {;}**. As colunas são delimitadas por um ponto-e-vírgula.<br /><br /> **Dois pontos {:}**. As colunas são delimitadas por dois-pontos.<br /><br /> **Vírgula {,}**. As colunas são delimitadas por uma vírgula.<br /><br /> **Tabulação {t}**. As colunas são delimitadas por uma tabulação.<br /><br /> **Barra vertical {&#124;}**. As colunas são delimitadas por uma barra vertical.|  
|**DataPrecision**|Especifica a precisão de dados numéricos. A precisão se refere ao número de dígitos. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).|  
|**InputColumnWidth**|Especifica um valor a ser armazenado como contagem de bytes; no caso de arquivos Unicode, isso será exibido como contagem de caracteres. Este valor é ignorado nas colunas delimitadas.<br /><br /> **Observação** No modelo de objeto, o nome desta propriedade é ColumnWidth.|  
  
 **Nova**  
 Adicione uma nova coluna, clicando em **Nova**. Por padrão, o botão **Nova** adiciona uma nova coluna ao final da lista. O botão também tem as opções a seguir, disponíveis na lista suspensa.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Adicionar Coluna**|Adiciona uma nova coluna fim da lista.|  
|**Insert Before**|Insere uma nova coluna antes da coluna selecionada.|  
|**Insert After**|Insere uma nova coluna depois da coluna selecionada.|  
  
 **Delete (excluir)**  
 Selecione uma coluna e remova-a, clicando em **Excluir**.  
  
 **Sugerir Tipos**  
 Use a caixa de diálogo **Sugerir Tipos de Coluna** para avaliar dados de amostra no arquivo e obter sugestões de tipo de dados e tamanho de cada coluna. Para obter mais informações, consulte [Referência da interface do usuário da caixa de diálogo Sugerir Tipos de Coluna](../../integration-services/connection-manager/suggest-column-types-dialog-box-ui-reference.md).  
## <a name="flat-file-connection-manager-editor-preview-page"></a>Editor do Gerenciador de Conexões de Arquivos Simples (página Visualização)
  Use o nó **Visualização** da caixa de diálogo **Editor do Gerenciador de Conexões de Arquivos Simples** para exibir os conteúdos do arquivo de origem em um formato tabular.  
  
 Para obter mais informações sobre o gerenciador de conexões de Arquivo Simples, consulte [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
### <a name="options"></a>Opções  
 **Nome do gerenciador de conexões**  
 Forneça um nome exclusivo para a conexão de Arquivo Simples no fluxo de trabalho. O nome fornecido será exibido no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Descrição**  
 Descreva a conexão. Como prática recomendável, descreva a conexão em termos de objetivo, para tornar os pacotes autodocumentados e mais fáceis de manter.  
  
 **Linhas de dados a ignorar**  
 Especifique quantas linhas serão ignoradas no início do arquivo simples.  
  
 **Atualizar**  
 Exiba o efeito de alterar o número de linhas a ignorar, clicando em **Atualizar**. Esse botão só ficará visível após você alterar outras opções de conexão.  
  
 **Visualizar linhas**  
 Exiba os dados no arquivo simples, dividido em colunas e linhas, de acordo com as opções que você selecionou.  
 
