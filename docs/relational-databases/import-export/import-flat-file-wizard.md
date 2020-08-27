---
title: Importar Arquivo Simples para SQL | Microsoft Docs
description: O assistente Importar Arquivo Simples é uma forma simples de copiar dados de um arquivo .csv ou .txt para uma nova tabela de banco de dados. Este artigo mostra como e quando usar o assistente.
ms.custom: ''
ms.date: 09/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: data-movement
ms.topic: conceptual
f1_keywords:
- sql13.swb.importflatfile.f1
author: yualan
ms.author: alayu
ms.reviewer: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c083045beaae0d9cbdc6c815723a60093a97431a
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88646038"
---
# <a name="import-flat-file-to-sql-wizard"></a>Assistente Importar Arquivo Simples para SQL
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
> Para obter conteúdo relacionado ao Assistente de Importação e de Exportação, consulte [Assistente de Importação e Exportação do SQL Server](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard).

O Assistente Importar Arquivo Simples fornece uma maneira simples de copiar dados de um arquivo simples (.csv, .txt) para uma nova tabela no seu banco de dados.  O assistente Importar Arquivo Simples é compatível com arquivos de formato de largura fixa e separado por vírgulas. Esta visão geral descreve os motivos para usar esse assistente, como encontrá-lo e um exemplo simples as ser seguido.

## <a name="why-would-i-use-this-wizard"></a>Por que usar esse assistente?
Esse assistente foi criado para melhorar a experiência de importação atual usando uma estrutura inteligente conhecida como [PROSE](https://microsoft.github.io/prose/) (Program Synthesis using Examples). Para um usuário sem conhecimento especializado de domínio, a importação de dados normalmente pode ser uma tarefa complexa, propensa a erros e entediante. Esse assistente simplifica tanto o processo de importação de modo que é necessário apenas selecionar um arquivo de entrada e o nome exclusivo da tabela, deixando que a estrutura PROSE cuide do restante.

O PROSE analisa os padrões de dados no arquivo de entrada para inferir os nomes das colunas, bem como os tipos, os delimitadores e muito mais. Essa estrutura aprende a estrutura do arquivo e faz todo o trabalho pesado, de modo que os usuários não precisem fazê-lo.

Para entender melhor a melhoria na experiência do usuário do Assistente Importar Arquivo Simples, confira este vídeo:

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-new-Import-Flat-File-Wizard-in-SSMS-173/player?WT.mc_id=dataexposed-c9-niner]

## <a name="prerequisites"></a>Pré-requisitos
Este recurso está disponível no SSMS (SQL Server Management Studio) v17.3 ou posterior. Verifique se você está usando a versão mais recente. É possível encontrar a versão mais recente [aqui.](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)
 
## <a name="getting-started"></a><a id="started"></a>Introdução
Para acessar o Assistente Importar Arquivo Simples, siga estas etapas:

1. Abra o **SQL Server Management Studio**.
2. Conecte-se a uma instância do Mecanismo de Banco de Dados do Microsoft SQL Server ou do localhost.
3. Expanda **Bancos de Dados**, clique com o botão direito do mouse em um banco de dados ("test" no exemplo abaixo), aponte para **Tarefas** e clique em **Importar Arquivo Simples** acima de Importar Dados.

![Menu do assistente](media/import-flat-file-wizard/import-flat-file-menu.png)

Para saber mais sobre as diferentes funções do assistente, consulte o seguinte tutorial:

## <a name="tutorial"></a>Tutorial
Para os fins deste tutorial, sinta-se à vontade para usar seu próprio arquivo simples. Caso contrário, este tutorial usará o seguinte CSV do Excel, o qual você pode copiar. Se você usar esse CSV, nomeie-o **example.csv** e salve-o como um CSV em um local fácil, como a área de trabalho.

![Excel do assistente](media/import-flat-file-wizard/import-flat-file-example.png)

