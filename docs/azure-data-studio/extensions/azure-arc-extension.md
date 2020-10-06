---
title: Extensão do Azure Arc (versão prévia)
description: Saiba como instalar e usar a extensão do Azure Arc para experimentar os serviços de dados do Azure Arc.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.reviewer: maghan, sstein
ms.custom: ''
ms.date: 09/22/2020
ms.openlocfilehash: 3bcdd76cf143c94dc1e200a21972d00419f26b96
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725207"
---
# <a name="azure-arc-extension-for-azure-data-studio-preview"></a>Extensão do Azure Arc para Azure Data Studio (versão prévia)

A [extensão do Azure Arc (versão prévia)](/azure/azure-arc/data/) é uma extensão para criar e gerenciar recursos de serviços de dados do Azure Arc.

**As principais ações incluem:**
- Criar um recurso
    - Controlador de exibição
    - Instância Gerenciada de SQL do Azure Arc
    - PostgreSQL para o Azure Arc
- Gerenciar um recurso
    - Exibir o painel Controlador de Dados
    - Exibir a Instância Gerenciada de SQL para o painel do Azure Arc
    - Exibir o painel do PostgreSQL para o Azure Arc
- Executar o Jupyter Book do Azure Arc

## <a name="install-the-extension"></a>Instalar a extensão
- Instalar a extensão da **CLI do Azure Data** por meio da galeria.
- Instalar a extensão do **Azure Arc** por meio da galeria.
- Reiniciar o Azure Data Studio

## <a name="sign-in-with-azure-account"></a>Entre com a conta do Azure
1. Selecione Contas no canto inferior esquerdo
1. Selecione Adicionar Conta
1. Essa ação iniciará um navegador. Entre em sua Conta do Azure.

## <a name="create-a-resource"></a>Criar um recurso
Esta extensão dá suporte à implantação de controladores de dados do Azure Arc, Postgres para o Azure Arc e Instância Gerenciada de SQL para o Azure Arc. As implantações podem ser feitas por meio do assistente de Implantação interno.

1. Selecionar o viewlet de Conexões na barra de atividades esquerda
1. Selecione os três pontos e selecione **Nova Implantação**
1. Siga os prompts para criar um recurso do Azure Arc.

## <a name="manage-a-resource"></a>Gerenciar um recurso
Depois de implantar um controlador de dados do Azure Arc por meio do azdata, do portal do Azure ou do Azure Data Studio, você pode se conectar a ele por meio do Azure Data Studio.

1. Abra o viewlet de Conexões na barra de atividades esquerda.
1. Expandir **controladores do Azure Arc**
1. Selecione **Conectar controlador**
1. Preencha os parâmetros e conecte-se.

Uma vez conectado, é possível exibir os recursos implantados no controlador de dados. Em seguida, é possível clicar com o botão direito do mouse e selecionar **Gerenciar** para acessar o painel de recursos.  

Esses painéis fornecerão informações adicionais sobre o recurso, incluindo a opção de abri-lo no portal do Azure.

## <a name="next-steps"></a>Próximas etapas
Para saber mais sobre os serviços de dados do Azure Arc, [confira nossa documentação.](/azure/azure-arc/data/)