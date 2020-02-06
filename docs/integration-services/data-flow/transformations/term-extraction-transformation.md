---
title: Transformação Extração de Termos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.termextractiontrans.f1
- sql13.dts.designer.termextraction.termextraction.f1
- sql13.dts.designer.termextraction.inclusionexclusion.f1
- sql13.dts.designer.termextraction.advanced.f1
helpviewer_keywords:
- word boundaries [Integration Services]
- extracting data [Integration Services]
- sentence boundaries
- word extractions [Integration Services]
- Term Extraction transformation
- tagging words
- normalized data [Integration Services]
- tokenizing text [Integration Services]
- parts of speech [Integration Services]
- text extraction [Integration Services]
- term extractions [Integration Services]
- stemming words [Integration Services]
ms.assetid: d0821526-1603-4ea6-8322-2d901568fbeb
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 23ae71eff12e7155580eff8238a459c47211c5de
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71297752"
---
# <a name="term-extraction-transformation"></a>Transformação Extração de Termos

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  A transformação Extração de Termo extrai termos de texto em uma coluna de entrada de transformação e grava os termos em uma coluna de saída de transformação. A transformação trabalha apenas com texto em inglês e usa seu próprio dicionário de inglês e informações linguísticas sobre o inglês.  
  
 Você pode usar a transformação Extração de Termos para descobrir o conteúdo de um conjunto de dados. Por exemplo, texto que contém mensagens de email pode fornecer comentários úteis sobre produtos, possibilitando o uso da transformação Extração de Termos para extrair os tópicos de discussão nas mensagens, como forma de analisar os comentários.  
  
## <a name="extracted-terms-and-data-types"></a>Termos e tipos de dados extraídos  
 A transformação Extração de Termos só pode extrair substantivos, frases apenas nominais, tanto substantivos quanto frases nominais. Um substantivo é um substantivo único; uma frase nominal são pelo menos duas palavras, das quais uma é um substantivo e a outra é um substantivo ou um adjetivo. Por exemplo, se a transformação usar a opção só substantivos, extrairá termos como *bicicleta* e *paisagem*; se a transformação usar a opção de frase nominal, extrairá termos como *bicicleta azul nova*, *capacete de bicicleta*e *bicicletas encaixotadas*.  
  
 Não são extraídos artigos e pronomes. Por exemplo, a transformação Extração de Termos extrai o termo *bicicleta* do texto *a bicicleta*, *minha bicicleta*e *aquela bicicleta*.  
  
 A transformação Extração de Termos gera uma contagem para cada termo que extrai. A contagem pode ser um valor de TFIDF ou a frequência bruta, significando o número de vezes que o termo normalizado aparece na entrada. Nesse caso, a contagem é representada por um número real que é maior do que 0. Por exemplo, a pontuação de TFIDF poderia ter o valor 0,5, e a frequência seria um valor como 1,0 ou 2,0.  
  
 A saída da transformação Extração de Termos inclui apenas duas colunas. Uma coluna contém os termos extraídos e a outra coluna contém a pontuação. Os nomes padrão das colunas são **Termo** e **Pontuação**. Como a coluna de texto na entrada pode conter múltiplos termos, a saída da transformação Extração de Termos geralmente tem mais linhas que a entrada.  
  
 Se os termos extraídos forem gravados em uma tabela, eles podem ser usados por outra transformação de pesquisa como a Pesquisa de Termos, Pesquisa Difusa e transformações de Pesquisa.  
  
 A transformação Extração de Termos só pode trabalhar com texto em uma coluna que tenha ou DT_WSTR ou o tipo de dados DT_NTEXT. Se uma coluna contiver texto, mas não tiver um desses tipos de dados, a transformação Conversão de Dados pode adicionar uma coluna com tipo de dados DT_WSTR ou DT_NTEXT para o fluxo de dados e copiar os valores da coluna para a nova coluna. A saída da transformação Conversão de Dados pode, então, ser usada como entrada para a transformação Extração de Termos. Para obter mais informações, consulte [Data Conversion Transformation](../../../integration-services/data-flow/transformations/data-conversion-transformation.md).  
  
