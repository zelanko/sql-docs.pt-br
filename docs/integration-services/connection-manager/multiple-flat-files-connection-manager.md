---
title: "Gerenciador de Conexões de Vários Arquivos Simples | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: connection-manager
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.multifile.advanced.f1
- sql13.dts.designer.multifile.columns.f1
- sql13.dts.designer.multifile.general.f1
- sql13.dts.designer.multifile.preview.f1
helpviewer_keywords:
- Multiple Flat Files connection manager
- connections [Integration Services], flat files
- flat files
- flat file connections [Integration Services]
- connection managers [Integration Services], Multiple Flat Files
- multiple flat file connections
ms.assetid: 31fc3f7a-d323-44f5-a907-1fa3de66631a
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 53e7c263916e9a07504fea6b9756f034e8e570fd
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="multiple-flat-files-connection-manager"></a>Gerenciador de conexões de vários arquivos simples
  Um gerenciador de conexões de Vários Arquivos Simples permite que um pacote acesse dados em vários arquivos simples. Por exemplo, uma fonte de Arquivo Simples pode usar um gerenciador de conexões de Vários Arquivos Simples quando a tarefa Fluxo de Dados está dentro de um contêiner de loop, como o contêiner Loop For. Em cada loop do contêiner, a fonte de Arquivo Simples carrega dados do nome de arquivo seguinte fornecido pelo gerenciador de conexões de Vários Arquivos Simples.  
  
 Quando você adiciona um gerenciador de conexões de Vários Arquivos Simples a um pacote, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria um gerenciador de conexões que resolverá uma conexão de Vários Arquivos Simples no tempo de execução, define as propriedades no gerenciador de conexões de Vários Arquivos Simples e adiciona o gerenciador de conexões de Arquivos Simples Múltiplos à coleção **Connections** do pacote.  
  
 A propriedade **ConnectionManagerType** do gerenciador de conexões é definida como **MULTIFLATFILE**.  
  
 Você pode configurar o gerenciador de conexões de Vários Arquivos Simples da seguinte maneira:  
  
-   Especifique os arquivos, a localidade e a página de código que serão usados. A localidade é usada para interpretar dados confidenciais de localidade como datas, e a página de código é usada para converter dados de cadeia de caracteres para Unicode.  
  
-   Especifique o formato de arquivo. Você pode usar um formato delimitado, de largura fixa ou irregular à direita.  
  
-   Especifique uma linha de cabeçalho, fila de dados e delimitadores de coluna. Delimitadores de coluna podem ser definidos no nível de arquivo e ser sobrescritos no nível de coluna.  
  
-   Indique se a primeira linha nos arquivos contém nomes de coluna.  
  
-   Especifique um caractere de qualificador de texto. Cada coluna pode ser configurada para reconhecer um qualificador de texto.  
  
