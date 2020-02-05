---
title: Virtualizar dados externos
description: Esta página fornece detalhes sobre as etapas para usar o assistente Criar tabela externa para Fontes de dados relacionais
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
ms.date: 12/13/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: polybase
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.metadata: seo-lt-2019
ms.openlocfilehash: f4bd7eec24be747fe6c0933d31467410bfecf2a9
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75227510"
---
# <a name="use-the-external-table-wizard-with-relational-data-sources"></a>Usar o Assistente de Tabela Externa com fontes de dados relacionais

Um dos principais cenários para o SQL Server 2019 é a capacidade de virtualizar os dados. Esse processo permite que os dados se mantenham em sua localização original. É possível *virtualizar* os dados em uma instância do SQL Server para que ela possa ser consultada lá como qualquer outra tabela no SQL Server. Esse processo minimiza a necessidade de processos de ETL. Esse processo é possível com o uso de conectores do PolyBase. Para obter mais informações sobre virtualização de dados, confira [Introdução ao PolyBase](polybase-guide.md).

Este vídeo apresenta uma introdução à virtualização de dados:

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-Data-Virtualization/player?WT.mc_id=dataexposed-c9-niner]


## <a name="start-the-external-table-wizard"></a>Inicializar o assistente de Tabela Externa

Conecte-se à instância mestra usando o endereço IP/número da porta do ponto de extremidade **sql-server-master** obtido por meio do comando [**azdata cluster endpoints list**](../../big-data-cluster/deployment-guidance.md#endpoints). Expanda seu nó **Bancos de Dados** no Pesquisador de Objetos. Em seguida, selecione um dos bancos de dados no qual deseja virtualizar os dados de uma instância do SQL Server existente. Clique com o botão direito do mouse no banco de dados e selecione **Criar Tabela Externa** para iniciar o assistente de Virtualização de Dados. Você também pode iniciar o assistente de Virtualização de Dados na paleta de comandos. Use Ctrl + Shift + P no Windows ou use Cmd + Shift + P em um Mac.

![Assistente de Virtualização de Dados](media/data-virtualization/virtualize-data-wizard.png)
## <a name="select-a-data-source"></a>Selecionar uma fonte de dados

Se você tiver iniciado o assistente de um dos bancos de dados, a caixa suspensa de destino será preenchida automaticamente. Você também tem a opção de inserir ou alterar o banco de dados de destino nessa página. Os tipos de fonte de dados externa compatíveis com o assistente são SQL Server e Oracle.

> [!NOTE]
>O SQL Server é realçado por padrão.


![Selecionar uma fonte de dados](media/data-virtualization/select-data-source.png)

Selecione **Avançar** para continuar.

## <a name="create-a-database-master-key"></a>Criar uma chave mestra de banco de dados

Nesta etapa, você criará uma chave mestra de banco de dados. É necessário criar uma chave mestra. Uma chave mestra protege as credenciais usadas por uma fonte de dados externa. Escolha uma senha forte para a chave mestra. Além disso, faça o backup da chave mestra usando **BACKUP MASTER KEY**. Armazene o backup em uma localização externa segura.

![Criar uma chave mestra de banco de dados](media/data-virtualization/virtualize-data-master-key.png)

> [!IMPORTANT]
> Se você já tiver uma chave mestra de banco de dados, esta etapa será automaticamente ignorada.

## <a name="enter-external-data-source-credentials"></a>Insira as credenciais da fonte de dados externa

Nesta etapa, insira sua fonte de dados externa e os detalhes de credenciais para criar um objeto da fonte de dados externa. As credenciais são usadas pelo objeto de banco de dados para se conectar à fonte de dados. Digite um nome para a fonte de dados externa. Um exemplo é o Test. Forneça detalhes de conexão do SQL Server da fonte de dados externa. Insira o **Nome do servidor** e o **Nome do banco de dados** em que deseja que sua fonte de dados seja criada.

A próxima etapa é configurar uma credencial. Insira um nome para a credencial. Esse nome é a credencial no escopo do banco de dados, usada para armazenar com segurança as informações de entrada para a fonte de dados externa que você criou. Um exemplo é o TestCred. Insira um nome de usuário e senha para se conectar à fonte de dados.

![Credenciais de fonte de dados externa](media/data-virtualization/data-source-credentials.png)

## <a name="external-data-table-mapping"></a>Mapeamento da tabela de dados externos

Na próxima página, selecione as tabelas para criar modos de exibição externos. Ao selecionar os bancos de dados pai, as tabelas filho também são incluídas. Depois de selecionar tabelas, uma tabela de mapeamento será exibida à direita. Aqui, você poderá fazer alterações nos tipos. Você também poderá alterar o nome da tabela externa selecionada.

![Credenciais de fonte de dados externa](media/data-virtualization/data-table-mapping.png)

> [!NOTE]
>Para alterar o modo de exibição de mapeamento, clique duas vezes em outra tabela selecionada.

> [!IMPORTANT]
>O tipo foto não é compatível com a ferramenta de Tabela Externa. Caso crie um modo de exibição externo com um tipo de foto nele, um erro será exibido depois que a tabela for criada. Contudo, a tabela ainda será criada.

## <a name="summary"></a>Resumo

Essa etapa exibe um resumo das suas seleções. Ela fornece o nome da credencial com escopo de banco de dados e os objetos da fonte de dados externa criados no banco de dados de destino. Selecione **Gerar script** para gerar o script, no T-SQL, da sintaxe usada para criar a fonte de dados externa. Selecione **Criar** para criar o objeto da fonte de dados externa.

![Tela de resumo](media/data-virtualization/virtualize-data-summary.png)

Caso clique em **Criar**, você verá o objeto da fonte de dados externa criado no banco de dados de destino.

![Fontes de dados externas](media/data-virtualization/external-data-sources.png)

Caso clique em **Gerar Script**, verá a consulta T-SQL que está sendo gerada para criar o objeto da fonte de dados externa.

![Gerar script](media/data-virtualization/generated-script.png)

> [!NOTE]
> **Gerar script** estará visível somente na última página do assistente. Atualmente, essa opção é exibida em todas as páginas.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre os clusters de Big Data do SQL Server e os cenários relacionados, confira [O que são clusters de Big Data do SQL Server?](../../big-data-cluster/big-data-cluster-overview.md).
