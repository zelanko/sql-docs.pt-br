---
title: "Opções da solicitação de Perfil de Padrão de Coluna (tarefa Criação de Perfil de Dados) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Data Profiling Task Editor
ms.assetid: 9ccb8fc5-f65e-41a2-9511-7fa55586eb8b
caps.latest.revision: "24"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f51bdacbe57674f10f2dc7ea1c20d1ab64b0c229
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="column-pattern-profile-request-options-data-profiling-task"></a>Opções da solicitação de perfil Padrão de Coluna (tarefa Criação de Perfil de Dados)
  Use o painel **Propriedades da Solicitação** da página **Solicitações de Perfil** para definir as opções da **Solicitação de Perfil de Padrão de Coluna** selecionada no painel de solicitações. Um perfil de Padrão de Coluna informa um conjunto de expressões regulares que cobrem a porcentagem especificada de valores em uma coluna de cadeia de caracteres. Esse perfil pode ajudá-lo a identificar problemas em seus dados, como cadeias de caracteres inválidas, além de sugerir expressões regulares que podem ser usadas posteriormente para validar novos valores. Por exemplo, um perfil de padrão de uma coluna de Códigos Postais dos Estados Unidos pode produzir as expressões regulares \d{5}-\d{4}, \d{5} e \d{9}. Se você vir outras expressões regulares, seus dados provavelmente conterão valores inválidos ou que estão em um formato incorreto.  
  
> [!NOTE]  
>  As opções descritas neste tópico são exibidas na página **Solicitações de Perfil** do **Editor da Tarefa Criação de Perfil de Dados**. Para obter mais informações sobre essa página do editor, consulte [Editor da Tarefa Criação de Perfil de Dados &#40;Página Solicitações de perfil&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md).  
  
 Para obter mais informações sobre como usar a Tarefa Criação de Perfil de Dados, consulte [Configuração da Tarefa Criação de Perfil de Dados](../../integration-services/control-flow/setup-of-the-data-profiling-task.md). Para obter mais informações sobre como usar o Visualizador de Perfil de Dados para analisar a saída da Tarefa Criação de Perfil de Dados, consulte [Visualizador de Perfil de Dados](../../integration-services/control-flow/data-profile-viewer.md).  
  
## <a name="understanding-the-use-of-delimiters-and-symbols"></a>Compreendendo o uso de delimitadores e símbolos  
 Antes de computar os padrões para uma **Solicitação de Perfil de Padrão de Coluna**, a Tarefa Criação de Perfil de Dados gera tokens a partir dos dados. Ou seja, a tarefa separa os valores da cadeia de caracteres em unidades menores conhecidas como tokens. A tarefa separa cadeias de caracteres em tokens com base nos delimitadores e símbolos especificados para as propriedades de **Delimitadores** e **Símbolos** :  
  
-   **Delimitadores** Por padrão, a lista de delimitadores contém os seguintes caracteres: espaço, guia horizontal (\t), nova linha (\n) e retorno de carro (\r). É possível especificar delimitadores adicionais, mas não é possível remover os delimitadores padrão.  
  
-   **Símbolos** Por padrão, a lista de **Símbolos** contém os seguintes caracteres: `,.;:-"'~=&/@!?()<>[]{}|#*^%`, além da marca de escala. Por exemplo, se os símbolos forem "`()-`", será gerado o token ["(", "425", ")", "123", "-", "4567", ")"] para o valor "(425) 123-4567".  
  
 Um caractere não pode ser um delimitador e um símbolo ao mesmo tempo.  
  
 Todos os delimitadores são normalizados em um único espaço como parte do processo de geração de tokens, enquanto os símbolos são retidos.  
  
## <a name="understanding-the-use-of-the-tag-table"></a>Compreendendo o uso da tabela de marcas  
 Como opção, é possível agrupar tokens relacionados com uma única marca armazenando marcas e os seus termos relacionados em uma tabela especial criada em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . É necessário que a tabela de marcas tenha duas colunas de cadeias de caracteres: "Marca" e "Termo". Essas colunas podem ser dos tipos **char**, **nchar**, **varchar**ou **nvarchar**, mas não **text** ou **ntext**. É possível combinar várias marcas e os termos correspondentes em uma única tabela. Uma Solicitação de Perfil de Padrão de Coluna pode usar uma só tabela de marcas. É possível usar um gerenciador de conexões [!INCLUDE[vstecado](../../includes/vstecado-md.md)] separado para se conectar à tabela de marcas. Portanto, a tabela de marcas pode estar localizada em um banco de dados diferente ou em um servidor diferente do banco de dados de origem.  
  
 Por exemplo, é possível agrupar os valores "Leste", "Oeste", "Norte" e "Sul" que podem aparecer em endereços usando uma única marca: "Direção". A tabela a seguir é um exemplo de uma tabela de marcas desse tipo.  
  
|Marca|Termo|  
|---------|----------|  
|Direção|Leste|  
|Direção|Oeste|  
|Direção|Norte|  
|Direção|Sul|  
  
 Também seria possível usar outra marca para agrupar as palavras que especificam o logradouro em endereços:  
  
|Marca|Termo|  
|---------|----------|  
|Logradouro|Logradouro|  
|Logradouro|Avenida|  
|Logradouro|Vila|  
|Logradouro|Travessa|  
  
 Com base nessa combinação de marcas, o padrão resultante para um endereço poderia se assemelhar ao seguinte padrão:  
  
 `\d+\ LookupTag=Direction \d+\p{L}+\ LookupTag=Street`  
  
> [!NOTE]  
>  Usar uma tabela de marcas diminui o desempenho da tarefa Criação de Perfil de Dados. Não use mais de 10 marcas nem mais de 100 termos por marca.  
  
 O mesmo termo pode pertencer a mais de uma marca.  
  
## <a name="request-properties-options"></a>Opções de Propriedades da Solicitação  
 Para uma **Solicitação de Perfil de Padrão de Coluna**, o painel **Propriedades da Solicitação** exibe os seguintes grupos de opções:  
  
-   **Dados**que incluem as opções **TableOrView** e **Column**  
  
-   **Geral**  
  
-   **Opções**  
  
### <a name="data-options"></a>Opções de dados  
 **ConnectionManager**  
 Selecione o gerente de conexões do [!INCLUDE[vstecado](../../includes/vstecado-md.md)] que usa o Provedor de Dados .NET para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) para conexão com o banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contém a tabela ou a exibição que você deseja analisar.  
  
 **TableOrView**  
 Selecione a tabela ou exibição existente que contêm a coluna para a qual será criado um perfil.  
  
 Para obter mais informações, consulte a seção "Opções TableOrView" neste tópico.  
  
 **Column**  
 Selecione a coluna existente para a qual um perfil será criado. Selecione **(\*)** para analisar todas as colunas.  
  
 Para obter mais informações, consulte a seção “Opções Column” neste tópico.  
  
