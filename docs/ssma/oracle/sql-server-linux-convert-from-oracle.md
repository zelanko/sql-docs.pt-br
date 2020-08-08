---
title: Migre o esquema do Oracle HR para SQL Server em Linux | Microsoft Docs
description: Converter o esquema Oracle de exemplo em SQL Server em Linux
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: ''
ms.technology: ssma
ms.openlocfilehash: 1d28458896d4ae4806db1b0f705c5e33badddfb7
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87932747"
---
# <a name="migrate-an-oracle-schema-to-sql-server-2017-on-linux-with-the-sql-server-migration-assistant"></a>Migre um esquema Oracle para SQL Server 2017 no Linux com o Assistente de Migração do SQL Server

Este tutorial usa o Assistente de Migração do SQL Server (SSMA) para Oracle no Windows para converter o esquema de **HR** de exemplo Oracle em [SQL Server 2017 no Linux](../../linux/sql-server-linux-overview.md).

> [!div class="checklist"]
> * Baixe e instale o SSMA no Windows
> * Criar um projeto do SSMA para gerenciar a migração
> * Conectar-se ao Oracle
> * Executar um relatório de migração
> * Converter o esquema de RH de exemplo
> * Migrar os dados

## <a name="prerequisites"></a>Pré-requisitos

- Uma instância do Oracle 12c (12.2.0.1.0) com o esquema de **RH** instalado
- Uma instância de trabalho do SQL Server em Linux

> [!NOTE]
> As mesmas etapas podem ser usadas para direcionar SQL Server no Windows, mas você deve selecionar Windows na configuração **migrar para** projeto.

## <a name="download-and-install-ssma-for-oracle"></a>Baixe e instale o SSMA para Oracle

Há várias edições do Assistente de Migração do SQL Server disponíveis, dependendo do banco de dados de origem.  Baixe a versão atual do [Assistente de migração do SQL Server para Oracle](https://aka.ms/ssmafororacle) e instale-a usando as instruções encontradas na página de download.

> [!NOTE]
> Neste momento, o **pacote de extensão do SSMA para Oracle** não tem suporte no Linux, mas não é necessário para este tutorial.

## <a name="create-and-set-up-project"></a>Criar e configurar o projeto

Use as seguintes etapas para criar um novo projeto do SSMA:

1. Abra o SSMA para Oracle e escolha **novo projeto** no menu **arquivo** .

1. Dê um nome ao projeto.

1. Escolha "SQL Server 2017 (Linux)-Preview" no campo **migrar para** .

O SSMA para Oracle não usa os esquemas de exemplo Oracle por padrão. Para habilitar o esquema de RH, use as seguintes etapas:

1. No SSMA, selecione o menu **ferramentas** .

1. Selecione **configurações de projeto padrão**e, em seguida, escolha **carregar objetos do sistema**.

1. Verifique se **HR** está marcado e escolha **OK**.

## <a name="connect-to-oracle"></a>Conectar-se ao Oracle

Em seguida, conecte o SSMA ao Oracle.

1. Na barra de ferramentas, clique em **conectar-se ao Oracle**.

1. Insira o nome do servidor, a porta, o SID do Oracle, o nome de usuário e a senha.

   ![Conectar-se ao Oracle](./media/sql-server-linux-convert-from-oracle/ConnectToOracle.png)

1. E clique em **Conectar**. Em alguns instantes, o SSMA para Oracle se conecta ao seu banco de dados e lê seus metadados.

## <a name="create-a-report"></a>Criar um relatório

Use as etapas a seguir para gerar um relatório de migração.

1. No **Gerenciador de metadados Oracle**, expanda o nó do servidor.

1. Expanda **esquemas**, clique com o botão direito do mouse em **HR**e selecione **criar relatório**.

   ![Criar relatório do Gerenciador de metadados Oracle](./media/sql-server-linux-convert-from-oracle/CreateReport.png)

1. Uma nova janela do navegador é aberta com um relatório que lista todos os avisos e erros associados à conversão.

   > [!NOTE]
   > Você não precisa fazer nada com essa lista para este tutorial. Se você executar essas etapas para seu próprio banco de dados Oracle, examine o relatório para resolver quaisquer problemas de conversão importantes para seu banco de dados.

   ![Relatório de migração de exemplo](./media/sql-server-linux-convert-from-oracle/SSMAReport.png)

## <a name="connect-to-sql-server"></a>Conecte-se ao SQL Server

Em seguida, escolha **conectar-se a SQL Server** e insira as informações de conexão apropriadas.  Se você usar um nome de banco de dados que ainda não existe, o SSMA para Oracle o criará para você.

![Conecte-se ao SQL Server](./media/sql-server-linux-convert-from-oracle/ConnectToSQLServer.png)

## <a name="convert-schema"></a>Converter esquema

Clique com o botão direito do mouse em **HR** no **Gerenciador de metadados Oracle**e escolha converter esquema.

![Converter esquema](./media/sql-server-linux-convert-from-oracle/ConvertSchema.png)

## <a name="synchronize-database"></a>Sincronizar banco de dados

Em seguida, Sincronize seu banco de dados.

1. Quando a conversão for concluída, use o **SQL Server Gerenciador de metadados** para ir para o banco de dados criado na etapa anterior.

1. Clique com o botão direito do mouse no banco de dados, selecione **sincronizar com Banco de dados**e clique em OK.

   ![Sincronizar com Banco de dados](./media/sql-server-linux-convert-from-oracle/SynchronizeWithDatabase.png)

## <a name="migrate-data"></a>Migrar dados

A etapa final é migrar seus dados.

1. No **Gerenciador de metadados da Oracle**, clique com o botão direito do mouse em **HR**e selecione **migrar dados**.

1. A etapa de migração de dados exige que você insira novamente suas credenciais do Oracle e do SQL Server.

1. Quando terminar, examine o relatório de migração de dados, que deve ser semelhante à captura de tela a seguir:

   ![Relatório de migração de dados](./media/sql-server-linux-convert-from-oracle/DataMigrationReport.png)

## <a name="next-steps"></a>Próximas etapas

Para um esquema Orcale mais complexo, o processo de conversão envolveria mais tempo, testes e possíveis alterações nos aplicativos cliente. A finalidade deste tutorial é mostrar como você pode usar o SSMA para Oracle como parte do processo de migração geral.

Neste tutorial, você aprendeu a:
> [!div class="checklist"]
> * Instalar o SSMA no Windows
> * Criar um novo projeto do SSMA
> * Avaliar e executar uma migração do Oracle

Em seguida, Explore outras maneiras de usar o SSMA:

> [!div class="nextstepaction"]
>[Documentação do Assistente de Migração do SQL Server](../sql-server-migration-assistant.md)
