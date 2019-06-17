---
title: Máscara de Dados Estáticos | Microsoft Docs
ms.date: 04/10/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: a62f4ff9-2953-42ca-b7d8-1f8f527c4d66
author: aliceku
ms.author: aliceku
manager: ajayj
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1cf3b95ec5836ac86770bd0cd9784f0617b91846
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580975"
---
# <a name="static-data-masking"></a>Máscara de Dados Estáticos
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

A Máscara de Dados Estáticos liberada é um componente do [SQL Server Management Studio](../../ssms/sql-server-management-studio-ssms.md) 18.0 versão prévia 5 e superior. 
> [!IMPORTANT]
> Decidimos que nosso protótipo atual não atende a expectativas do nosso cliente. Portanto, não levaremos essa funcionalidade adiante. Atualizaremos a todos sobre nossos planos se tivermos um candidato de substituição.
>



![Mascaramento de dados estáticos](../../relational-databases/security/media/sql-static-data-masking/static_data_masking_intro_image.PNG)


## <a name="what-is-static-data-masking"></a>O que é a Máscara de Dados Estáticos? 
A Máscara de Dados Estáticos é um recurso do SQL Server Management Studio que permite aos usuários criar uma cópia mascarada de um banco de dados. O recurso foi desenvolvido para organizações que precisam compartilhar dados, sendo alguns dos quais confidenciais, entre equipes ou com outras organizações. 

Substituindo dados confidenciais (dados pré-mascaramento) por dados novos (dados pós-mascaramento), a Máscara de Dados Estáticos facilitará os seguintes cenários: 
- Desenvolvimento e teste 
- Análise e relatórios empresariais 
- Solução de problemas 
- Compartilhamento do banco de dados com um consultor, uma equipe de pesquisa ou um terceiro 

O exemplo abaixo mostra como a Máscara de Dados Estáticos funciona na prática. Antes do mascaramento, a coluna contém os números do seguro social. Depois de mascaramento, os primeiros cinco dígitos de cada número do seguro social foram substituídos por números gerados aleatoriamente.

| Número do seguro social dos EUA (pré-mascaramento)   | Número do seguro social (pós-mascaramento)  |
| ------------- | ------------- |
| 140-38-9110 | 302-92-9110 |
| 463-34-5535 | 189-70-5535 |
| 116-30-8733 | 201-01-8733 |
| 209-36-1971 | 683-10-1971 |
| 372-38-6948 | 372-38-6948 |
| 267-64-2334 | 100-03-2334 |
| 523-93-4176 | 582-20-4176 |
| 573-91-5137 | 730-20-5137 |
| 612-72-1026 | 369-40-1026 |

Os usuários da Máscara de Dados Estáticos podem escolher entre várias funções de mascaramento. Dependendo da função de mascaramento, os dados pré e pós-mascaramento podem estar altamente relacionados ou nem um pouco relacionados. Uma função de mascaramento que executa uma ordem aleatória deixará os dados pós-mascaramento altamente relacionados com os dados pré-mascaramento. 

| Número do seguro social dos EUA (pré-mascaramento) | Número do seguro social (pós-mascaramento) |
| ------------- | ------------- |
| 140-38-9110 | 612-72-1026 |  
| 463-34-5535 | 372-38-6948 | 
| 116-30-8733 | 523-93-4176 |
| 209-36-1971 | 209-36-1971 | 
| 372-38-6948 | 140-38-9110 |
| 267-64-2334 | 463-34-5535 | 
| 523-93-4176 | 573-91-5137 | 
| 573-91-5137 | 267-64-2334 | 
| 612-72-1026 | 116-30-8733 |

Uma função de mascaramento que executa uma substituição com valor NULL deixará os dados pós-mascaramento não relacionados com os dados pré-mascaramento. 
 
| Número do seguro social dos EUA (pré-mascaramento) | Número do seguro social (pós-mascaramento) |
| ------------- | ------------- |
| 140-38-9110 | NULL |  
| 463-34-5535 | NULL | 
| 116-30-8733 | NULL |
| 209-36-1971 | NULL | 
| 372-38-6948 | NULL |
| 267-64-2334 | NULL | 
| 523-93-4176 | NULL | 
| 573-91-5137 | NULL | 
| 612-72-1026 | NULL |