#### <a name="tableorview-options"></a>Opções TableOrView  
 **Esquema**  
 Especifica o esquema ao qual a tabela selecionada pertence. Esta opção é somente leitura.  
  
 **Table**  
 Exibe o nome da tabela selecionada. Esta opção é somente leitura.  
  
#### <a name="column-options"></a>Opções de Coluna  
 **IsWildCard**  
 Especifica se o curinga **(\*)** foi selecionado. Esta opção será definida como **True** se você tiver selecionado **(\*)** para analisar todas as colunas. Será **Falso** se você selecionou uma coluna individual para a criação de um perfil. Esta opção é somente leitura.  
  
 **ColumnName**  
 Exibe o nome da coluna selecionada. Esta opção estará em branco se você tiver selecionado **(\*)** para analisar todas as colunas. Esta opção é somente leitura.  
  
 **StringCompareOptions**  
 Esta opção não é aplicável ao Perfil de Criação de Coluna.  
  
### <a name="general-options"></a>Opções gerais  
 **RequestID**  
 Digite um nome descritivo para identificar esta solicitação de perfil. Normalmente, não é necessário alterar o valor gerado automaticamente.  
  
### <a name="options"></a>Opções  
 **MaxNumberOfPatterns**  
 Especifique o número máximo de padrões que deve ser computado pelo perfil. O valor padrão desta opção é 10. O valor máximo é 100.  
  
 **PercentageDataCoverageDesired**  
 Especifique a porcentagem dos dados a ser coberta pelos padrões computados. O valor padrão desta opção é 95 (por cento).  
  
 **CaseSensitive**  
 Indique se os padrões deveriam fazer distinção entre letras maiúsculas e minúsculas. O valor padrão desta opção é **False**.  
  
 **Delimitadores**  
 Liste os caracteres que deveriam ser tratados como equivalentes a espaços entre palavras ao gerar tokens para texto. Por padrão, a lista de **Delimitadores** contém os seguintes caracteres: espaço, guia horizontal (\t), nova linha (\n) e retorno de carro (\r). É possível especificar delimitadores adicionais, mas não é possível remover os delimitadores padrão.  
  
 Para obter mais informações, consulte "Compreendendo o uso de delimitadores e símbolos" anteriormente neste tópico.  
  
 **Símbolos**  
 Liste os símbolos que deveriam ser retidos como parte de padrões. Exemplos poderiam incluir "/" para datas, ":" para horários e "@" para endereços de email. Por padrão, a lista de **Símbolos** contém os seguintes caracteres: `,.;:-"'~=&/@!?()<>[]{}|#*^%`.  
  
 Para obter mais informações, consulte "Compreendendo o uso de delimitadores e símbolos" anteriormente neste tópico.  
  
 **TagTableConnectionManager**  
 Selecione o gerenciador de conexões existente do [!INCLUDE[vstecado](../../includes/vstecado-md.md)] que usa o Provedor de Dados .NET para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) se conectar ao banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contém a tabela de marcações.  
  
 Para obter mais informações, consulte "Compreendendo o uso da tabela de marcas" anteriormente neste tópico.  
  
 **TagTableName**  
 Selecione a tabela de marcas existente, a qual deve ter duas colunas de cadeia de caracteres: Marca e Termo.  
  
 Para obter mais informações, consulte "Compreendendo o uso da tabela de marcas" anteriormente neste tópico.  
  
## <a name="see-also"></a>Consulte também  
 [Editor da tarefa Criação de Perfil de Dados &#40;Página Geral&#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [Formulário de Perfil Rápido de Tabela Única &#40;Tarefa Criação de Perfil de Dados&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  
