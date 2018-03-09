---
title: Migrar o esquema do Oracle HR para o SQL Server no Linux | Microsoft Docs
description: Converter o esquema do Oracle de exemplo para o SQL Server no Linux
author: edmacauley
ms.author: edmacauley
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-oracle
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.workload: Inactive
ms.openlocfilehash: f4ab25f440db693c0fd81093f6191fc0c3390ebb
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="migrate-an-oracle-schema-to-sql-server-2017-on-linux-with-the-sql-server-migration-assistant"></a>Migrar um esquema do Oracle para 2017 do SQL Server no Linux com o SQL Server Migration Assistant

Este tutorial usa Migration Assistant SSMA (SQL Server) para Oracle no Windows para converter o exemplo Oracle **HR** esquema [2017 do SQL Server no Linux](../../linux/sql-server-linux-overview.md).

> [!div class="checklist"]
> * Baixe e instale o SSMA no Windows
> * Criar um projeto do SSMA para gerenciar a migração
> * Conectar-se ao Oracle
> * Executar um relatório de migração
> * Converter o esquema de RH de exemplo
> * migrar os dados

## <a name="prerequisites"></a>Prerequisites

- Uma instância do Oracle 12c (12.2.0.1.0) com o **HR** esquema instalada
- Uma instância de trabalho do SQL Server no Linux

> [!NOTE]
> As mesmas etapas podem ser usado para o destino do SQL Server no Windows, mas você deve selecionar o Windows o **migrar para** configuração do projeto.

## <a name="download-and-install-ssma-for-oracle"></a>Baixe e instale o SSMA para Oracle

Há várias edições do SQL Server Migration Assistant disponíveis, dependendo de seu banco de dados de origem.  Baixar a versão atual do [SQL Server Migration Assistant para Oracle](http://aka.ms/ssmafororacle) e instalá-lo usando as instruções fornecidas na página de download.

> [!NOTE]
> Neste momento, o **SSMA para o pacote de extensão do Oracle** não tem suporte no Linux, mas não é necessário para este tutorial.

## <a name="create-and-set-up-project"></a>Criar e projeto de instalação

Use as etapas a seguir para criar um novo projeto SSMA:

1. Abra o SSMA para Oracle e escolha **novo projeto** do **arquivo** menu.

1. Nomeie o projeto.

1. Escolha "SQL Server de 2017 (Linux) - Preview" no **migrar para** campo.

SSMA para Oracle não usa os esquemas de exemplo do Oracle por padrão. Para habilitar o esquema de RH, use as seguintes etapas:

1. No SSMA, selecione o **ferramentas** menu.

1. Selecione **configurações de projeto padrão**e, em seguida, escolha **carregar objetos do sistema**.

1. Certifique-se de **HR** está marcada e escolha **Okey**.

## <a name="connect-to-oracle"></a>Conectar-se ao Oracle

Em seguida conecte SSMA para Oracle.

1. Na barra de ferramentas, clique em **conectar-se ao Oracle**.

1. Insira o nome do servidor de porta, Oracle SID, nome de usuário e senha.

   ![Conectar-se ao Oracle](./media/sql-server-linux-convert-from-oracle/ConnectToOracle.png)

1. Em seguida, clique em **conectar**. Em alguns instantes, o SSMA para Oracle se conecta ao banco de dados e lê seus metadados.

## <a name="create-a-report"></a>Criar um relatório

Use as seguintes etapas para gerar um relatório de migração.

1. No **Gerenciador de metadados do Oracle**, expanda o nó do servidor.

1. Expanda **esquemas**, clique com botão direito **HR**e selecione **criar relatório**.

   ![Gerenciador de metadados do Oracle criar relatório](./media/sql-server-linux-convert-from-oracle/CreateReport.png)

1. Uma nova janela do navegador é aberta com um relatório que lista todos os avisos e erros associados com a conversão.

   > [!NOTE]
   > Você não precisa fazer nada com essa lista para este tutorial. Se você executar estas etapas para seu próprio banco de dados Oracle, você deve examinar o relatório para resolver qualquer problema de conversão importante para seu banco de dados.

   ![Relatório de migração de exemplo](./media/sql-server-linux-convert-from-oracle/SSMAReport.png)

## <a name="connect-to-sql-server"></a>Conecte-se ao SQL Server

Em seguida escolha **conectar ao SQL Server** e insira as informações de conexão apropriado.  Se você usar um nome de banco de dados que ainda não exista, SSMA para Oracle cria para você.

![Conecte-se ao SQL Server](./media/sql-server-linux-convert-from-oracle/ConnectToSQLServer.png)

## <a name="convert-schema"></a>Converter esquema

Clique duas vezes em **HR** na **Gerenciador de metadados do Oracle**e escolha Converter esquema.

![Converter esquema](./media/sql-server-linux-convert-from-oracle/ConvertSchema.png)

## <a name="synchronize-database"></a>Sincronizar o banco de dados

Em seguida, sincronize o banco de dados.

1. Depois que a conversão for concluída, use o **Gerenciador de metadados do SQL Server** para ir para o banco de dados que você criou na etapa anterior.

1. Clique com botão direito no banco de dados, selecione **sincronizar com o banco de dados**e, em seguida, clique em Okey.

   ![Sincronizar com o banco de dados](./media/sql-server-linux-convert-from-oracle/SynchronizeWithDatabase.png)

## <a name="migrate-data"></a>Migrar dados

A etapa final é migrar seus dados.

1. No **Gerenciador de metadados do Oracle**, clique duas vezes em **HR**e selecione **migrar dados**.

1. A etapa de migração de dados requer que você insira novamente suas credenciais do Oracle e SQL Server.

1. Quando terminar, examine o relatório de migração de dados, que deve ser semelhante à captura de tela a seguir:

   ![Relatório de migração de dados](./media/sql-server-linux-convert-from-oracle/DataMigrationReport.png)

## <a name="next-steps"></a>Próximas etapas

Para um esquema Orcale mais complexo, o processo de conversão envolve mais tempo, teste e possíveis alterações nos aplicativos cliente. O objetivo deste tutorial é mostrar como você pode usar o SSMA para Oracle como parte do processo de migração geral.

Neste tutorial, você aprendeu como:
> [!div class="checklist"]
> * Instalar o SSMA no Windows
> * Criar um novo projeto SSMA
> * Avaliar e executar uma migração do Oracle

Em seguida, explore outras maneiras de usar o SSMA:

> [!div class="nextstepaction"]
>[Documentação do SQL Server Migration Assistant](../sql-server-migration-assistant.md)