## <a name="exclusion-terms"></a>Exclusão de termos  
 Além disso, a transformação Extração de Termos pode referir-se a uma coluna em uma tabela que contenha termos de exclusão, significando termos que a transformação não deve considerar ao extrair termos de um conjunto de dados. Isso é útil quando um conjunto de termos já foi identificado como inconsequente em um negócio específico e na indústria, porque o termo ocorre com uma frequência tão alta que se torna uma palavra de ruído. Por exemplo, ao extrair termos de um conjunto de dados que contém informações de apoio ao cliente sobre uma marca específica de carros, a própria marca poderá ser excluída porque a marca é mencionada com muita frequência e significativa. Portanto, os valores na lista de exclusão devem ser personalizados conforme o conjunto de dados com o qual está trabalhando.  
  
 Quando você adiciona um termo à lista de exclusões, todos os termos, como palavras ou frases nominais, que contêm o termo também são excluídos. Por exemplo, se a lista de exclusões incluir a apenas a palavra *dados*então, todos os termos que contenham essa palavra, como *dados*, *mineração de dados*, *integridade de dados*e *validade de dados* também serão excluídos. Se você quiser excluir apenas compostos que contenham a palavra *dados*, será necessário adicionar esses termos compostos explicitamente na lista de exclusões. Por exemplo, se você quisesse extrair incidências de *dados*, mas excluir *validação de dados*, você adicionaria *validação de dados* à lista de exclusão e teria certeza de que o termo *dados* seria removido da lista de exclusões.  
  
 A tabela de referência deve ser uma tabela em um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou do Access. A transformação Extração de Termos utiliza uma conexão OLE DB separada para conectar-se à tabela de referência. Para obter mais informações, consulte [OLE DB Connection Manager](../../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
 A transformação Extração de Termos trabalha em um modo completamente pré-protegido. No momento da execução, a transformação Extração de Termos lê os termos de exclusão da tabela de referência e os armazena em sua memória privada antes que processe qualquer linha de entrada de transformação.  
  
## <a name="extraction-of-terms-from-text"></a>Extrações de termos de texto  
 Para extrair termos do texto, a transformação Extração de Termos executa as seguintes tarefas.  
  
### <a name="identification-of-words"></a>Identificação de palavras  
 Primeiro, a transformação Extração de Termos identifica palavras executando as seguintes tarefas:  
  
-   Separando o texto em palavras usando espaços, quebras de linha e outros delimitadores vocabulares da língua inglesa. Por exemplo, sinais de pontuação tais como *?* e *:* são caracteres delimitadores de palavras.  
  
-   Preservando palavras que estão conectadas por hífens ou sublinhadas. Por exemplo, as palavras *protegido por cópia* e *somente leitura* permanecem como uma palavra simples.  
  
-   Mantendo intactos os acrônimos que incluem pontos. Por exemplo, a Empresa *A.B.C* seria simbolizada por **ABC** e **Empresa**.  
  
-   Separando palavras com caracteres especiais. Por exemplo, a palavra *data/hora* é extraída como *data* e *hora*, *(bicicleta)* como *bicicleta*, e C# é tratado como C. Caracteres especiais são descartados e não podem ser interpretados como palavras.  
  
-   Reconhecendo quando caracteres especiais como o apóstrofo não devem separar palavras. Por exemplo, a palavra *bicicletas* não é separada em duas palavras e resulta no termo simples *bicicleta* (substantivo).  
  
-   Separando expressões de tempo, expressões monetárias, endereços de email e endereços postais. Por exemplo, a data *31 de janeiro de 2004* é separada em três marcas *janeiro*, *31*e *2004*.  
  
### <a name="tagged-words"></a>Palavras marcadas  
 Segundo, a transformação Extração de Termos marca as palavras como uma das seguintes classes gramaticais:  
  
-   Um substantivo na forma singular. Por exemplo, *bicicleta* e *batata*.  
  
-   Um substantivo na forma plural. Por exemplo, *bicicletas* e *batatas*. Todos os substantivos plurais que não são objetivados estão sujeitos a reduzirem-se à forma do radical.  
  
-   Um substantivo próprio na forma singular. Por exemplo, *abril* e *Peter*.  
  
-   Um substantivo próprio na forma plural. Por exemplo *abris* e *Peters*. Para um substantivo próprio ficar sujeito a reduzir-se à forma de radical, ele deve ser uma parte do léxico interno, que esteja limitado a palavras da língua inglesa padrão.  
  
-   Um adjetivo. Por exemplo, *azul*.  
  
-   Um adjetivo comparativo que compara dois termos. Por exemplo, *mais elevado* e *mais alto*.  
  
-   Um adjetivo superlativo que identifica um termo que tem uma qualidade acima ou abaixo do nível de pelo menos dois outros. Por exemplo, *o mais elevado* e *o mais alto*.  
  
-   Um número. Por exemplo, *62* e *2004*.  
  
 Palavras que não sejam nenhuma destas classes gramaticais estão descartadas. Por exemplo, verbos e pronomes estão descartados.  
  
> [!NOTE]  
>  A marcação de classes gramaticais é baseada em um modelo estatístico e a marcação pode não ser completamente precisa  
  
 Se a transformação Extração de Termos for configurada para só extrair substantivos, apenas as palavras que estiverem marcadas como formas singulares ou plurais de substantivos e os substantivos próprios são extraídos.  
  
 Se a transformação Extração de Termos for configurada para só extrair frases nominais, as palavras que estiverem marcadas como substantivos, substantivos próprios, adjetivos e numerais podem ser combinadas para formar uma frase nominal, mas a frase deve incluir ao menos uma palavra que esteja marcada como uma forma singular ou plural de um substantivo ou um substantivo próprio. Por exemplo, a frase nominal *a montanha mais alta* combina uma palavra marcada como um adjetivo superlativo (*mais alta*) e uma palavra marcada como substantivo (*montanha*).  
  
 Se Extração de Termos for configurada para extrair tanto substantivos quanto frases nominais, aplicam-se tanto as regras para substantivos quanto as regras para frases nominais. Por exemplo, a transformação extrai *bicicleta* e *bonita bicicleta azul* do texto *muitas bicicletas azuis bonitas*.  
  
> [!NOTE]  
>  Os termos extraídos continuam sujeitos ao tamanho máximo de termos e ao limite de frequência que a transformação utiliza.  
  
### <a name="stemmed-words"></a>Palavras reduzidas  
 A transformação Extração de Termos também reduz substantivos para extrair apenas a forma singular de um substantivo. Por exemplo, a transformação extrai *homem* de *homens*, *rato* de *ratos*e *bicicleta* de *bicicletas*. A transformação usa seu dicionário para reduzir os substantivos. Gerúndios são tratados como substantivos caso estejam no dicionário.  
  
 A transformação Extração de Termos reduz palavras até sua forma do dicionário conforme mostrado nestes exemplos por meio do uso do dicionário interno à transformação Extração de Termos.  
  
-   Removendo *s* de substantivos. Por exemplo, *bicicletas* torna-se *bicicleta*.  
  
-   Removendo *es* de substantivos. Por exemplo, *histórias* torna-se *história*.  
  
-   Recuperando a forma singular de substantivos irregulares a partir do dicionário. Por exemplo, *gansos* torna-se *ganso*.  
  
### <a name="normalized-words"></a>Palavras normalizadas  
 A transformação Extração de Termos normaliza termos que só aparecem com inicial em maiúscula por causa de sua posição em uma oração e, ao invés disso, utiliza a forma sem inicial em minúscula. Por exemplo, nas orações *Cachorros perseguem bolas* e *Caminhos de montanha são íngremes*, seriam normalizadas *Cachorros* e *Montanha* para *cachorro* e *montanha*.  
  
 A transformação Extração de Termos normaliza palavras de forma que as versões de palavras com inicial em maiúscula ou normal não sejam tratadas como termos diferentes. Por exemplo, no texto *Você vê muitas bicicletas em Seattle* e *Bicicletas são azuis*, *bicicletas* e *Bicicletas* são reconhecidas como o mesmo termo e a transformação só mantém *bicicleta*. Substantivos próprios e palavras que não estão listadas no dicionário interno não são normalizados.  
  
### <a name="case-sensitive-normalization"></a>Normalização de maiúsculas e minúsculas  
 A transformação Extração de Termos pode ser configurada para considerar palavras com inicial minúscula e maiúscula ou como termos distintos, ou como variantes diferentes do mesmo termo.  
  
-   Se a transformação for configurada para reconhecer diferenças de maiúsculas ou minúsculas, termos como *Método* e *método* serão extraídos como dois termos distintos. Nunca são normalizadas palavras com inicial em maiúscula que não sejam a primeira palavra em uma oração, sendo marcadas como substantivos próprios.  
  
-   Se a transformação for configurada para ser sensível a iniciais maiúsculas e minúsculas, termos como *Método* e *método* serão reconhecidos como variantes de um único termo. A lista de termos extraídos poderia incluir ou *Método* ou *método*, dependendo de qual palavra ocorra primeiro no conjunto de dados de entrada. Se *Método* estiver com inicial em maiúscula apenas porque é a primeira palavra em uma oração, será extraído na forma normalizada.  
  
## <a name="sentence-and-word-boundaries"></a>Oração e limites de vocábulos  
 A transformação Extração de Termos separa o texto em orações que usam os caracteres seguintes como limites de oração:  
  
-   Caracteres 0x0d de quebra de linha ASCII (retorno de carro) e 0x0a (avanço de linha). Para usar esse caractere como um limite de orações, deve haver dois ou mais caracteres de quebra de linha consecutivos.  
  
-   Hifens (-). Para usar esse caractere como um limite de orações,  nem o caractere à esquerda nem à direita do hífen pode ser uma letra.  
  
-   Sublinhado (_). Para usar esse caractere como um limite de orações,  nem o caractere à esquerda nem à direita do hífen pode ser uma letra.  
  
-   Todos os caracteres de Unicode que sejam menores ou iguais a 0x19, ou maiores ou iguais a 0x7b.  
  
-   Combinações de números, sinais de pontuação e caracteres alfabéticos. Por exemplo, *A23B#99* retorna o termo *A23B*.  
  
-   Os caracteres, %, @, &, $, #, \*, :, ;, ., **,** , !, ?, \<, >, +, =, ^, ~, |, \\, /, (, ), [, ], {, }, " e '.  
  
    > [!NOTE]  
    >  Acrônimos que contêm um ou mais pontos (.) não são separados em várias sentenças.  
  
 A transformação Extração de Termos separa a sentença em palavras usando o seguinte limite de palavra:  
  
-   Space  
  
-   Tab  
  
-   ASCII 0x0d (retorno de carro)  
  
-   ASCII 0x0a (alimentação de linha)  
  
    > [!NOTE]  
    >  Se um apóstrofo estiver em uma palavra que seja uma contração, como *we're* ou *it's*, a palavra será quebrada até o apóstrofo; caso contrário, as letras que seguem o apóstrofo serão cortados. Por exemplo, *we're* é divido em *we* e *'re*e *bicycle’s* é cortada para *bicycle*.  
  
## <a name="configuration-of-the-term-extraction-transformation"></a>Configuração da transformação Extração de Termos  
 A transformação Extração de Texto utiliza algoritmos internos e modelos estatísticos para gerar seus resultados. Você pode ter que executar a transformação  Extração de Termos várias vezes e examinar os resultados para configurar a transformação, a fim de gerar o tipo de resultados que funcione para sua solução para filtragem de texto.  
  
 A transformação Extração de Termos tem uma entrada normal, uma saída e uma saída de erros.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propriedades personalizadas de Transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Para obter mais informações sobre como definir as propriedades, consulte [Definir as propriedades de um componente de fluxo de dados](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="term-extraction-transformation-editor-term-extraction-tab"></a>Editor de Transformação Extração de Termos (guia Extração de Termos)
  Use a guia **Extração de Termos** da caixa de diálogo **Editor de Transformação Extração de Termos** para especificar uma coluna de texto que contém texto a ser extraído.  
  
### <a name="options"></a>Opções  
 **Colunas de Entrada Disponíveis**  
 Usando as caixas de seleção, selecione uma única coluna de texto a ser utilizada para extração de termos.  
  
 **Termo**  
 Forneça um nome para a coluna de saída que conterá os termos extraídos.  
  
 **Pontuação**  
 Forneça um nome para a coluna de saída que conterá a pontuação de cada termo extraído.  
  
 **Configurar Saída de Erro**  
 Use a caixa de diálogo [Configurar Saída de Erro](https://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) para especificar tratamento de erro em linhas que causam erros.  
  
## <a name="term-extraction-transformation-editor-exclusion-tab"></a>Editor de Transformação Extração de Termos (guia Exclusão)
  Use a guia **Exclusão** da caixa de diálogo do **Editor de Transformação Extração de Termos** para definir uma conexão com uma tabela de exclusão e especificar as colunas que contêm termos de exclusão.  
  
### <a name="options"></a>Opções  
 **Usar termos de exclusão**  
 Indique se devem ser excluídos termos específicos durante uma extração de termos especificando uma coluna que contém termos de exclusão. Você deve especificar as seguintes propriedades de origem caso opte por excluir termos.  
  
 **Gerenciador de conexões OLE DB**  
 Selecione um gerenciador de conexões OLE DB existente ou crie uma nova conexão clicando em **Novo**.  
  
 **Novo**  
 Crie uma nova conexão com um banco de dados usando a caixa de diálogo **Configurar Gerenciador de Conexões OLE DB** .  
  
 **Tabela ou exibição**  
 Selecione a tabela ou exibição que contém os termos de exclusão.  
  
 **Coluna**  
 Selecione a coluna na tabela ou exibição que contém os termos de exclusão.  
  
 **Configurar Saída de Erro**  
 Use a caixa de diálogo [Configurar Saída de Erro](https://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) para especificar tratamento de erro em linhas que causam erros.  
  
## <a name="term-extraction-transformation-editor-advanced-tab"></a>Editor de Transformação Extração de Termos (guia Avançado)
  Use a guia **Avançado** da caixa de diálogo **Editor de Transformação de Extração de Termos** para especificar propriedades de extração, como frequência, comprimento e se devem ser extraídas palavras ou frases.  
  
### <a name="options"></a>Opções  
 **Substantivo**  
 Especifique que a transformação só extrai substantivos individuais.  
  
 **Frase substantivada**  
 Especifique que a transformação só extraia frases substantivadas.  
  
 **Substantivo e frase substantivada**  
 Especifique que a transformação extraia tanto substantivos como frases substantivadas.  
  
 **Frequência**  
 Especifique que a pontuação é a frequência do termo.  
  
 **TFIDF**  
 Especifique que a pontuação é o valor TFIDF do termo. A pontuação TFIDF é o produto da Frequência do Termo e da Frequência de Documento Inversa, definido como: TFIDF de um termo T = (frequência de T) * log ((nºs de linhas na Entrada) / (nº de linhas com T))  
  
 **Limite de frequência**  
 Especifique o número de vezes que uma palavra ou frase deve aparecer antes de ser extraída. O valor padrão é 2.  
  
 **Comprimento máximo do termo**  
 Especifique o comprimento máximo de uma frase em palavras. Esta opção só afeta frases substantivadas. O valor padrão é 12.  
  
 **Usar extração de termos com diferenciação de maiúsculas e minúsculas**  
 Especifique se a extração deve ser feita diferenciando maiúsculas e minúsculas. O padrão é **False**.  
  
 **Configurar Saída de Erro**  
 Use a caixa de diálogo [Configurar Saída de Erro](https://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) para especificar tratamento de erro em linhas que causam erros.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de mensagens e erros do Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Transformação Pesquisa de Termos](../../../integration-services/data-flow/transformations/term-lookup-transformation.md)  

