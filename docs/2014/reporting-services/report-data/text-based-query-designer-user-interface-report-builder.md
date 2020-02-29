---
title: Interface do usuário do Designer de Consultas baseado em texto (Construtor de Relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10010"
helpviewer_keywords:
- query designers, text-based
ms.assetid: 89fddca5-bd96-4128-9072-5348d1b6e02c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b7453be98f6877f77eb61af4bbd429704816a219
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78172759"
---
# <a name="text-based-query-designer-user-interface-report-builder"></a>Interface de usuário do Designer de Consulta baseado em texto (Construtor de Relatórios)
  Use o designer de consulta baseado em texto para especificar uma consulta usando o idioma de consulta suportado pela fonte de dados, execute a consulta e exiba os resultados no tempo de design. Você pode especificar várias instruções do [!INCLUDE[tsql](../../../includes/tsql-md.md)] , consulta ou sintaxe de comando para as extensões de processamento de dados e consultas que são especificadas como expressões. Como o designer de consulta baseado em texto não processa previamente a consulta e pode acomodar qualquer tipo de sintaxe de consulta, esta é a ferramenta de designer de consulta padrão para muitos tipos de fontes de dados.

> [!IMPORTANT]
>  Os usuários acessam fontes de dados quando criam e executam consultas. Você deve conceder permissões mínimas nas fontes de dados, como permissões somente leitura.

 O designer de consulta baseado em texto exibe uma barra de ferramentas e os dois painéis a seguir:

-   **Consulta** Mostra o texto da consulta, o nome da tabela ou o nome do procedimento armazenado, dependendo do tipo de consulta. Nem todos os tipos de consulta estão disponíveis para todos os tipos de fontes de dados. Por exemplo, nome da tabela tem suporte apenas para o tipo de fonte de dados OLE DB.

-   **Resultado** Mostra os resultados da execução da consulta em tempo de design.

## <a name="text-based-query-designer-toolbar"></a>Barra de ferramentas do Designer de Consulta baseado em texto
 O designer de consulta baseado em texto fornece uma única barra de ferramentas para todos os tipos de comando. A tabela a seguir lista cada botão da barra de ferramentas e suas respectivas funções.

|Botão|Descrição|
|------------|-----------------|
|**Editar como Texto**|Alterna entre o designer de consulta baseado em texto e o designer de consultas gráficas. Nem todos os tipos de fonte de dados dão suporte aos designers de consultas gráficas.|
|**Importaçãoação**|Importa uma consulta existente de um arquivo ou relatório. Apenas os tipos de arquivo .sql e .rdl têm suporte|
|![Executar a consulta](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-run.gif "Executar a consulta")|Executa a consulta e exibe o conjunto de resultados no painel Resultado.|
|**Tipo de Comando**|Selecione **Text**, **StoredProcedure**ou **TableDirect**. Se um procedimento armazenado tiver parâmetros, a caixa de diálogo **Definir Parâmetros de Consulta** será aberta quando você clicar em **Executar** na barra de ferramentas e os valores poderão ser preenchidos conforme necessário.<br /><br /> Observação: se um procedimento armazenado retornar mais de um conjunto de resultados, somente o primeiro deles será usado para popular o conjunto de dados.|

### <a name="command-type-text"></a>Tipo de comando Text
 Quando você cria um conjunto de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o designer de consulta relacional é aberto por padrão. Para mudar para o designer de consulta baseado em texto, clique no botão de alternância **Editar como Texto** na barra de ferramentas. O designer de consulta baseado em texto apresenta dois painéis: Consulta e Resultado. A imagem a seguir define cada painel.

 ![Designer de consultas genérico para consulta de dados relacionais](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqd-dsaw-sql-generic.gif "Designer de consultas genérico para consulta de dados relacionais")

 A tabela a seguir descreve a função de cada painel.

|Painel|Função|
|----------|--------------|
|Consulta|Exibe o texto da consulta do [!INCLUDE[tsql](../../../includes/tsql-md.md)] . Use esse painel para gravar ou editar uma consulta do [!INCLUDE[tsql](../../../includes/tsql-md.md)] .|
|Result|Exibe os resultados da consulta. Para executar a consulta, clique com o botão direito do mouse em qualquer painel e clique em **Executar**ou clique no botão **Executar** na barra de ferramentas.|

#### <a name="example"></a>Exemplo
 A consulta a seguir retorna a lista de sobrenomes [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)]da tabela `ContactType` de banco de `Person` dados **2008** para o esquema.