-   Defina as propriedades, como o nome, o tipo de dados e a largura máxima em colunas individuais.  
  
 Quando o gerenciador de conexões de Vários Arquivos Simples se refere a vários arquivos, os caminhos dos arquivos são separados pelo caractere de pipe (|). A propriedade **ConnectionString** do gerenciador de conexões tem o seguinte formato:  
  
 \<*path*>|\<*path*>  
  
 Você também pode especificar vários arquivos usando curingas. Por exemplo, para fazer referência a todos os arquivos de texto na unidade C, o valor da propriedade **ConnectionString** pode ser definido como C:\\*.txt.  
  
 Se um gerenciador de conexões de Vários Arquivos Simples se referir a vários arquivos, todos os arquivos deverão ter o mesmo formato.  
  
 Por padrão, o gerenciador de conexões de Vários Arquivos Simples define o comprimento de colunas de cadeia de caracteres em 50 caracteres. Na caixa de diálogo do **Editor de Gerenciador de Conexões de Vários Arquivos Simples** , você pode avaliar dados de amostra e redimensionar automaticamente o comprimento dessas colunas para evitar truncamento de dados ou excesso de largura de coluna. A menos que você redimensione o comprimento de coluna na fonte de Arquivo Simples ou na transformação, o comprimento da coluna permanecerá o mesmo ao longo do fluxo de dados. Se essas colunas mapearem para colunas de destino mais estreitas, serão exibidos avisos na interface do usuário, e poderão ocorrer erros no tempo de execução, devido a truncamento de dados. Você pode redimensionar as colunas para que sejam compatíveis com as colunas de destino no gerenciador de conexões de Vários Arquivo, na fonte de Arquivo Simples ou em uma transformação. Para modificar o comprimento de colunas de saída, você define a propriedade **Length** da coluna de saída na guia **Propriedades de Entrada e Saída** na caixa de diálogo **Editor Avançado** .  
  
 Se você atualizar os comprimentos de coluna no gerenciador de conexões de Vários Arquivos Simples depois de adicionar e configurar a fonte de Arquivo Simples que usa o gerenciador de conexões, não será necessário redimensionar as colunas de saída manualmente na fonte de Arquivo Simples. Quando você abre a caixa de diálogo **Origem de Arquivo Simples** , a origem de arquivo simples fornece uma opção para sincronizar os metadados da coluna.  
  
## <a name="configuration-of-the-multiple-flat-files-connection-manager"></a>Configuração do gerenciador de conexões de vários arquivos simples  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter informações sobre como configurar um gerenciador de conexões programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Adicionando conexões programaticamente](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="multiple-flat-files-connection-manager-editor-general-page"></a>Editor do Gerenciador de Conexões de Vários Arquivos Simples (página Geral)
  Use a página **Geral** da caixa de diálogo do **Editor do Gerenciador de Conexões de Vários Arquivos Simples** para selecionar um grupo de arquivos que têm o mesmo formato de dados e para especificar seu formato de dados. Uma conexão de vários arquivos simples habilita um pacote a conectar-se com um grupo de arquivos de texto que têm o mesmo formato.  
  
 Para saber mais sobre o gerenciador de conexões de Vários Arquivos Simples, consulte [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md).  
  
### <a name="options"></a>Opções  
 **Nome do gerenciador de conexões**  
 Forneça um nome exclusivo para a conexão de Vários Arquivos Simples no fluxo de trabalho. O nome fornecido será exibido no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Descrição**  
 Descreva a conexão. Como prática recomendável, descreva a conexão em termos de objetivo, para tornar os pacotes autodocumentados e mais fáceis de manter.  
  
 **Nomes de arquivo**  
 Digite o caminho e o nome de arquivos para usar na conexão de vários arquivos simples. Você pode especificar vários arquivos usando curingas, como no exemplo “C:\\*.txt”, ou usando o caractere de barra vertical (|) para separar vários nomes de arquivo. Todos os arquivos devem ter o mesmo formato de dados.  
  
 **Procurar**  
 Procure os nomes de arquivo para usar na conexão de vários arquivos simples. Você pode selecionar vários arquivos. Todos os arquivos devem ter o mesmo formato de dados.  
  
 **Localidade**  
 Especifique a localidade para fornecer informações de classificação e de conversão de data e hora.  
  
 **Unicode**  
 Indique se deve ser usado o Unicode. O uso do Unicode impede a especificação de uma página de código.  
  
 **Página de código**  
 Especifique a página de código do texto não Unicode.  
  
 **Formato**  
 Indique se será usada formatação delimitada, de largura fixa ou irregular à direita. Todos os arquivos devem ter o mesmo formato de dados.  
  
