---
title: Implantar o Banco de Dados SQL do Azure via Notebook
description: Este tutorial mostra como criar um Banco de Dados SQL do Azure.
author: ninarn
ms.author: ninarn
ms.reviewer: alayu, markingmyname
ms.topic: tutorial
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.custom: ''
ms.date: 10/16/2020
ms.openlocfilehash: 5b68bda566bdd28c8dd2e70f036dd8e17643f776
ms.sourcegitcommit: 43b92518c5848489d03c68505bd9905f8686cbc0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/17/2020
ms.locfileid: "92155027"
---
# <a name="create-an-azure-sql-database-using-azure-data-studio"></a>Criar um Banco de Dados SQL do Azure usando o Azure Data Studio

Você pode criar um Banco de Dados SQL do Azure usando o Azure Data Studio por meio do assistente de implantação e de notebooks.

## <a name="pre-requisites"></a>Pré-requisitos

 - [Azure Data Studio](download-azure-data-studio.md) instalado
 - Uma conta e uma assinatura do Azure ativas. Se não tiver uma, [crie uma conta gratuita](https://azure.microsoft.com/free/).

## <a name="use-the-deployment-wizard"></a>Usar o assistente de implantação

Siga estas etapas para usar o assistente de implantação, que orientará você quanto às configurações obrigatórias em uma experiência de interface do usuário simples.

Primeiro, localize e selecione o Banco de Dados SQL do Azure no assistente de implantação.

 1. No Azure Data Studio, selecione o viewlet de Conexões na navegação do lado esquerdo.
 2. Selecione o botão **...** na parte superior do painel Conexões e escolha **Nova Implantação...**
 3. No assistente de implantação, selecione o bloco **Banco de Dados SQL do Azure** e marque a caixa de seleção de aceitação dos termos
 4. Na lista suspensa Tipo de recurso, selecione o que você gostaria de criar: um banco de dados, um servidor de banco de dados ou um pool elástico. Se você não tiver nenhum Banco de Dados SQL no Azure, comece pela criação de um.
 5. Selecione **Criar no portal do Azure** se você optar por criar um servidor ou um pool, ou clique em **Selecionar** se optar por criar um banco de dados.

Se você escolheu criar um banco de dados, siga as etapas abaixo.

 1. Entre na sua conta do Azure caso ainda não tenha feito isso. Atualize a conexão se tiver problemas nesta página do assistente.
 2. Selecione a assinatura e o servidor desejados. Em seguida, selecione **Avançar**.
 3. Insira um nome de banco de dados.
 4. Insira um nome de regra de firewall e o intervalo de IP do computador cliente local que estiver executando o Azure Data Studio. Faça isso para poder se conectar ao servidor e ao banco de dados do ADS logo após sua criação.
 5. Selecione **Avançar**.
 6. Revise os parâmetros inseridos e selecione **Script para Notebook**.

Quando o Notebook for aberto, você poderá examinar o conteúdo e o código e fazer alterações, se desejar. Em particular, é possível alterar as configurações de computação e armazenamento do padrão se você tiver preferências específicas de desempenho ou custo. No entanto, lembre-se de que todas as alterações feitas no Notebook podem causar erros de validação.

A última etapa é selecionar **Executar todos** para executar todas as células no Notebook. Quando isso for concluído, você terá um Banco de Dados SQL totalmente criado e em execução ao qual poderá se conectar e fazer consulta do ADS.

## <a name="next-steps"></a>Próximas etapas

Depois de criar seu banco de dados, servidor ou pool, você pode [conectar e consultar](quickstart-sql-database.md) o banco de dados no Azure Data Studio.
