---
title: "Conectar a uma fonte de dados de arquivo simples (Assistente de exportação e importação do SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d7e7067b-f5a5-482f-b97e-9d82fe8e9f76
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2f28400200105e8e63f787cbcda58c183ba00da5
ms.openlocfilehash: 568d02ef58102b47501415d35f64369e997e875b
ms.contentlocale: pt-br
ms.lasthandoff: 10/18/2017

---
# <a name="connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard"></a>Conectar a uma fonte de dados de arquivo simples (Assistente de exportação e importação do SQL Server)
Este tópico mostra como se conectar a um **arquivo simples** da fonte de dados (arquivo de texto) do **escolher uma fonte de dados** ou **escolha um destino** página de exportação e importação do SQL Server Assistente. Para arquivos simples, essas duas páginas do Assistente para apresentam conjuntos diferentes de opções, este tópico descreve a origem de arquivo simples e o destino de arquivo simples separadamente.

## <a name="an-alternative-for-simple-text-import"></a>Uma alternativa para importação de texto simples
Se você precisa importar um arquivo de texto no SQL Server, e todas as opções de configuração disponíveis no Assistente de importação e exportação não é necessário, considere o uso de **Importar Assistente de arquivo simples** no SQL Server Management Studio (SSMS). Para saber mais, veja os tópicos a seguir:
- [Novidades do SQL Server Management Studio 17.3](https://blogs.technet.microsoft.com/dataplatforminsider/2017/10/10/whats-new-in-sql-server-management-studio-17-3/)
- [Apresentamos os novo Assistente Importar Arquivo Simples no SQL Server Management Studio 17.3](https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-new-Import-Flat-File-Wizard-in-SSMS-173)

## <a name="connect-to-a-flat-file-source"></a>Conectar a uma fonte de arquivo simples
 
 Há quatro páginas de opções para fontes de dados de arquivo simples. Isso é muito de páginas! Mas você não precisa gastar muito tempo em cada página. Aqui estão as tarefas a serem considerados.
 
Página|Recomendação  |Tipo  
----|---------|---------
**Geral**|Certifique-se de atualizar as opções de **formato** seção.|Recomendado    
**Colunas**|Certifique-se de verificar os delimitadores de coluna e linha (para um arquivo delimitado) ou marcar as colunas (para um arquivo de largura fixa).|Recomendado
**Avançado**|Opcionalmente, verifique os tipos de dados e outras propriedades atribuídas por padrão para as colunas.|Opcional
**Visualização**|Opcionalmente, visualize um exemplo dos dados, usando as configurações que você especificou.|Opcional

## <a name="general-page-source"></a>Página geral (origem)
 Na página **Geral**, navegue para selecionar o arquivo e verifique as configurações na seção **Formato**.
 
 ![Conexão geral de arquivo simples](../../integration-services/import-export-data/media/flat-file-connection-general.png)  

### <a name="options-to-specify-general-page"></a>Opções para especificar (**geral** página)

 **Nome do arquivo**  
 Insira o nome de arquivo e caminho do arquivo simples.  
  
 **Procurar**  
 Localize o arquivo simples.  
  
 **Localidade**  
 Especifique a localidade para fornecer informações específicas do idioma para classificação e de formatos de data e hora.  
  
 **Unicode**  
 Especifique se o arquivo usa o Unicode. Se você usar o Unicode, você não pode especificar uma página de código.  
  
 **Página de código**  
 Especifique a página de código do texto não Unicode.  
  
 **Formato**  
 Selecione se o arquivo usa largura delimitada, fixa ou irregular à direita de formatação.  
  
|Valor|Description|  
|-----------|-----------------|  
|Delimitado|As colunas são separadas por delimitadores. Especifique o delimitador no **colunas** página.|  
|Largura fixa|As colunas têm uma largura fixa.|  
|Irregular à direita|Nos arquivos irregulares à direita, todas as colunas têm uma largura fixa, com exceção da última, que é delimitada pelo delimitador de linha.|  
  
 **Qualificador de texto**  
 Especifique o qualificador de texto, se houver, usado pelo arquivo. Por exemplo, você pode especificar que os campos de texto fiquem entre aspas. (Essa propriedade se aplica somente para arquivos delimitados por.) 
  
> [!NOTE]
> Depois de selecionar um qualificador de texto, você não pode selecionar o **nenhum** opção. Digite **None** para anular a seleção do qualificador de texto.  
  
 **Delimitador de linha de cabeçalho**  
 Selecione na lista de delimitadores de linhas de cabeçalho ou digite o texto do delimitador.  
  
|Value|Description|  
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
 Especifique o número de linhas a ignorar na parte superior do arquivo, se houver.  
  
 **Nomes de coluna na primeira linha de dados**  
 Especifique se a primeira linha (após qualquer linhas ignoradas) contém nomes de coluna.

## <a name="columns-page---format--delimited-source"></a>Página de colunas - formato = delimitado (origem)
 Na página **Colunas**, verifique se a lista de colunas e os delimitadores que o assistente identificou. A captura de tela a seguir mostra a página depois de selecionar **delimitado** como formato de arquivo simples.
 
![Arquivo simples, delimitado, página colunas](../../integration-services/import-export-data/media/flat-file-delimited-columns-page.jpg)

### <a name="options-to-specify-columns-page---format--delimited"></a>Opções para especificar (**colunas** página - formato = delimitado)

 **Delimitador de linha**  
 Selecione na lista de delimitadores de linha disponíveis ou digite o texto delimitador.  
  
|Value|Description|  
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
  
|Value|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|As colunas são delimitadas por uma combinação de retorno de carro e alimentação de linha.|  
|**{CR}**|As colunas são delimitadas por um retorno de carro.|  
|**{LF}**|As colunas são delimitadas por uma alimentação de linha.|  
|**Ponto-e-vírgula {;}**|As colunas são delimitadas por um ponto-e-vírgula.|  
|**Dois-pontos {:}**|As colunas são delimitadas por dois-pontos.|  
|**Vírgula {,}**|As colunas são delimitadas por uma vírgula.|  
|**Tabulação {t}**|As colunas são delimitadas por uma tabulação.|  
|**Barra vertical {&#124;}**|As colunas são delimitadas por uma barra vertical.|  
  
 **Visualizar linhas**  
 Exiba os dados de amostra do arquivo simples, dividido em colunas e linhas, usando as opções selecionadas.  
 
 **Atualizar**  
 Exiba o efeito de alterar os delimitadores a serem ignorados clicando em **Atualizar**. Esse botão só ficará visível após você alterar outras opções de conexão.  
  
 **Redefinir Colunas**  
 Restaure as colunas originais.  

## <a name="columns-page---format--fixed-width-source"></a>Página de colunas - formato = largura fixa (origem)
Na página **Colunas**, verifique se a lista de colunas e os delimitadores que o assistente identificou. A captura de tela a seguir mostra a página depois de selecionar **largura fixa** como formato de arquivo simples.
  
![Arquivo simples, largura, a página colunas fixa](../../integration-services/import-export-data/media/flat-file-fixed-width-columns-page.jpg)

### <a name="options-to-specify-columns-page---format--fixed-width"></a>Opções para especificar (**colunas** página - formato = largura fixa)

 **Fonte**  
 Selecione a fonte em que os dados de visualização serão exibidos.  
  
 **Colunas de dados de origem**  
 Ajuste a largura da linha deslizando o marcador de linha vertical vermelho e ajuste a largura das colunas clicando na régua na parte superior da janela de visualização  
  
 **Largura da linha**  
 Especifique o comprimento da linha antes de adicionar delimitadores para colunas individuais. Você também pode arrastar a linha vermelha vertical na janela de visualização para marcar o fim da linha. O valor de largura da linha é atualizado automaticamente.  
  
 **Redefinir Colunas**  
 Restaure as colunas originais.  
  
## <a name="columns-page---format--ragged-right-source"></a>Página de colunas - formato = irregular à direita (origem)
Na página **Colunas**, verifique se a lista de colunas e os delimitadores que o assistente identificou. A captura de tela a seguir mostra a página depois de selecionar **irregular à direita** como formato de arquivo simples.

> [!NOTE]
> Nos arquivos irregulares à direita, todas as colunas têm uma largura fixa, com exceção da última, que é delimitada pelo delimitador de linha.  
 
![Arquivo simples, irregular à direita, a página colunas](../../integration-services/import-export-data/media/flat-file-ragged-right-columns-page.jpg)

### <a name="options-to-specify-columns-page---format--ragged-right"></a>Opções para especificar (**colunas** página - formato = irregular à direita)
   
 **Fonte**  
 Selecione a fonte em que os dados de visualização serão exibidos.  
  
 **Colunas de dados de origem**  
 Ajuste a largura da linha deslizando o marcador de linha vertical vermelho e ajuste a largura das colunas clicando na régua na parte superior da janela de visualização  
  
 **Delimitador de linha**  
 Selecione na lista de delimitadores de linha disponíveis ou digite o texto delimitador.  
  
|Value|Description|  
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
 Restaure as colunas originais.  

## <a name="advanced-page-source"></a>Página Avançado (origem)
A página **Avançado** mostra informações detalhadas sobre cada coluna na fonte de dados, como o tipo de dados e tamanho. Captura de tela a seguir mostra o **avançado** página da primeira coluna em um arquivo simples delimitado.

![Página de arquivo simples, delimitado, Avançado](../../integration-services/import-export-data/media/flat-file-delimited-advanced-page.jpg)

Na captura de tela, observe que o **id** inicialmente, a coluna que contém números, tem um tipo de dados de cadeia de caracteres.

### <a name="options-to-specify-advanced-page"></a>Opções para especificar (**avançado** página)

 **Configurar as propriedades de cada coluna**  
 Selecione uma coluna no painel esquerdo para exibir suas propriedades no painel direito. Consulte a tabela a seguir para obter uma descrição das propriedades de coluna. Algumas das propriedades listadas são configuráveis apenas para certos formatos de arquivo simples em colunas de certos tipos de dados.  
  
|Propriedade|Description|  
|--------------|-----------------|  
|**Nome**|Forneça um nome de coluna descritivo. Se você não digitar um nome, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria automaticamente um nome no formato de coluna 0, coluna 1 e assim por diante.|
|**ColumnDelimiter**|Seleciona na lista de delimitadores de coluna disponíveis. Escolha delimitadores com pouca probabilidade de ocorrer no texto. Esse valor é ignorado para colunas de largura fixa.<br /><br /> **{CR}{LF}**. As colunas são delimitadas por uma combinação de retorno de carro e alimentação de linha.<br /><br /> **{CR}**. As colunas são delimitadas por um retorno de carro.<br /><br /> **{LF}**. As colunas são delimitadas por uma alimentação de linha.<br /><br /> **Porto e vírgula {;}**. As colunas são delimitadas por um ponto-e-vírgula.<br /><br /> **Dois pontos {:}**. As colunas são delimitadas por dois-pontos.<br /><br /> **Vírgula {,}**. As colunas são delimitadas por uma vírgula.<br /><br /> **Tabulação {t}**. As colunas são delimitadas por uma tabulação.<br /><br /> **Barra vertical {&#124;}**. As colunas são delimitadas por uma barra vertical.|
|**ColumnType**|Denota se a coluna é delimitada, de largura fixa ou com imperfeição à direita. Esta propriedade é somente leitura. Arquivos irregulares à direita são arquivos em que toda coluna tem uma largura fixa, à exceção da última coluna. Ela é delimitada pelo delimitador de linha.|  
|**InputColumnWidth**|Especifique um valor a ser armazenado como uma contagem de bytes. para arquivos Unicode, esse valor é uma contagem de caracteres. Este valor é ignorado nas colunas delimitadas.<br /><br /> **Observação** No modelo de objeto, o nome desta propriedade é ColumnWidth.|
|**DataPrecision**|Especifica a precisão de dados numéricos. A precisão se refere ao número de dígitos.|
|**DataScale**|Especifica a escala de dados numéricos. A escala se refere ao número de casas decimais.|
|**DataType**|Seleciona na lista de tipos de dados disponíveis.<br/>Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).|
|**OutputColumnWidth**|Especifique um valor a ser armazenado como contagem de bytes; para arquivos Unicode, esse valor corresponde a uma contagem de caracteres. Na tarefa Fluxo de Dados, esse valor é usado para definir a largura de coluna de saída para a fonte de Arquivo Simples. No modelo de objeto, o nome desta propriedade é MaximumWidth.|  
|**TextQualified**|Indique se os dados de texto são delimitados por caracteres qualificadores de texto, como aspas.<br /><br /> True: os dados de texto no arquivo simples são qualificados. False: os dados de texto no arquivo simples NÃO são qualificados.|  
  
**Nova**  
 Adicione uma nova coluna, clicando em **Nova**. Por padrão, o botão **Nova** adiciona uma nova coluna ao final da lista. O botão também tem as opções a seguir, disponíveis na lista suspensa.  
  
|Value|Description|  
|-----------|-----------------|  
|**Adicionar Coluna**|Adiciona uma nova coluna fim da lista.|  
|**Insert Before**|Insere uma nova coluna antes da coluna selecionada.|  
|**Insert After**|Insere uma nova coluna depois da coluna selecionada.|  
  
 **Delete (excluir)**  
 Selecione uma coluna e remova-a, clicando em **Excluir**.  
  
 **Sugerir Tipos**  
 Use a caixa de diálogo **Sugerir Tipos de Coluna** para avaliar dados de amostra no arquivo e obter sugestões de tipo de dados e tamanho de cada coluna.  
 
Clique em **Sugerir tipos** para exibir a caixa de diálogo **Sugerir tipos de coluna**. 

![Caixa de diálogo tipos de sugerir de conexão de arquivo simples](../../integration-services/import-export-data/media/flat-file-connection-suggest.png)

Depois de escolher opções de **sugerir tipos de coluna** caixa de diálogo e clique em **Okey**, o assistente pode alterar os tipos de dados de algumas das colunas.

A captura de tela a seguir mostra que, depois de clicar em **sugerir tipos**, o assistente reconheceu que o **id** coluna na fonte de dados é na verdade um número e não uma cadeia de caracteres de texto e alterou o tipo de dados a coluna de uma cadeia de caracteres em um número inteiro.

![Conexão de arquivo simples avançado depois de](../../integration-services/import-export-data/media/flat-file-connection-advanced-after.png)

Para obter mais informações, consulte [sugerir referência da interface do usuário de caixa de diálogo do coluna tipos](../../integration-services/connection-manager/suggest-column-types-dialog-box-ui-reference.md).

## <a name="preview-page-source"></a>Página de visualização (origem)

Na página **Visualização**, verifique se que a lista de colunas e os dados de exemplo são os esperados.

![Arquivo simples, a página de visualização](../../integration-services/import-export-data/media/flat-file-preview-page.jpg)

### <a name="options-to-specify-preview-page"></a>Opções para especificar (**visualização** página)

 **Linhas de dados a ignorar**  
 Especifique quantas linhas serão ignoradas no início do arquivo simples.  
  
 **Visualizar linhas**  
 Exiba os dados no arquivo simples, dividido em colunas e linhas, de acordo com as opções que você selecionou.
 
 **Atualizar**  
 Exiba o efeito de alterar o número de linhas a ignorar, clicando em **Atualizar**. Esse botão só ficará visível após você alterar outras opções de conexão.  
 
Para obter mais informações sobre a página **Visualização**, consulte a seguinte página de referência do Integration Services: [Editor do Gerenciador de Conexões de arquivos simples &#40;página Visualização&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md).

## <a name="connect-to-a-flat-file-destination"></a>Conectar a um destino de arquivo simples
Para um destino de arquivo simples, há apenas uma única página de opções, como mostrado na captura de tela a seguir. Procurar para selecionar o arquivo, em seguida, verifique as configurações no **formato** seção.

![Conecte-se ao destino de arquivo simples](../../integration-services/import-export-data/media/connect-to-flat-file-destination.jpg)

### <a name="options-to-specify-choose-a-destination-page"></a>Opções para especificar (**escolha um destino** página)

 **Nome do arquivo**  
 Insira o nome de arquivo e caminho do arquivo simples.  
  
 **Procurar**  
 Localize o arquivo simples.  
  
 **Localidade**  
 Especifique a localidade para fornecer informações específicas do idioma para classificação e de formatos de data e hora.  
  
 **Unicode**  
 Especifique se o arquivo usa o Unicode. Se você usar o Unicode, você não pode especificar uma página de código.  
  
 **Página de código**  
 Especifique a página de código do texto não Unicode.  
  
 **Formato**  
 Selecione se o arquivo usa largura delimitada, fixa ou irregular à direita de formatação.  
  
|Valor|Description|  
|-----------|-----------------|  
|Delimitado|As colunas são separadas por delimitadores. Especifique o delimitador no **colunas** página.|  
|Largura fixa|As colunas têm uma largura fixa.|  
|Irregular à direita|Nos arquivos irregulares à direita, todas as colunas têm uma largura fixa, com exceção da última, que é delimitada pelo delimitador de linha.|  
  
 **Qualificador de texto**  
 Especifique o qualificador de texto, se houver, usado pelo arquivo. Por exemplo, você pode especificar que os campos de texto fiquem entre aspas. (Essa propriedade se aplica somente para arquivos delimitados por.) 
  
> [!NOTE] 
> Depois de selecionar um qualificador de texto, você não pode selecionar novamente o **nenhum** opção. Digite **None** para anular a seleção do qualificador de texto.  

## <a name="see-also"></a>Consulte também
[Escolha uma fonte de dados](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Escolha um destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