|Valor|Description|  
|-----------|-----------------|  
|Delimitado|As colunas são separadas por delimitadores, especificados na página **Colunas** .|  
|Largura fixa|As colunas têm uma largura fixa, especificada arrastando as linhas do marcador na página **Colunas** .|  
|Irregular à direita|Em arquivos irregulares à direita, todas as colunas têm uma largura fixa, com exceção da última, que é delimitada pelo delimitador de linha especificado na página **Colunas** .|  
  
 **Qualificador de texto**  
 Especifique o qualificador de texto a ser usado. Por exemplo, você pode especificar incluir o texto entre aspas.  
  
 **Delimitador de linha de cabeçalho**  
 Selecione na lista de delimitadores de linhas de cabeçalho ou digite o texto do delimitador.  
  
|Valor|Description|  
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
 Especifique o número de linhas de cabeçalho a ignorar, caso existam.  
  
 **Nomes de coluna na primeira linha de dados**  
 Indique se deseja esperar ou fornecer nomes de coluna na primeira linha de dados.  
  
## <a name="multiple-flat-files-connection-manager-editor-columns-page"></a>Editor do Gerenciador de Conexões de Vários Arquivos Simples (página Colunas)
  Use o nó **Colunas** da caixa de diálogo **Editor do Gerenciador de Conexões de Vários Arquivos Simples** para especificar as informações da linha e da coluna e visualizar o primeiro arquivo selecionado.  
  
 Para saber mais sobre o gerenciador de conexões de Vários Arquivos Simples, consulte [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md).  
  
### <a name="static-options"></a>Opções estáticas  
 **Nome do gerenciador de conexões**  
 Forneça um nome exclusivo para a conexão de Vários Arquivos Simples no fluxo de trabalho. O nome fornecido será exibido no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Descrição**  
 Descreva a conexão. Como prática recomendável, descreva a conexão em termos de objetivo, para tornar os pacotes autodocumentados e mais fáceis de manter.  
  
### <a name="flat-file-format-dynamic-options"></a>Opções dinâmicas do formato de arquivo simples  
  
#### <a name="format--delimited"></a>Formato = Delimitado  
 **Delimitador de linha**  
 Selecione na lista de delimitadores de linha disponíveis ou digite o texto delimitador.  
  
|Valor|Description|  
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
  
