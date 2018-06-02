---
title: No banco de dados a análise de R para desenvolvedores em SQL (tutorial) | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e1ff2799ba37c97f5ff82c1c15cdeb986220a947
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34585268"
---
# <a name="in-database-r-analytics-for-sql-developers-tutorial"></a>Análise de R no banco de dados para desenvolvedores do SQL (tutorial)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

O objetivo deste tutorial é fornecer os programadores SQL com experiência prática na criação de uma solução no SQL Server de aprendizado de máquina. Neste tutorial, você aprenderá como incorporar R em um aplicativo ou a solução de BI ao encapsular o código R em procedimentos armazenados.

> [!NOTE]
> 
> A mesma solução está disponível em Python. 2017 do SQL Server é necessária. Consulte [no banco de dados analytics para desenvolvedores Python](../tutorials/sqldev-in-database-python-for-sql-developers.md)

## <a name="overview"></a>Visão geral

O processo de criação de uma solução de ponta a ponta normalmente consiste na obtenção e limpeza de dados, exploração de dados e engenharia de recursos, treinamento do modelo e ajuste e, por fim, na implantação do modelo em produção. Desenvolvimento e teste do código real é mais bem executada usando um ambiente de desenvolvimento dedicado. Para R, isso pode significar que RStudio ou [!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)].

No entanto, depois que a solução for criada, você poderá implantá-la com facilidade no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando os procedimentos armazenados do [!INCLUDE[tsql](../../includes/tsql-md.md)] no ambiente conhecido do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].

Neste tutorial, vamos supor que você tenha recebido todo o código de R necessário para a solução e foco sobre como compilar e implantar a solução usando o SQL Server.

- [Lição 1: Baixar os dados de exemplo](../tutorials/sqldev-download-the-sample-data.md)

    Baixe o conjunto de dados de exemplo e os arquivos do script SQL de exemplo em um computador local.

- [Lição 2: Importar dados para o SQL Server usando o PowerShell](../r/sqldev-import-data-to-sql-server-using-powershell.md)

    Executar um script do PowerShell que cria um banco de dados e uma tabela na instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e que carrega os dados de exemplo na tabela.

- [Lição 3: Explorar e visualizar os dados](../tutorials/sqldev-explore-and-visualize-the-data.md)

    Realize a exploração e visualização de dados básicos chamando pacotes e funções do R em procedimentos armazenados do [!INCLUDE[tsql](../../includes/tsql-md.md)] .

- [Lição 4: Criar recursos de dados usando o T-SQL](../tutorials/sqldev-create-data-features-using-t-sql.md)

    Crie novos recursos de dados usando funções personalizadas do SQL.
  
-   [Lição 5: Treinar e salvar um modelo de R usando o T-SQL](../r/sqldev-train-and-save-a-model-using-t-sql.md)

    Crie um modelo de aprendizado de máquina usando o R em procedimentos armazenados. Salve o modelo em uma tabela do SQL Server.
  
-   [Lição 6: Colocar o modelo](../tutorials/sqldev-operationalize-the-model.md)

    Depois que o modelo for salvo no banco de dados, chame o modelo de previsão no [!INCLUDE[tsql](../../includes/tsql-md.md)] usando procedimentos armazenados.

### <a name="scenario"></a>Cenário

Este tutorial usa um dataset público bem conhecido, com base em viagens em táxis cidade de Nova York. Para tornar mais rápido executar o código de exemplo, criamos uma amostra representativa de 1% dos dados. Você usará esses dados para criar um modelo de classificação binária que prevê se uma viagem específica é provável obter uma dica ou não, com base em colunas, como a hora do dia, distância e local de coleta.

### <a name="requirements"></a>Requisitos

Este tutorial destina-se a usuários que estão familiarizados com operações de banco de dados básicos, como criação de tabelas e bancos de dados, importar dados em tabelas e escrever consultas SQL. Todo o código do R é fornecido e, portanto, não é necessário nenhum ambiente de desenvolvimento do R. Pode usar um programador SQL experiente [! INCLUIR [tsql] (... /.. / inclui/md.md tsql)] em [! INCLUIR [ssManStudioFull] (... /.. / inclui / ssmanstudiofull md.md) e execute o script do PowerShell fornecido para concluir este exemplo. No entanto, antes de iniciar este tutorial, você deve concluir as seguintes preparações:

No entanto, antes de iniciar o tutorial, você deve concluir esses preparativos:

- Conecte-se a uma instância do SQL Server 2016 com R Services ou SQL Server 2017 com serviços de aprendizado de máquina e R habilitado.
- O logon que você usa para este tutorial deve ter permissões para criar bancos de dados e outros objetos, para carregar dados, selecione os dados e executar procedimentos armazenados.

> [!NOTE]
> Recomendamos que você faça **não** usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para gravar ou testar o código de R. Se o código que você inserir em um procedimento armazenado tiver problemas, as informações que são retornadas pelo procedimento armazenado serão geralmente inadequadas entender a causa do erro.
> 
> Para depuração, é recomendável que você use uma ferramenta como [!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)], ou RStudio. Os scripts do R fornecidos neste tutorial já foram desenvolvidos e depurados com ferramentas tradicionais do R.

## <a name="next-lesson"></a>Próxima lição

[Lição 1: Baixar os dados de exemplo](../tutorials/sqldev-download-the-sample-data.md)