## <a name="how-does-static-data-masking-work"></a>Como funciona a Máscara de Dados Estáticos?
A Máscara de Dados Estáticos acontece no nível da coluna. Os usuários selecionam quais colunas eles desejam mascarar e, para cada coluna selecionada, qual função de mascaramento eles desejam aplicar. Há várias funções de mascaramento entre as quais escolher. Elas são descritas detalhadamente em [Funções de mascaramento](#masking-functions). 

A Máscara de Dados Estáticos criará uma cópia do banco de dados. Para o Banco de Dados SQL do Azure, a cópia é realizada por meio da [função copiar](https://azure.microsoft.com/blog/static-data-masking-preview/). Para o SQL Server, ela é executada por meio de uma operação de backup seguida por uma operação de restauração. Daí, para cada coluna, a Máscara de Dados Estáticos começa a substituir os dados pré-mascaramento por dados pós-mascaramento de acordo com a função de mascaramento selecionada. 

A substituição é feita no nível do armazenamento. Em decorrência disso, não será possível recuperar os dados pré-mascaramento da cópia mascarada do banco de dados após a Máscara de Dados Estáticos ser concluída.

## <a name="how-to-guide"></a>Guia de instruções

Veja abaixo um guia passo a passo para executar a Máscara de Dados Estáticos. 
 
1. Inicie o SQL Server Management Studio. Conecte-se ao banco de dados. No painel **Pesquisador de Objetos** do lado esquerdo, expanda a pasta Bancos de dados. Clique com o botão direito do mouse no banco de dados que você deseja mascarar. Clique com o botão esquerdo do mouse em **Tarefas**. Clique com o botão esquerdo do mouse em **Mascarar banco de dados... (versão prévia)** .
 
 ![Menu de tarefas](../../relational-databases/security/media/sql-static-data-masking/task_data_masking.PNG)
 
2. A janela de configuração do mascaramento é aberta. Ela exibirá todas as tabelas no banco de dados. As tabelas são apresentadas por esquema e colocadas em ordem alfabética dentro dele. 
 
 ![Interface do usuário](../../relational-databases/security/media/sql-static-data-masking/ui_dropdown.PNG)
 
3. Clique no ícone suspenso ao lado do nome da tabela para obter uma lista de todas as colunas nela. Para cada coluna na tabela, o tipo de dados da coluna é especificado, além da condição de a coluna ser anulável. Uma coluna anulável é uma coluna que pode receber o valor NULL como uma entrada. 
 
 ![Menu suspenso de tabela](../../relational-databases/security/media/sql-static-data-masking/ui_dropdown_column.png)
 
4. Selecione todas as colunas que você deseja mascarar e a função de mascaramento que você deseja aplicar. Os tipos de mascaramento disponíveis são mascaramento **Ordem aleatória**, **Ordem aleatória de grupo**, **Valor único**, **NULL** e **Composição de cadeia de caracteres**. 
 
 ![Lista suspensa de funções de mascaramento](../../relational-databases/security/media/sql-static-data-masking/masking_functions.PNG)
 
 OBSERVAÇÃO: a maioria dessas funções de mascaramento tem parâmetros de configuração adicionais. Para mascaramento de ordem aleatória, a Máscara de Dados Estáticos oferece um parâmetro padrão. Para o Máscara de ordem aleatória de grupo, Mascaramento de valor único e mascaramento de Composição de cadeia de caracteres, o usuário precisa fornecer parâmetros de configuração. Para alterar ou fornecer parâmetros de configuração, clique na opção **Configurar...** e especifique um valor (alternativo) para o parâmetro na caixa de diálogo que aparece. As descrições detalhadas de cada função de mascaramento são fornecidas em [Funções de mascaramento](#masking-functions).
 
 ![Botão de configuração de funções de mascaramento](../../relational-databases/security/media/sql-static-data-masking/masking_functions_configure.png)
 
 As opções da configuração de mascaramento são validadas para erros relacionados à configuração e ao esquema e avisos imediatos.  Qualquer coisa detectada será exibida como um ícone à esquerda sobre o qual você pode passar o mouse para obter detalhes adicionais. 
 
 No exemplo abaixo, o mascaramento NULL selecionado pelo usuário para uma coluna que não permite valores NULL (restrição NOT NULL).
 
 ![Erro de mecanismo de validação](../../relational-databases/security/media/sql-static-data-masking/validation_mechanism_error_message.PNG)
 
 No exemplo abaixo, o mascaramento de Ordem aleatória de grupo selecionado pelo usuário para apenas uma coluna. Como a Ordem aleatória de grupo exigia no mínimo duas colunas, um aviso foi emitido. 
 
 ![Aviso do mecanismo de validação](../../relational-databases/security/media/sql-static-data-masking/validation_warning.PNG)
 
5. A configuração de mascaramento completa pode ser salva em um arquivo XML para uso posterior.  Embora a configuração da função de mascaramento seja idêntica entre bancos de dados SQL do Azure e locais, há algumas diferenças sutis nas quais outras propriedades (como o caminho do arquivo de backup) são salvas. Para salvar a configuração, clique em **Salvar configuração**, forneça um nome de arquivo e clique em Salvar.  Posteriormente, os usuários podem carregar um arquivo de configuração existente usando **Carregar configuração**. Recomendamos usar arquivos de configuração para tabelas com um grande número de colunas. 
 
 ![Arquivo de configuração](../../relational-databases/security/media/sql-static-data-masking/load_save_config.PNG)
 
6. A Máscara de Dados Estáticos criará uma pasta na pasta **Documentos** do usuário chamada Máscara de Dados Estáticos e inserirá arquivos de log nela. Os arquivos de log podem ser úteis para fins de depuração. O nome do arquivo de log é indicado na parte inferior da janela de configuração. 
  
 
7. (Apenas SQL Server) Se você operar uma Máscara de Dados Estáticos em um banco de dados local, ela executará uma operação de backup/restauração. Na **Etapa 2: Clonar localização do arquivo .BAK**, forneça a localização no servidor em que o arquivo de backup será armazenado. 

## <a name="masking-functions"></a>Funções de mascaramento

### <a name="null-masking"></a>Mascaramento NULL

O mascaramento NULL substitui todos os valores na coluna por NULL. Se a coluna não permitir valores NULL, a ferramenta de Máscara de Dados Estáticos retornará um erro. 

### <a name="single-value-masking"></a>Mascaramento de valor único

O Mascaramento de valor único substitui todos os valores na coluna por um único valor fixo; esse valor é especificado pelo usuário. O formato da entrada deve ser conversível independentemente de qual seja o tipo da coluna selecionada. Para especificar o valor, clique em **Configurar...** , forneça um valor e, em seguida, clique em **OK**. 

![Parâmetro do mascaramento de valor único](../../relational-databases/security/media/sql-static-data-masking/single_value_parameter.PNG)


### <a name="shuffle-masking"></a>Mascaramento de ordem aleatória

Todos os valores na coluna são ordenados aleatoriamente em novas linhas. Nenhum dado novo é gerado. O mascaramento de ordem aleatória oferece a opção de manter entradas NULL na coluna. Para fazer isso, clique em **Configurar...**  e marque a caixa Manter posições NULL.

![Parâmetro de mascaramento de ordem aleatória](../../relational-databases/security/media/sql-static-data-masking/shuffle_parameter.PNG)

Veja abaixo um exemplo do Mascaramento de ordem aleatória com valores NULL não mantido em vigor e, em seguida, mantido em vigor.


| Número do seguro social dos EUA (pré-mascaramento) | Número do seguro social dos EUA (pós-mascaramento com entradas NULL ordenadas aleatoriamente) | Número do seguro social dos EUA (pós-mascaramento com entradas NULL não ordenadas aleatoriamente) |
| ------------- | ------------- | ------------- |
| 116-30-8733 | 612-72-1026 | 463-34-5535 |
| 140-38-9110 | NULL | 573-91-5137  |
| 209-36-1971 | 523-93-4176 | 140-38-9110 |
| NULL | 209-36-1971 | NULL |
| 463-34-5535 | 140-38-9110 | 116-30-8733  |
| 523-93-4176 | 463-34-5535 | 612-72-1026  |
| NULL | 573-91-5137 | NULL |
| 573-91-5137 | NULL | 523-93-4176 |
| 612-72-1026  | 116-30-8733  | 209-36-1971 |  

### <a name="group-shuffle-masking"></a>Mascaramento de ordem aleatória de grupo
A ordem aleatória de grupo associa várias colunas em um grupo de ordem aleatória. As colunas em um grupo de ordem aleatória serão ordenadas aleatoriamente em conjunto. O usuário precisa especificar o nome do grupo de ordem aleatória usando a opção **Configurar...** .

![Parâmetro de mascaramento de ordem aleatória de grupo](../../relational-databases/security/media/sql-static-data-masking/group_shuffle_parameter.PNG)

As ordens aleatórias de grupo acontecem dentro da mesma tabela; se o mesmo nome do grupo de ordem aleatória for usado em várias tabelas, as duas ordens aleatórias do grupo serão ações independentes. O nome do grupo deve ser o mesmo para cada coluna a ser incluída nele. O nome diferencia maiúsculas de minúsculas. Vários grupos de ordem aleatória (com nomes diferentes) podem ocorrer na mesma tabela. 

### <a name="string-composite-masking"></a>Mascaramento de composição de cadeia de caracteres

O Mascaramento de composição de cadeia de caracteres gera cadeias de caracteres aleatórias junto com um padrão. Ele foi criado para cadeias de caracteres que devem seguir um padrão predefinido para ser uma entrada válida. Por exemplo, os números do seguro social americano têm o formato 123-45-6789. A sintaxe para mascaramento de composição de cadeia de caracteres é especificada na caixa de diálogo na qual o usuário precisa inserir o padrão.

![Parâmetro do mascaramento de composição de cadeia de caracteres](../../relational-databases/security/media/sql-static-data-masking/string_composite.PNG)

O Mascaramento de composição de cadeia de caracteres fornece três padrões de exemplo que podem ser testados clicando neles. Se você clicar em Número de telefone, a caixa de padrão será populada automaticamente com a fórmula necessária para gerar números de telefone americanos aleatórios.

![Exemplo de parâmetro do mascaramento de composição de cadeia de caracteres](../../relational-databases/security/media/sql-static-data-masking/string_composite_phone_example.PNG)

O mascaramento de Composição de cadeia de caracteres também tem um modo avançado que permite que subseções dos dados existentes sejam substituídas por cadeias de caracteres geradas pelo padrão. A parte substituída da cadeia de caracteres é determinada pelo grupo de captura em uma expressão regular. Por exemplo, a parte de nome de usuário de um email pode ser substituída preservando o domínio ou o número de telefone pode ser substituído preservando o código de área. Mais informações sobre expressões regulares estão disponíveis [aqui](https://docs.microsoft.com/dotnet/standard/base-types/regular-expression-language-quick-reference).

![Exemplo de parâmetro avançado do mascaramento de composição de cadeia de caracteres](../../relational-databases/security/media/sql-static-data-masking/string_composite_advanced.PNG)

O mascaramento de Composição de cadeia de caracteres e seu modo avançado só pode ser usado para colunas com os [datatypes](../../t-sql/data-types/data-types-transact-sql.md) char, varchar, text, nchar, nvarchar, ntext.

## <a name="limitations"></a>Limitações 

A Máscara de Dados Estáticos tem as seguintes limitações:

- A Máscara de Dados Estáticos não dá suporte a bancos de dados com [tabelas temporais](../../relational-databases/tables/temporal-tables.md).

- A Máscara de Dados Estáticos não mascara tabelas [otimizadas para memória](../../relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables.md).

- A Máscara de Dados Estáticos não mascara [colunas computadas](../../relational-databases/tables/specify-computed-columns-in-a-table.md) nem de [identidade](../../t-sql/statements/create-table-transact-sql-identity-property.md).

- A Máscara de Dados Estáticos não dá suporte a bancos de dados em hiperescala do Azure SQL.

- A Máscara de Dados Estáticos não dá suporte a datatypes de geometria nem de geografia. 

Além disso, a Mascara de Dados Estáticos apresenta três limitações em suas capacidades de mascaramento:

- A Mascara de Dados Estáticos não atualiza [estatísticas de histograma](../../relational-databases/statistics/statistics.md). Consequentemente, a cópia mascarada do banco de dados ainda poderão conter dados confidenciais nas estatísticas de histograma quando a Máscara de Dados Estáticos tiver sido concluída. Considere executar [UPDATE STATISTICS](../../t-sql/statements/update-statistics-transact-sql.md) para corrigir esse problema. 

- Se a Máscara de Dados Estáticos retornar um erro, todas as operações de mascaramento serão suspensas. A cópia do banco de dados não será excluída e poderá conter informações confidenciais. O usuário será responsável por excluir a cópia do banco de dados se a Máscara de Dados Estáticos retornar um erro. 

- (Apenas SQL Server) Os [arquivos de dados](../../relational-databases/databases/database-files-and-filegroups.md) e o [arquivo de log](../../relational-databases/logs/the-transaction-log-sql-server.md) ainda pode conter alguns dados confidenciais na memória não alocada após a conclusão da Máscara de Dados Estáticos. Esses dados confidenciais poderão ser recuperáveis com um editor hexadecimal se receberem acesso ao arquivo de dados e ao arquivo de log.

## <a name="see-also"></a>Consulte Também  
 [Máscara de Dados Dinâmicos](../../relational-databases/security/dynamic-data-masking.md)   
 [Introdução à Máscara de Dados Estáticos do Banco de Dados SQL](https://azure.microsoft.com/documentation/articles/sql-database-static-data-masking-get-started/)  