|Valor|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|As colunas são delimitadas por uma combinação de retorno de carro e alimentação de linha.|  
|**{CR}**|As colunas são delimitadas por um retorno de carro.|  
|**{LF}**|As colunas são delimitadas por uma alimentação de linha.|  
|**Ponto-e-vírgula {;}**|As colunas são delimitadas por um ponto-e-vírgula.|  
|**Dois-pontos {:}**|As colunas são delimitadas por dois-pontos.|  
|**Vírgula {,}**|As colunas são delimitadas por uma vírgula.|  
|**Tabulação {t}**|As colunas são delimitadas por uma tabulação.|  
|**Barra vertical {&#124;}**|As colunas são delimitadas por uma barra vertical.|  
  
 **Redefinir Colunas**  
 Remova todas as colunas, exceto as originais, clicando em **Redefinir Colunas**.  
  
#### <a name="format--fixed-width"></a>Formato = Largura fixa  
 **Fonte**  
 Selecione a fonte em que os dados de visualização serão exibidos.  
  
 **Colunas de dados de origem**  
 Ajuste a largura da linha deslizando o marcador de linha vertical e ajuste a largura das colunas clicando na régua na parte superior da janela de visualização  
  
 **Largura da linha**  
 Especifique o comprimento da linha antes de adicionar delimitadores para colunas individuais. Você também pode arrastar a linha vertical na janela de visualização para marcar o fim da linha. O valor de largura da linha é atualizado automaticamente.  
  
 **Redefinir Colunas**  
 Remova todas as colunas, exceto as originais, clicando em **Redefinir Colunas**.  
  
#### <a name="format--ragged-right"></a>Formato = Irregular à direita  
  
> [!NOTE]  
>  Arquivos irregulares à direita são arquivos nos quais toda coluna tem uma largura fixa, à exceção da última coluna. Ela é delimitada pelo delimitador de linha.  
  
 **Fonte**  
 Selecione a fonte em que os dados de visualização serão exibidos.  
  
 **Colunas de dados de origem**  
 Ajuste a largura da linha deslizando o marcador de linha vertical e ajuste a largura das colunas clicando na régua na parte superior da janela de visualização  
  
 **Delimitador de linha**  
 Selecione na lista de delimitadores de linha disponíveis ou digite o texto delimitador.  
  
|Valor|Description|  
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
  
## <a name="multiple-flat-files-connection-manager-editor-advanced-page"></a>Editor do Gerenciador de Conexões de Vários Arquivos Simples (Página Avançado)
  Use a página **Avançado** da caixa de diálogo **Editor do Gerenciador de Conexões de Vários Arquivos Simples** para definir propriedades como o tipo de dados e os delimitadores de cada coluna nos arquivos de texto com os quais o gerenciador de conexões de arquivos simples se conecta.  
  
 Por padrão, o tamanho da coluna de cadeia de caracteres é de 50 caracteres. É possível avaliar os dados de exemplo e automaticamente redimensionar o tamanho dessas colunas para impedir o truncamento de dados ou excesso de largura das colunas. Também é possível atualizar outros metadados para habilitar a compatibilidade com as colunas de destino. Por exemplo, você pode alterar o tipo de dados de uma coluna que contém apenas dados inteiros para um tipo de dados numérico, como DT_I2.  
  
 Para saber mais sobre o gerenciador de conexões de Vários Arquivos Simples, consulte [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md).  
  
### <a name="options"></a>Opções  
 **Nome do gerenciador de conexões**  
 Forneça um nome exclusivo para o gerenciador de conexões de Vários Arquivos Simples no fluxo de trabalho. O nome fornecido será exibido na área **Gerenciadores de Conexões** do Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Descrição**  
 Descreva o gerenciador de conexões. Como prática recomendável, descreva o gerenciador de conexões em termos de objetivo, para tornar os pacotes autodocumentados e mais fáceis de manter.  
  
 **Configurar as propriedades de cada coluna**  
 Selecione uma coluna no painel esquerdo para exibir suas propriedades no painel direito. Consulte a tabela a seguir para obter uma descrição das propriedades dos tipos de dados. Algumas das propriedades listadas são configuráveis apenas para alguns formatos de arquivo simples.  
  
|Propriedade|Description|  
|--------------|-----------------|  
|**ColumnType**|Denota se a coluna é delimitada, de largura fixa ou com imperfeição à direita. Esta propriedade é somente leitura. Nos arquivos irregulares à direita, todas as colunas têm uma largura fixa, com exceção da última, que é encerrada pelo delimitador de linha.|  
|**OutputColumnWidth**|Especifica um valor a ser armazenado como contagem de bytes; no caso de arquivos Unicode, isso será exibido como contagem de caracteres. Na tarefa Fluxo de Dados, esse valor é usado para definir a largura de coluna de saída para a fonte de Arquivo Simples.<br /><br /> Observação: no modelo de objeto, o nome desta propriedade é MaximumWidth.|  
|**DataType**|Seleciona na lista de tipos de dados disponíveis. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).|  
|**TextQualified**|Indica se os dados de texto são qualificados usando um caractere de qualificador de texto:<br /><br /> **True**: os dados de texto no arquivo simples são qualificados.<br /><br /> **False**: os dados de texto no arquivo simples não são qualificados.|  
|**Nome**|Forneça um nome de coluna. O padrão é uma lista numerada das colunas; entretanto, é possível escolher qualquer nome exclusivo e descritivo.|  
|**DataScale**|Especifica a escala de dados numéricos. A escala se refere ao número de casas decimais. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).|  
|**ColumnDelimiter**|Seleciona na lista de delimitadores de coluna disponíveis. Escolha delimitadores com pouca probabilidade de ocorrer no texto. Esse valor é ignorado para colunas de largura fixa.<br /><br /> **{CR}{LF}** – as colunas são delimitadas por uma combinação de retorno de carro e de alimentação de linha<br /><br /> **{CR}** – as colunas são delimitadas por um retorno de carro<br /><br /> **{LF}** – as colunas são delimitadas por uma alimentação de linha<br /><br /> **Ponto e vírgula {;}** – as colunas são delimitadas por um ponto e vírgula<br /><br /> **Dois pontos {:}** – as colunas são delimitadas por dois pontos<br /><br /> **Vírgula {,}** – as colunas são delimitadas por uma vírgula<br /><br /> **Tabulação {t}** – as colunas são delimitadas por uma tabulação<br /><br /> **Barra vertical {&#124;}** – as colunas são delimitadas por uma barra vertical|  
|**DataPrecision**|Especifica a precisão de dados numéricos. A precisão se refere ao número de dígitos. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).|  
|**InputColumnWidth**|Especifica um valor a ser armazenado como contagem de bytes; no caso de arquivos Unicode, isso será exibido como contagem de caracteres. Este valor é ignorado nas colunas delimitadas.<br /><br /> **Observação** No modelo de objeto, o nome desta propriedade é ColumnWidth.|  
  
 **Nova**  
 Adicione uma nova coluna, clicando em **Nova**. Por padrão, o botão **Nova** adiciona uma nova coluna ao final da lista. O botão também tem as opções a seguir, disponíveis na lista suspensa.  
  