Visão geral:
1. [Assistente de acesso](#step-1-access-wizard-and-intro-page)
2. [Especificar Arquivo de Entrada](#step-2-specify-input-file)
3. [Visualizar Dados](#step-3-preview-data)
4. [Modificar Colunas](#step-4-modify-columns)
5. [Resumo](#step-5-summary)
6. [Resultados](#step-6-results)

### <a name="step-1-access-wizard-and-intro-page"></a>Etapa 1: Acessar o assistente e a página Introdução
Acesse o assistente conforme descrito [aqui](#started).

A primeira página do assistente é a página inicial. Se não quiser ver esta página novamente, clique em **Não mostrar esta página inicial novamente.**

![Introdução do assistente](media/import-flat-file-wizard/import-flat-file-intro.png)

### <a name="step-2-specify-input-file"></a>Etapa 2: Especificar Arquivo de Entrada
Clique em Procurar para selecionar o arquivo de entrada. Como padrão, o assistente procura arquivos .csv e .txt. O PROSE detectará se o arquivo é do formato de largura fixa ou separado por vírgulas, independentemente da extensão do arquivo.

O novo nome da tabela deverá ser exclusivo, caso contrário, o assistente não permitirá a continuação do processo.

![Especificação no assistente](media/import-flat-file-wizard/import-flat-file-specify.png)

### <a name="step-3-preview-data"></a>Etapa 3: Visualizar Dados
O assistente gera uma visualização na qual é possível exibir as primeiras 50 linhas. Se houver problemas, clique em Cancelar, caso contrário, prossiga para a próxima página.

![Visualização no assistente](media/import-flat-file-wizard/import-flat-file-preview.png)

### <a name="step-4-modify-columns"></a>Etapa 4: Modificar Colunas
O assistente identifica o que ele acredita que são os nomes corretos das colunas, bem como os tipos de dados, etc. Aqui será possível editar os campos se eles estiverem incorretos (por exemplo, o tipo de dados deve ser um float em vez de um int).

As colunas em que forem detectados valores vazios terão a opção "Permitir Nulos" marcada. No entanto, se você espera nulos em uma coluna e a opção "Permitir Nulos" não está marcada, é aqui que você pode atualizar a definição de tabela para permitir nulos em uma ou em todas as colunas.

Continue quando estiver pronto.

![Modificação no assistente](media/import-flat-file-wizard/import-flat-file-modify.png)

### <a name="step-5-summary"></a>Etapa 5: Resumo
Esta é uma página de resumo que exibe a configuração atual. Se houver problemas, será possível voltar às seções anteriores. Caso contrário, clicar em Concluir iniciará a tentativa de execução do processo de importação.

![Resumo do assistente](media/import-flat-file-wizard/import-flat-file-summary.png)

### <a name="step-6-results"></a>Etapa 6: Resultados
Esta página indica se a importação foi bem-sucedida. Se uma marca de seleção verde aparecer, a operação foi bem-sucedida, caso contrário, talvez seja necessário examinar a configuração ou o arquivo de entrada em busca de erros.

![Resultados do assistente](media/import-flat-file-wizard/import-flat-file-results.png)

## <a name="troubleshooting"></a>Solução de problemas
O Assistente de Importação de Arquivo Simples detecta os tipos de dados com base nas primeiras 200 linhas.  Em cenários em que os dados adicionais do arquivo simples não estiverem em conformidade com os tipos de dados detectados automaticamente, ocorrerá um erro durante a importação. A mensagem de erro exibida é semelhante à seguinte:
```
Error inserting data into table. (Microsoft.SqlServer.Prose.Import)
The given value of type String from the data source cannot be converted to type nvarchar of the specified target column. (System.Data)
String or binary data would be truncated. (System.Data)
```
Táticas para atenuar esse erro:
- Expandir os tamanhos de tipo de dados na etapa [Modificar Colunas](#step-4-modify-columns), como o comprimento de uma coluna nvarchar, pode compensar as variações nos dados do restante do arquivo simples.
- Habilitar o relatório de erros na etapa [Modificar Colunas](#step-4-modify-columns), especialmente com um número menor, revelará quais linhas do arquivo simples contêm dados que não se ajustam aos tipos de dados selecionados. Por exemplo, em um arquivo simples em que a segunda linha apresenta um erro, a execução da importação com o relatório de erros com um intervalo de 1 fornece uma mensagem de erro específica.  Examinar o arquivo diretamente no local pode fornecer as alterações mais direcionadas aos tipos de dados com base nos dados das linhas identificadas.

![Resultados do relatório de erros](media/import-flat-file-wizard/import-flat-file-error.png)

```
Error inserting data into table occured while inserting rows 1 - 2. (Microsoft.SqlServer.Prose.Import)
The given value of type String from the data source cannot be converted to type float of the specified target column. (System.Data)
Failed to convert parameter value from a String to a Double. (System.Data)
```


## <a name="learn-more"></a>Saiba mais

Saiba mais sobre o assistente.
 
- **Saiba mais sobre como importar outras fontes.** Se desejar importar outros itens que não sejam arquivos simples, consulte [Assistente de Importação e Exportação do SQL Server](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard).
- **Saiba mais sobre como conectar-se a fontes de arquivos simples.** Se desejar obter mais informações sobre como conectar-se a fontes de arquivos simples, consulte [Conectar a uma fonte de dados de arquivo simples](https://docs.microsoft.com/sql/integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard).
- **Saiba mais sobre o PROSE.** Se desejar uma visão geral da estrutura inteligente usada por esse assistente, consulte [PROSE SDK](https://microsoft.github.io/prose/).