```
SELECT Name FROM Person.ContactType
```

 Ao clicar em **Executar** , na barra de ferramentas, o comando no painel **Consulta** será executado e os resultados serão exibidos no painel **Resultado** . O conjunto de resultados exibe uma lista de 20 tipos de contatos, por exemplo, Proprietário ou Agente de Vendas.

### <a name="command-type-storedprocedure"></a>Tipo de comando StoredProcedure
 Quando você seleciona o **Comando typeStoredProcedure**, o designer de consulta baseado em texto apresenta dois painéis: Consulta e Resultado. Insira o nome do procedimento armazenado no painel Consulta e clique em **Executar** na barra de ferramentas. Se o procedimento armazenado usar parâmetros, a caixa de diálogo **Definir Parâmetros de Consulta** será aberta. Insira os valores dos parâmetros do procedimento armazenado. Um parâmetro de relatório é criado para cada parâmetro de entrada de procedimento armazenado.

 A figura a seguir mostra os painéis Consulta e Resultados quando você executa um procedimento armazenado. Neste caso, os parâmetros de entrada são constantes.

 ![Procedimento armazenado no designer de consultas baseado em texto](https://docs.microsoft.com/analysis-services/analysis-services/media/rs-relational-text-sp.gif "Procedimento armazenado no designer de consultas baseado em texto")

 A tabela a seguir descreve a função de cada painel.

|Painel|Função|
|----------|--------------|
|Consulta|Exibe o nome do procedimento armazenado e os parâmetros de entrada.|
|Result|Exibe os resultados da consulta. Para executar a consulta, clique com o botão direito do mouse em qualquer painel e clique em **Executar**ou clique no botão **Executar** na barra de ferramentas.|

#### <a name="example"></a>Exemplo
 A consulta a seguir chama [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)]o procedimento `uspGetWhereUsedProductID`armazenado **2008** . Você deve inserir um valor para o parâmetro do número de identificação do produto quando executar a consulta.

```
uspGetWhereUsedProductID
```

 Clique no botão **Executar** (**!**). Quando os parâmetros de consulta forem solicitados, use a seguinte tabela para digitar valores.

|||
|-|-|
|*@StartProductID*|820|
|*@CheckDate*|20010115|

 Para a data especificada, o conjunto de resultados exibe uma lista de 13 identificadores de produtos que usaram o número de componente especificado.

### <a name="command-type-tabledirect"></a>Tipo de comando TableDirect
 Quando você seleciona o **Comando typeTableDirect**, o designer de consulta baseado em texto apresenta dois painéis: Consulta e Resultado. Se você inserir uma tabela e clicar no botão **Executar** , todas as colunas dessa tabela serão retornadas.

#### <a name="example"></a>Exemplo
 Para um tipo de fonte de dados OLE DB, a seguinte consulta de conjunto retorna um conjunto de resultados para todos [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)]os tipos de contato no banco de dados **2008** .

 `Person.ContactType`

 Quando você insere o nome da tabela Person.ContactType, esse procedimento equivale à criação da instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] do `SELECT * FROM Person.ContactType`.

## <a name="see-also"></a>Consulte Também
 [Interface do usuário do designer de consulta relacional &#40;Construtor de Relatórios&#41;](relational-query-designer-user-interface-report-builder.md) [Designers de consulta &#40;Construtor de relatórios&#41;](../query-designers-report-builder.md)


