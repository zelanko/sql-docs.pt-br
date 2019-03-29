---
title: Conectar-se a uma fonte de dados de arquivo simples (Assistente de Importação e Exportação do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: d7e7067b-f5a5-482f-b97e-9d82fe8e9f76
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a071c773077832c15d41f73764b56c3bac9e5cf0
ms.sourcegitcommit: 5683044d87f16200888eda2c2c4dee38ff87793f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58222130"
---
# <a name="connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard"></a>Conectar-se a uma fonte de dados de arquivo simples (Assistente de Importação e Exportação do SQL Server)
Este tópico mostra como se conectar a uma fonte de dados de **arquivo simples** (arquivo de texto) por meio da página **Escolher uma Fonte de Dados** ou **Escolher um Destino** do Assistente de Importação e Exportação do SQL Server. Para arquivos simples, essas duas páginas do assistente apresentam conjuntos diferentes de opções e, portanto, este tópico descreve a origem de arquivo simples e o destino de arquivo simples separadamente.

## <a name="an-alternative-for-simple-text-import"></a>Uma alternativa para a importação de texto simples
Se precisar importar um arquivo de texto para o SQL Server e não precisar de todas as opções de configuração disponíveis no Assistente de Importação e Exportação, considere a possibilidade de usar o **Assistente Importar Arquivo Simples** no SSMS (SQL Server Management Studio). Para saber mais, veja os tópicos a seguir:
- [Novidades do SQL Server Management Studio 17.3 ](https://blogs.technet.microsoft.com/dataplatforminsider/2017/10/10/whats-new-in-sql-server-management-studio-17-3/)
- [Apresentamos os novo Assistente Importar Arquivo Simples no SQL Server Management Studio 17.3](https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-new-Import-Flat-File-Wizard-in-SSMS-173)

## <a name="connect-to-a-flat-file-source"></a>Conectar-se a uma fonte de arquivo simples
 
 Há quatro páginas de opções para fontes de dados de arquivo simples. São muitas páginas! Mas você não precisa gastar muito tempo em cada página. Veja abaixo as tarefas a serem consideradas.
 
Página|Recomendação  |Tipo  
----|---------|---------
**Geral**|Atualize as opções na seção **Formato**.|Recomendado    
**Colunas**|Marque os delimitadores de coluna e linha (para um arquivo Delimitado) ou marque as colunas (para um arquivo de Largura Fixa).|Recomendado
**Avançado**|Opcionalmente, marque os tipos de dados e outras propriedades atribuídas por padrão às colunas.|Opcional
**Visualização**|Opcionalmente, visualize uma amostra dos dados, usando as configurações especificadas.|Opcional

## <a name="general-page-source"></a>Página Geral (origem)
 Na página **Geral**, navegue para selecionar o arquivo e verifique as configurações na seção **Formato**.
 
 ![Conexão geral de arquivo simples](../../integration-services/import-export-data/media/flat-file-connection-general.png)  

### <a name="options-to-specify-general-page"></a>Opções a serem especificadas (página **Geral**)

 **Nome do arquivo**  
 Insira o caminho e o nome de arquivo do arquivo simples.  
  
 **Procurar**  
 Localize o arquivo simples.  
  
 **Localidade**  
 Especifique a localidade para fornecer informações específicas a um idioma de classificação e formatos de data e hora.  
  
 **Unicode**  
 Especifique se o arquivo usa Unicode. Se você usar Unicode, não poderá especificar uma página de código.  
  
 **Página de código**  
 Especifique a página de código do texto não Unicode.  
  
 **Formato**  
 Selecione se o arquivo usa formatação delimitada, de largura fixa ou irregular à direita.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|Delimitado|As colunas são separadas por delimitadores. Especifique o delimitador na página **Colunas**.|  
|Largura fixa|As colunas têm uma largura fixa.|  
|Irregular à direita|Nos arquivos irregulares à direita, todas as colunas têm uma largura fixa, com exceção da última, que é delimitada pelo delimitador de linha.|  
  
 **Qualificador de texto**  
 Especifique o qualificador de texto, se houver, usado pelo arquivo. Por exemplo, você pode especificar que os campos de texto fiquem entre aspas. (Essa propriedade se aplica somente a arquivos Delimitados.) 
  
> [!NOTE]
> Depois de selecionar um qualificador de texto, não é possível selecionar a opção **Nenhum** novamente. Digite **None** para anular a seleção do qualificador de texto.  
  
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
 Especifique o número de linhas a serem ignoradas na parte superior do arquivo, se houver.  
  
 **Nomes de coluna na primeira linha de dados**  
 Especifique se a primeira linha (após as linhas ignoradas) contém nomes de coluna.

## <a name="columns-page---format--delimited-source"></a>Página Colunas – Formato = Delimitado (origem)
 Na página **Colunas**, verifique se a lista de colunas e os delimitadores que o assistente identificou. A captura de tela a seguir mostra a página após a seleção de **Delimitado** como o formato de arquivo simples.
 
![Arquivo simples, delimitado, página Colunas](../../integration-services/import-export-data/media/flat-file-delimited-columns-page.jpg)

### <a name="options-to-specify-columns-page---format--delimited"></a>Opções a serem especificadas (página **Colunas** – Formato = Delimitado)

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
  
 **Visualizar linhas**  
 Exiba os dados de amostra do arquivo simples, dividido em colunas e linhas, usando as opções selecionadas.  
 
 **Atualizar**  
 Exiba o efeito de alterar os delimitadores a serem ignorados clicando em **Atualizar**. Esse botão só ficará visível após você alterar outras opções de conexão.  
  
 **Redefinir Colunas**  
 Restaure as colunas originais.  

## <a name="columns-page---format--fixed-width-source"></a>Página Colunas – Formato = Largura Fixa (origem)
Na página **Colunas**, verifique se a lista de colunas e os delimitadores que o assistente identificou. A captura de tela a seguir mostra a página após a seleção de **Largura Fixa** como o formato de arquivo simples.
  
![Arquivo simples, largura fixa, página Colunas](../../integration-services/import-export-data/media/flat-file-fixed-width-columns-page.jpg)

### <a name="options-to-specify-columns-page---format--fixed-width"></a>Opções a serem especificadas (página **Colunas** – Formato = Largura Fixa)

 **Fonte**  
 Selecione a fonte em que os dados de visualização serão exibidos.  
  
 **Colunas de dados de origem**  
 Ajuste a largura da linha deslizando o marcador de linha vertical vermelho e ajuste a largura das colunas clicando na régua na parte superior da janela de visualização  
  
 **Largura da linha**  
 Especifique o comprimento da linha antes de adicionar delimitadores para colunas individuais. Você também pode arrastar a linha vermelha vertical na janela de visualização para marcar o fim da linha. O valor de largura da linha é atualizado automaticamente.  
  
 **Redefinir Colunas**  
 Restaure as colunas originais.  
  
## <a name="columns-page---format--ragged-right-source"></a>Página Colunas – Formato = Irregular à Direita (origem)
Na página **Colunas**, verifique se a lista de colunas e os delimitadores que o assistente identificou. A captura de tela a seguir mostra a página após a seleção de **Irregular à Direita** como o formato de arquivo simples.

> [!NOTE]
> Nos arquivos irregulares à direita, todas as colunas têm uma largura fixa, com exceção da última, que é delimitada pelo delimitador de linha.  
 
![Arquivo simples, irregular à direita, página Colunas](../../integration-services/import-export-data/media/flat-file-ragged-right-columns-page.jpg)

### <a name="options-to-specify-columns-page---format--ragged-right"></a>Opções a serem especificadas (página **Colunas** – Formato = Irregular à Direita)
   
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
 Restaure as colunas originais.  

## <a name="advanced-page-source"></a>Página Avançado (origem)
A página **Avançado** mostra informações detalhadas sobre cada coluna na fonte de dados, como o tipo de dados e tamanho. A captura de tela a seguir mostra a página **Avançado** da primeira coluna em um arquivo simples delimitado.

![Arquivo simples, delimitado, página Avançado](../../integration-services/import-export-data/media/flat-file-delimited-advanced-page.jpg)

Na captura de tela, observe que a coluna **id**, que contém números, inicialmente tem um tipo de dados de cadeia de caracteres.

### <a name="options-to-specify-advanced-page"></a>Opções a serem especificadas (página **Avançado**)

 **Configurar as propriedades de cada coluna**  
 Selecione uma coluna no painel esquerdo para exibir suas propriedades no painel direito. Consulte a tabela a seguir para obter uma descrição das propriedades de coluna. Algumas das propriedades listadas são configuráveis apenas em determinados formatos de arquivo simples e em colunas de determinados tipos de dados.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|**Nome**|Forneça um nome de coluna descritivo. Se você não inserir um nome, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] criará um nome automaticamente no formato Coluna 0, Coluna 1 e assim por diante.|
|**ColumnDelimiter**|Seleciona na lista de delimitadores de coluna disponíveis. Escolha delimitadores com pouca probabilidade de ocorrer no texto. Esse valor é ignorado para colunas de largura fixa.<br /><br /> **{CR}{LF}**. As colunas são delimitadas por uma combinação de retorno de carro e alimentação de linha.<br /><br /> **{CR}**. As colunas são delimitadas por um retorno de carro.<br /><br /> **{LF}**. As colunas são delimitadas por uma alimentação de linha.<br /><br /> **Porto e vírgula {;}**. As colunas são delimitadas por um ponto-e-vírgula.<br /><br /> **Dois pontos {:}**. As colunas são delimitadas por dois-pontos.<br /><br /> **Vírgula {,}**. As colunas são delimitadas por uma vírgula.<br /><br /> **Tabulação {t}**. As colunas são delimitadas por uma tabulação.<br /><br /> **Barra vertical {&#124;}**. As colunas são delimitadas por uma barra vertical.|
|**ColumnType**|Denota se a coluna é delimitada, de largura fixa ou com imperfeição à direita. Esta propriedade é somente leitura. Arquivos irregulares à direita são arquivos em que toda coluna tem uma largura fixa, à exceção da última coluna. Ela é delimitada pelo delimitador de linha.|  
|**InputColumnWidth**|Especifique um valor a ser armazenado como uma contagem de bytes; para arquivos Unicode, esse valor é uma contagem de caracteres. Este valor é ignorado nas colunas delimitadas.<br /><br /> **Observação** No modelo de objeto, o nome desta propriedade é ColumnWidth.|
|**DataPrecision**|Especifica a precisão de dados numéricos. A precisão se refere ao número de dígitos.|
|**DataScale**|Especifica a escala de dados numéricos. A escala se refere ao número de casas decimais.|
|**DataType**|Seleciona na lista de tipos de dados disponíveis.<br/>Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).|
|**OutputColumnWidth**|Especifique um valor a ser armazenado como contagem de bytes; para arquivos Unicode, esse valor corresponde a uma contagem de caracteres. Na tarefa Fluxo de Dados, esse valor é usado para definir a largura de coluna de saída para a fonte de Arquivo Simples. No modelo de objeto, o nome desta propriedade é MaximumWidth.|  
|**TextQualified**|Indique se os dados de texto são delimitados por caracteres qualificadores de texto, como aspas.<br /><br /> True: Os dados de texto no arquivo simples são qualificados. False: Os dados de texto no arquivo simples NÃO são qualificados.|  
  
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
 Use a caixa de diálogo **Sugerir Tipos de Coluna** para avaliar dados de amostra no arquivo e obter sugestões de tipo de dados e tamanho de cada coluna.  
 
Clique em **Sugerir tipos** para exibir a caixa de diálogo **Sugerir tipos de coluna**. 

![Caixa de diálogo Sugerir tipos de conexão de arquivo simples](../../integration-services/import-export-data/media/flat-file-connection-suggest.png)

Depois de escolher as opções na caixa de diálogo **Sugerir Tipos de Coluna** e clicar em **OK**, o assistente poderá alterar os tipos de dados de algumas das colunas.

A captura de tela a seguir mostra que, depois que você clicou em **Sugerir tipos**, o assistente reconheceu que a coluna **id** na fonte de dados é, na verdade, um número e não uma cadeia de texto e alterou o tipo de dados da coluna de uma cadeia de caracteres para um inteiro.

![Conexão de arquivo simples avançado depois de](../../integration-services/import-export-data/media/flat-file-connection-advanced-after.png)

Para obter mais informações, consulte [Referência da interface do usuário da caixa de diálogo Sugerir Tipos de Coluna](../../integration-services/connection-manager/suggest-column-types-dialog-box-ui-reference.md).

## <a name="preview-page-source"></a>Página Visualizar (origem)

Na página **Visualização**, verifique se que a lista de colunas e os dados de exemplo são os esperados.

![Arquivo simples, página Visualizar](../../integration-services/import-export-data/media/flat-file-preview-page.jpg)

### <a name="options-to-specify-preview-page"></a>Opções a serem especificadas (página **Visualizar**)

 **Linhas de dados a ignorar**  
 Especifique quantas linhas serão ignoradas no início do arquivo simples.  
  
 **Visualizar linhas**  
 Exiba os dados no arquivo simples, dividido em colunas e linhas, de acordo com as opções que você selecionou.
 
 **Atualizar**  
 Exiba o efeito de alterar o número de linhas a ignorar, clicando em **Atualizar**. Esse botão só ficará visível após você alterar outras opções de conexão.  
 
Para obter mais informações sobre a página **Visualização**, consulte a seguinte página de referência do Integration Services: [Editor do Gerenciador de Conexões de arquivos simples &#40;página Visualização&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md).

## <a name="connect-to-a-flat-file-destination"></a>Conectar-se a um destino de arquivo simples
Para um destino de arquivo simples, há apenas uma única página de opções, conforme mostrado na captura de tela a seguir. Procure para selecionar o arquivo e, em seguida, verifique as configurações na seção **Formato**.

![Conectar-se a um destino de arquivo simples](../../integration-services/import-export-data/media/connect-to-flat-file-destination.jpg)

### <a name="options-to-specify-choose-a-destination-page"></a>Opções a serem especificadas (página **Escolher um Destino**)

 **Nome do arquivo**  
 Insira o caminho e o nome de arquivo do arquivo simples.  
  
 **Procurar**  
 Localize o arquivo simples.  
  
 **Localidade**  
 Especifique a localidade para fornecer informações específicas a um idioma de classificação e formatos de data e hora.  
  
 **Unicode**  
 Especifique se o arquivo usa Unicode. Se você usar Unicode, não poderá especificar uma página de código.  
  
 **Página de código**  
 Especifique a página de código do texto não Unicode.  
  
 **Formato**  
 Selecione se o arquivo usa formatação delimitada, de largura fixa ou irregular à direita.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|Delimitado|As colunas são separadas por delimitadores. Especifique o delimitador na página **Colunas**.|  
|Largura fixa|As colunas têm uma largura fixa.|  
|Irregular à direita|Nos arquivos irregulares à direita, todas as colunas têm uma largura fixa, com exceção da última, que é delimitada pelo delimitador de linha.|  
  
 **Qualificador de texto**  
 Especifique o qualificador de texto, se houver, usado pelo arquivo. Por exemplo, você pode especificar que os campos de texto fiquem entre aspas. (Essa propriedade se aplica somente a arquivos Delimitados.) 
  
> [!NOTE] 
> Depois de selecionar um qualificador de texto, não é possível selecionar a opção **Nenhum** novamente. Digite **None** para anular a seleção do qualificador de texto.  

## <a name="see-also"></a>Confira também
[Escolher uma Fonte de Dados](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Escolher um Destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