|Valor|Description|  
|-----------|-----------------|  
|**Adicionar Coluna**|Adiciona uma nova coluna fim da lista.|  
|**Insert Before**|Insere uma nova coluna antes da coluna selecionada.|  
|**Insert After**|Insere uma nova coluna depois da coluna selecionada.|  
  
 **Delete (excluir)**  
 Selecione uma coluna e remova-a, clicando em **Excluir**.  
  
 **Sugerir Tipos**  
 Use a caixa de diálogo **Sugerir Tipos de Coluna** para avaliar dados de exemplo no primeiro arquivo selecionado e obter sugestões de tipo de dados e tamanho de cada coluna. Para obter mais informações, consulte [Referência da interface do usuário da caixa de diálogo Sugerir Tipos de Coluna](../../integration-services/connection-manager/suggest-column-types-dialog-box-ui-reference.md).  
  
## <a name="multiple-flat-files-connection-manager-editor-preview-page"></a>Editor do Gerenciador de Conexões de Vários Arquivos Simples (página Visualização)
  Use a página **Visualização** da caixa de diálogo **Editor do Gerenciador de Conexões de Vários Arquivos Simples** para ver o conteúdo do primeiro arquivo de origem selecionado, dividido em colunas conforme definido por você.  
  
 Para saber mais sobre o gerenciador de conexões de Vários Arquivos Simples, consulte [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md).  
  
### <a name="options"></a>Opções  
 **Nome do gerenciador de conexões**  
 Forneça um nome exclusivo para a conexão de Vários Arquivos Simples no fluxo de trabalho. O nome fornecido será exibido na área **Gerenciadores de Conexões** do Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Descrição**  
 Descreva a conexão. Como prática recomendável, descreva a conexão em termos de objetivo, para tornar os pacotes autodocumentados e mais fáceis de manter.  
  
 **Linhas de dados a ignorar**  
 Especifique quantas linhas serão ignoradas no início do arquivo simples.  
  
 **Visualizar linhas**  
 Visualize os dados de exemplo do primeiro arquivo simples selecionado, dividido em colunas e linhas, usando as opções selecionadas.  
  
## <a name="see-also"></a>Consulte Também  
 [Origem de Arquivo Simples](../../integration-services/data-flow/flat-file-source.md)   
 [Destino de arquivo simples](../../integration-services/data-flow/flat-file-destination.md)   
 [Conexões do SSIS &#40;Integration Services&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
