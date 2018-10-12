---
title: Virtualizar dados externos no SQL Server 2019 CTP 2.0 | Microsoft Docs
description: ''
author: Abiola
ms.author: aboke
manager: craigg
ms.date: 09/24/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: polybase
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: dfd4460c51e4aeef8e9faff8479e7edf2678c35f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47627314"
---
# <a name="use-the-data-external-table-wizard-with-external-tables"></a>Usar o Assistente de tabela externa de dados com tabelas externas

Um dos principais cenários para o SQL Server 2019 CTP 2.0 é a capacidade de virtualizar os dados.  Esse processo permite que os dados permaneçam em seu local original, no entanto, é possível **virtualizar** os dados em uma instância do SQL Server para que ela possa ser consultada lá como qualquer outra tabela no SQL Server. Isso minimizará a necessidade de processos de ETL. Isso é possível com o uso de conectores do Polybase. Para obter mais informações sobre a Virtualização de dados, consulte nosso documento de [Introdução ao PolyBase](polybase-guide.md).

## <a name="launch-the-external-table-wizard"></a>Inicializar o Assistente de tabela externa

Conecte-se à instância mestre usando o endereço IP / número da porta (31433) obtidos no final do script de implantação. Expanda seu nó **Bancos de Dados** no Pesquisador de Objetos. Em seguida, selecione um dos bancos de dados em que você deseja virtualizar os dados de/para uma instância do SQL Server existente. Clique com botão direito do mouse no Banco de dados e selecione **Criar tabela externa** no menu de contexto. Isso inicia o Assistente de virtualização de dados. Você também pode iniciar o Assistente de virtualização de dados na paleta de comandos pressionando Ctrl+Shift+P (no Windows) e Cmd+Shift+P (no Mac).

![Assistente de virtualização de dados](media/data-virtualization/virtualize-data-wizard.png)
## <a name="select-a-data-source"></a>Selecionar uma fonte de dados

se você tiver iniciado o assistente de um dos banco de dados, poderá ver que o menu suspenso de destino é preenchido automaticamente. Você também tem a opção de inserir ou alterar o Banco de dados de destino nessa tela. Os Tipos de fonte de dados externa compatíveis com o assistente são SQL Server e Oracle.

> [!NOTE]
>O SQL Server é realçado por padrão


![Selecionar uma fonte de dados](media/data-virtualization/select-data-source.png)

Clique em Avançar para prosseguir para a próxima etapa do assistente que define a Chave mestra de banco de dados.

## <a name="create-database-master-key"></a>Criar chave mestra de banco de dados

Nesta etapa, será solicitado que você crie uma chave mestra de banco de dados. É obrigatório criar a chave mestra, pois isso protege as credenciais usadas por uma Fonte de dados externa. Escolha uma senha forte para a chave mestra. Faça também o backup da chave mestra usando BACKUP MASTER KEY e armazene-o em um local externo seguro.

![Criar uma chave mestra de banco de dados](media/data-virtualization/virtualize-data-master-key.png)

> [!IMPORTANT]
> Se você já tiver uma chave mestra de banco de dados, os campos de entrada serão restringidos e você poderá ignorar esta etapa. Basta clicar em “Avançar” para prosseguir para a próxima página do assistente.

> [!NOTE]
> Se você não escolher uma senha forte, o assistente irá fazer isso na última etapa. Esse é um problema conhecido que será corrigido na versão futura, para que seja mais intuitivo.

## <a name="enter-the-external-data-source-credentials"></a>Digite as credenciais de fonte de dados externa

Nesta etapa, insira sua fonte de dados externa e os detalhes de credenciais. Esta etapa cria um objeto de fonte de dados externa e, em seguida, usa as credenciais para o objeto de banco de dados para se conectar à fonte de dados. Forneça um nome para a Fonte de dados externa (exemplo: Teste) e forneça os detalhes da Conexão do SQL Server da fonte de dados externa – o Nome do servidor e o nome do Banco de dados nos quais você deseja que a fonte de dados externa seja criada nesse servidor.

A próxima etapa será Configurar a credencial, portanto, forneça um Nome de credencial, que é o nome da Credencial no escopo do banco de dados usada para armazenar com segurança as informações de entrada para a Fonte de dados externa que você está criando (exemplo: TestCred) e forneça o nome de usuário e a senha para se conectar à fonte de dados.

![Credenciais de fonte de dados externa](media/data-virtualization/data-source-credentials.png)

## <a name="external-data-table-mapping"></a>Mapeamento da tabela de dados externos

Na próxima janela, você poderá selecionar as tabelas das quais você deseja criar exibições externas. Selecionar os Bancos de dados pai incluirá também todas as tabelas filho. Quando as tabelas são selecionadas, uma tabela de mapeamento pode ser vista no lado direito. Aqui, você pode fazer alterações do “tipo” ou alterar o nome da própria tabela externa selecionada.

![Credenciais de fonte de dados externa](media/data-virtualization/data-table-mapping.png)

> [!NOTE]
>Clicar duas vezes em outra tabela selecionada alterará a exibição de mapeamento.

> [!IMPORTANT]
>O tipo foto ainda não é compatível com a ferramenta de Tabela externa. Criar uma exibição externa com um tipo foto nela gerará um erro após a criação da tabela. No entanto, a tabela ainda será criada.

## <a name="summary"></a>Resumo

Essa etapa fornece um resumo das suas seleções. Ela fornece o nome da Credencial com escopo de banco de dados e os objetos da Fonte de dados externa que serão criados no banco de dados de destino. Nesta etapa, você tem a opção de **“Gerar Script”** que gerará script em T-SQL a sintaxe para criar a fonte de dados externa ou **Criar** que criará o objeto da Fonte de dados externa.

![Tela de resumo](media/data-virtualization/virtualize-data-summary.png)

Se você clicar em “Criar”, poderá ver o objeto de Fonte de dados externa criado no Banco de dados de destino.

![Fontes de dados externas](media/data-virtualization/external-data-sources.png)

Se você clicar em **Gerar Script**, verá a consulta T-SQL que está sendo gerada para criar o objeto de Fonte de dados externa.

![Gerar script](media/data-virtualization/generated-script.png)

> [!NOTE]
> Gerar Script estará visível somente na última página do assistente. Atualmente, essa opção é mostrada em todas as páginas.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o Cluster de Big Data do SQL Server e cenários relacionados, consulte [O que é o Cluster de Big Data do SQL Server?](../../big-data-cluster/big-data-cluster-overview.md).
