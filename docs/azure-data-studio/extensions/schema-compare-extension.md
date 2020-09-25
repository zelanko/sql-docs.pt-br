---
title: Extensão de Comparação de Esquema
description: Saiba como instalar e usar a extensão de Comparação de Esquemas do Azure Data Studio para comparar facilmente dois bancos de dados e alterar seletivamente um para corresponder ao outro.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.reviewer: maghan, sstein
ms.custom: ''
ms.date: 11/04/2019
ms.openlocfilehash: 35afe56806ad1c24b1fa6ae1f03978d7f6558af4
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91123005"
---
# <a name="schema-compare-extension"></a>Extensão de Comparação de Esquema

A extensão Comparação de Esquemas oferece uma experiência fácil de usar para comparar duas definições de banco de dados e aplicar as diferenças da origem no destino.

## <a name="features"></a>Recursos

* Comparar esquemas de dois arquivos ou bancos de dados DACPAC
* Exibir resultados como um conjunto de ações que devem ser executadas em relação ao destino para corresponderem à origem
* Excluir seletivamente ações listadas em resultados
* Definir opções que controlam o escopo da comparação
* Aplicar alterações no destino ou gerar um script com o mesmo efeito
* Salvar a comparação

![Comparação de Esquemas: Exemplo de comparação](media/schema-compare-extension/schema-compare.png)

## <a name="why-would-i-use-the-schema-compare-extension"></a>Por que usar a extensão Comparação de Esquemas?

Pode ser entediante gerenciar e sincronizar manualmente diferentes versões do banco de dados. A extensão Comparação de Esquemas simplifica o processo de comparar bancos de dados e oferece controle completo ao sincronizá-los &mdash; você pode filtrar seletivamente diferenças específicas e categorias de diferenças antes de aplicar as alterações. A extensão Comparação de Esquemas é uma ferramenta confiável que faz você economizar tempo e código.

![Comparação de Esquemas: Caixa de diálogo Opções](media/schema-compare-extension/schema-compare-options.png)

## <a name="install-the-extension"></a>Instalar a Extensão

1. Selecione o ícone de Extensões para exibir as extensões disponíveis.

    ![ícone do gerenciador de extensões](media/add-extensions/extension-manager-icon.png)

2. Pesquise a extensão **Comparação de Esquemas** e selecione-a para exibir seus detalhes. Selecione **Instalar** para adicionar a extensão.

3. Após a instalação, clique em **Recarregar** para habilitar a extensão no Azure Data Studio (necessário somente ao instalar uma extensão pela primeira vez).

## <a name="launch-a-schema-compare"></a>Iniciar uma Comparação de Esquemas

1. Para abrir a caixa de diálogo Comparação de Esquemas, **clique com o botão direito do mouse** em um banco de dados no Pesquisador de Objetos e selecione **Comparação de Esquemas**. O banco de dados selecionado é definido como o Banco de dados de origem na comparação.

    ![menu de inicialização de comparação de esquemas](media/schema-compare-extension/schema-compare-launch.png)

2. Selecione uma das reticências (...) para alterar a origem e o destino de sua Comparação de Esquemas e selecione OK.

    ![origem/destino de seleção da comparação de esquemas](media/schema-compare-extension/schema-compare-select-source-target.png)

3. Para personalizar sua comparação, selecione o botão **Opções** na barra de ferramentas.

4. Selecione **Comparar** para exibir os resultados da comparação.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre a Comparação de Esquemas, visite [Usar a Comparação de Esquemas para comparar definições de banco de dados diferentes](../../ssdt/how-to-use-schema-compare-to-compare-different-database-definitions.md).
Informe problemas e solicite recursos [aqui](https://github.com/microsoft/azuredatastudio/issues).