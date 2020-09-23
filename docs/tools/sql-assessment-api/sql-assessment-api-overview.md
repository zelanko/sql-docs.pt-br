---
title: API de Avaliação do SQL Server
description: Saiba mais sobre a API de Avaliação do SQL que fornece um mecanismo para avaliar a configuração do SQL Server e obter as melhores práticas.
ms.prod: sql
ms.technology: tools-other
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: ''
ms.date: 11/04/2019
ms.openlocfilehash: a778fd92a44a229ae6806cef31a10b728f241865
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87987581"
---
# <a name="sql-assessment-api"></a>API de Avaliação do SQL

A API de Avaliação do SQL fornece um mecanismo para avaliar a configuração do SQL Server para obter as melhores práticas. A API é fornecida com um RuleSet que contém regras de melhores práticas sugeridas pela equipe do SQL Server. Esse conjunto de regras é aprimorado com o lançamento de novas versões. Porém, ao mesmo tempo, a API foi criada com a intenção de fornecer uma solução altamente personalizável e extensível. Portanto, os usuários podem ajustar as regras padrão e criar suas próprias.

A API de Avaliação do SQL é útil quando você deseja ter certeza de que a configuração do SQL Server está alinhada com as melhores práticas. Após uma avaliação inicial, é possível acompanhar a estabilidade da configuração realizando avaliações agendadas regularmente.

A API pode ser usada para avaliar a Instância Gerenciada de SQL do Azure e o SQL Server versões 2012 e posteriores. Há suporte para SQL no Linux.

## <a name="rules"></a>Regras

As regras, às vezes chamadas de verificações, são definidas em arquivos JSON formatados. O formato do conjunto de regras exige que o nome e a versão do conjunto de regras sejam especificados. Portanto, ao usar conjuntos de regras personalizados, você pode facilmente saber quais recomendações vêm de qual conjunto de regras.

