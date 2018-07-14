---
title: Migrar do Oracle HR Schema para SQL Server no Linux | Microsoft Docs
description: Converter o esquema do Oracle de exemplo para o SQL Server no Linux
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql
ms.suite: sql
ms.custom: ''
ms.technology: ssma
ms.openlocfilehash: c80a67028d1bb0d46596287b4ff168ce994af2a0
ms.sourcegitcommit: abd71294ebc39695d403e341c4f77829cb4166a8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2018
ms.locfileid: "36927107"
---
# <a name="migrate-an-oracle-schema-to-sql-server-2017-on-linux-with-the-sql-server-migration-assistant"></a>Migrar um esquema do Oracle para o SQL Server 2017 no Linux com o SQL Server Migration Assistant

Este tutorial usa o SQL Server Migration Assistant (SSMA) para Oracle no Windows para converter o exemplo da Oracle **HR** esquema [SQL Server 2017 no Linux](../../linux/sql-server-linux-overview.md).

> [!div class="checklist"]
> * Baixar e instalar o SSMA no Windows
> * Criar um projeto do SSMA para gerenciar a migração
> * Conectar-se ao Oracle
> * Executar um relatório de migração
> * Converter o esquema de RH de exemplo
> * Migrar os dados

## <a name="prerequisites"></a>Prerequisites

- Uma instância do Oracle 12c (12.2.0.1.0) com o **HR** esquema instalada
- Uma instância de trabalho do SQL Server no Linux

> [!NOTE]
> As mesmas etapas podem ser usado para o destino do SQL Server no Windows, mas você deve selecionar o Windows nas **migrar para** configuração do projeto.

## <a name="download-and-install-ssma-for-oracle"></a>Baixar e instalar o SSMA para Oracle

Há várias edições do SQL Server Migration Assistant disponíveis, dependendo do seu banco de dados de origem.  Baixe a versão atual do [SQL Server Migration Assistant for Oracle](http://aka.ms/ssmafororacle) e instalá-lo usando as instruções encontradas na página de download.

> [!NOTE]
> Neste momento, o **SSMA para Oracle extensão Pack** não tem suporte no Linux, mas não é necessário para este tutorial.

## <a name="create-and-set-up-project"></a>Criar e configurar projeto

Use as etapas a seguir para criar um novo projeto SSMA:

1. Abra o SSMA para Oracle e escolha **novo projeto** da **arquivo** menu.

1. Nomeie o projeto.

1. Escolha "SQL Server 2017 (Linux) – versão prévia" na **migrar para** campo.

O SSMA para Oracle não usa os esquemas de exemplo do Oracle por padrão. Para habilitar o esquema de RH, use as seguintes etapas:

1. No SSMA, selecione a **ferramentas** menu.

1. Selecione **configurações de projeto padrão**e, em seguida, escolha **carregar objetos do sistema**.

1. Certifique-se **HR** está marcada e, em seguida, escolha **Okey**.

## <a name="connect-to-oracle"></a>Conectar-se ao Oracle

Em seguida, conecte o SSMA para Oracle.

1. Na barra de ferramentas, clique em **conectar-se ao Oracle**.

1. Insira o nome do servidor, a porta, a SID do Oracle, a nome de usuário e a senha.

   ![Conectar-se ao Oracle](./media/sql-server-linux-convert-from-oracle/ConnectToOracle.png)

1. Em seguida, clique em **Connect**. Em alguns instantes, o SSMA para Oracle se conecta ao seu banco de dados e lê seus metadados.

## <a name="create-a-report"></a>Criar um relatório

Use as etapas a seguir para gerar um relatório de migração.

1. No **Gerenciador de metadados do Oracle**, expanda o nó do seu servidor.

1. Expandir **esquemas**, clique com botão direito **HR**e selecione **criar relatório**.

   ![Gerenciador de metadados do Oracle criar relatório](./media/sql-server-linux-convert-from-oracle/CreateReport.png)

1. Uma nova janela do navegador é aberta com um relatório que lista todos os avisos e erros associados com a conversão.

   > [!NOTE]
   > Você não precisa fazer nada com essa lista para este tutorial. Se você executar essas etapas para seu próprio banco de dados Oracle, você deve examinar o relatório para resolver qualquer problema de conversão importantes para seu banco de dados.

   ![Relatório de migração de exemplo](./media/sql-server-linux-convert-from-oracle/SSMAReport.png)

## <a name="connect-to-sql-server"></a>Conecte-se ao SQL Server

Em seguida, escolha **conectar-se ao SQL Server** e insira as informações de conexão apropriado.  Se você usar um nome de banco de dados que ainda não existir, o SSMA para Oracle cria para você.

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

1. Quando terminar, examine o relatório de migração de dados, que deve ser semelhante à seguinte captura de tela:

   ![Relatório de migração de dados](./media/sql-server-linux-convert-from-oracle/DataMigrationReport.png)

## <a name="next-steps"></a>Próximas etapas

Para um esquema Orcale mais complexo, o processo de conversão envolveria mais tempo, teste e possíveis alterações nos aplicativos cliente. O objetivo deste tutorial é mostrar como você pode usar o SSMA para Oracle como parte do processo geral de migração.

Neste tutorial, você aprendeu como:
> [!div class="checklist"]
> * Instalar o SSMA no Windows
> * Criar um novo projeto do SSMA
> * Avaliar e executar uma migração do Oracle

Em seguida, explore outras maneiras de usar o SSMA:

> [!div class="nextstepaction"]
>[Documentação do SQL Server Migration Assistant](../sql-server-migration-assistant.md)
