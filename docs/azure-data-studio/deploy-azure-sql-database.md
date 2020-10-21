---
title: Implantar o Banco de Dados SQL do Azure via Notebook
description: Este tutorial mostra como criar um Banco de Dados SQL do Azure.
author: ninarn
ms.author: ninarn
ms.reviewer: alayu, maghan
ms.topic: tutorial
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.custom: ''
ms.date: 10/14/2020
ms.openlocfilehash: 88bb9fd980da21b20f0faf6f699147d26abe65b9
ms.sourcegitcommit: 76ab3b57718341c6057613c9bd38cf82fb17786e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92060848"
---
# <a name="create-an-azure-sql-database-using-azure-data-studio"></a>Criar um Banco de Dados SQL do Azure usando o Azure Data Studio

Você pode criar um Banco de Dados SQL do Azure usando o Azure Data Studio por meio do assistente de implantação e de notebooks.

## <a name="pre-requisites"></a>Pré-requisitos

 - [Azure Data Studio](download-azure-data-studio.md) instalado
 - Uma conta e uma assinatura do Azure ativas. Se você não tiver uma, [crie uma conta gratuita](https://azure.microsoft.com/free/).

## <a name="use-the-deployment-wizard"></a>Usar o assistente de implantação

Siga estas etapas para usar o assistente de implantação, que orientará você quanto às configurações obrigatórias em uma experiência de interface do usuário simples.

Primeiro, localize e selecione o Banco de Dados SQL do Azure no assistente de implantação.

 1. No Azure Data Studio, selecione o viewlet de Conexões na navegação do lado esquerdo.
 2. Selecione o botão **...** na parte superior do painel Conexões e escolha **Nova Implantação...**
 3. No assistente de implantação, selecione o bloco **Banco de Dados SQL do Azure** e marque a caixa de seleção de aceitação dos termos
 4. Na lista suspensa Tipo de recurso, selecione o que você gostaria de criar: um banco de dados, um servidor de banco de dados ou um pool elástico. Se você não tiver nenhum Banco de Dados SQL no Azure, comece pela criação de um banco de dados.
 5. Selecione **Criar no portal do Azure**

Em seguida, insira todas as configurações preferenciais para criar seu banco de dados, servidor ou pool. Você pode encontrar algumas diretrizes sobre como definir essas configurações na [Documentação do SQL do Azure](https://docs.microsoft.com/azure/azure-sql/database/single-database-create-quickstart?tabs=azure-portal).

## <a name="next-steps"></a>Próximas etapas

Depois de criar seu banco de dados, servidor ou pool, você pode [conectar e consultar](quickstart-sql-database.md) o banco de dados no Azure Data Studio.