O conjunto de regras enviado pela Microsoft está disponível no GitHub. Você pode acessar o [repositório de exemplos](https://aka.ms/sql-assessment-api) para obter mais detalhes.

## <a name="sql-assessment-cmdlets-and-smo-extension"></a>Cmdlets de Avaliação do SQL e extensão de SMO

A API de Avaliação do SQL faz parte do [SMO (SQL Server Management Objects)](../../relational-databases/server-management-objects-smo/installing-smo.md), versão de lançamento de julho de 2019 e superiores, bem como do módulo [SQL Server PowerShell](../../powershell/download-sql-server-ps-module.md), versão de lançamento de julho 2019 e superiores.

* [Instalar o SMO](../../relational-databases/server-management-objects-smo/installing-smo.md)

* [Instalar o módulo do SQL Server PowerShell](../../powershell/download-sql-server-ps-module.md)

O módulo SqlServer está obtendo dois novos cmdlets para trabalhar com a API de Avaliação do SQL:

* **Get-SqlAssessmentItem** – fornece uma lista de verificações de avaliação disponíveis para um objeto SQL Server

* **Invoke-SqlAssessment** – fornece resultados de uma avaliação

A estrutura do SMO é complementada pela API de Avaliação do SQL que fornece os seguintes métodos:

* **GetAssessmentItems** – retorna verificações disponíveis para um objeto SQL específico (IEnumerable<... >)

* **GetAssessmentResults** – avalia de forma síncrona a avaliação e retorna resultados e erros se houver um (IEnumerable<... >)

* **GetAssessmentResultsList** – avalia de forma assíncrona a avaliação e retorna resultados e erros se houver um (Task<... >)

## <a name="get-started-using-sql-assessment-cmdlets"></a>Introdução ao uso de cmdlets de Avaliação do SQL

Uma avaliação é realizada em relação a um objeto do SQL Server escolhido. No conjunto de regras padrão, há verificações apenas de dois tipos de objetos: Servidor e banco de dados (além deles, a API dá suporte a dois outros tipos: Grupo de arquivos e Grupo de disponibilidade). Se você quiser avaliar uma instância do SQL e todos os seus bancos de dados, execute os cmdlets de Avaliação do SQL para cada objeto separadamente. Outra opção é passar os objetos para avaliação para os cmdlets de Avaliação do SQL em uma variável ou no pipeline.

Os objetos SqlServer e RegisteredServer são intercambiáveis, portanto, você pode passar qualquer um para os cmdlets de Avaliação do SQL.

Siga os exemplos abaixo para começar.

1. Obtenha uma lista de verificações disponíveis para uma instância padrão local para familiarizar-se com as verificações. Neste exemplo, estamos canalizando a saída do cmdlet Get-SqlInstance para o cmdlet Get-SqlAssessmentItem para passar o objeto de instância para ele.

    ```powershell
    Get-SqlInstance -ServerInstance 'localhost' | Get-SqlAssessmentItem
    ```

2. Obtenha uma lista das verificações disponíveis para todos os bancos de dados da instância. Aqui, estamos usando o cmdlet Get-Item e um caminho implementado com o provedor do SQL Server do Windows PowerShell para obter uma lista dos bancos de dados e, em seguida, direcioná-la para o cmdlet Get-SqlDatabase.

    ```powershell
    Get-Item SQLSERVER:\SQL\localhost\default | Get-SqlAssessmentItem
    ```

    Além disso, você pode usar o cmdlet Get-SqlDatabase para fazer o mesmo.

    ```powershell
    Get-SqlDatabase -ServerInstance 'localhost' | Get-SqlAssessmentItem
    ```

3. Obtenha uma lista das verificações disponíveis para todos os bancos de dados da instância. Aqui, estamos usando o cmdlet Get-Item e um caminho implementado com o provedor do SQL Server do Windows PowerShell para obter uma lista dos bancos de dados e, em seguida, direcioná-la para o cmdlet Get-SqlDatabase.

    ```powershell
    Get-Item SQLSERVER:\SQL\localhost\default | Get-SqlAssessmentItem
    ```

    Além disso, você pode usar o cmdlet Get-SqlDatabase para fazer o mesmo.

    ```powershell
    Get-SqlDatabase -ServerInstance 'localhost' | Get-SqlAssessmentItem
    ```

4. Invoque a avaliação para a instância e salve os resultados em uma tabela do SQL. Neste exemplo, estamos canalizando a saída do cmdlet Get-SqlInstance para o cmdlet Invoke-SqlAssessment, cujos resultados são canalizados para o cmdlet Write-SqlTableData. O cmdlet Invoke-Assessment é executado com o parâmetro `-FlattenOutput` neste exemplo. Esse parâmetro torna a saída adequada para o cmdlet Write-SqlTableData. O último gerará um erro se você omitir o parâmetro.

    ```powershell
    Get-SqlInstance -ServerInstance 'localhost' |
    Invoke-SqlAssessment -FlattenOutput |
    Write-SqlTableData -ServerInstance 'localhost' -DatabaseName SQLAssessmentDemo -SchemaName Assessment -TableName Results -Force
    ```

    Agora, vamos invocar uma avaliação para todos os bancos de dados da instância e adicionar os resultados à mesma tabela.

    ```powershell
    Get-SqlDatabase -ServerInstance 'localhost' |
    Invoke-SqlAssessment -FlattenOutput |
    Write-SqlTableData -ServerInstance 'localhost' -DatabaseName SQLAssessmentDemo -SchemaName Assessment -TableName Results -Force
    ```

5. Siga as descrições e os links na tabela para entender ainda mais as recomendações.

6. Personalize as regras com base em seu ambiente e nos requisitos organizacionais (veja abaixo).

7. Agende uma tarefa ou um trabalho para executar a avaliação regularmente ou sob demanda para medir o progresso.

## <a name="customizing-rules"></a>Como personalizar as regras

As regras são projetadas para serem personalizáveis e extensíveis. O conjunto de regras da Microsoft foi projetado para funcionar na maioria dos ambientes. No entanto, é impossível ter um conjunto de regras que funcione para cada ambiente único. Os usuários podem gravar os próprios arquivos JSON e personalizar as regras existentes ou adicionar novas. Exemplos de personalização e do conjunto de regras completo do Microsoft liberado estão disponíveis no [repositório de exemplos](https://aka.ms/sql-assessment-api). Para obter mais detalhes sobre como executar os cmdlets de Avaliação do SQL com arquivos JSON personalizados, use o cmdlet Get-Help.

### <a name="options-available-with-rule-customization-feature"></a>Opções disponíveis com o recurso de personalização de regra

#### <a name="enablingdisabling-certain-rules-or-groups-of-rules-using-tags"></a>Como habilitar/desabilitar determinadas regras ou grupos de regras (usando marcas)

Você pode silenciar regras específicas quando elas não são aplicadas a seu ambiente ou até que o trabalho agendado seja feito para corrigir o problema.

#### <a name="changing-threshold-parameters"></a>Como alterar parâmetros de limite

Regras específicas têm limites que são comparados ao valor atual de uma métrica para descobrir um problema. Se os limites padrão não forem adequados, você poderá alterá-los.

#### <a name="adding-more-rules-written-by-you-or-third-parties"></a>Como adicionar mais regras escritas por você ou por terceiros

Você pode reunir conjuntos de regras adicionando um ou mais arquivos JSON como parâmetros à sua chamada à API de Avaliação do SQL. Sua organização pode gravar esses arquivos ou obtê-los de terceiros. Por exemplo, você pode ter o arquivo JSON que desabilita regras específicas do conjunto de regras da Microsoft e outro arquivo JSON por um especialista do setor que inclui regras que você considera úteis para o seu ambiente, seguido por outro arquivo JSON que altera alguns valores limites em tal arquivo JSON.

> [!IMPORTANT]  
> Recomendamos não usar RuleSets provenientes de fontes não confiáveis até examiná-los detalhadamente para garantir que sejam seguros.

## <a name="next-steps"></a>Próximas etapas

* [SQL Server Management Objects (SMO)](../../relational-databases/server-management-objects-smo/overview-smo.md)
* [PowerShell](../../powershell/download-sql-server-ps-module.md).
