---
title: Notebooks com o kernel do Python no Azure Data Studio
description: Este tutorial mostra como criar e executar um notebook do Python.
author: garyericson
ms.author: garye
ms.reviewer: mikeray, alayu, maghan
ms.topic: tutorial
ms.prod: azure-data-studio
ms.technology: ''
ms.custom: ''
ms.date: 04/27/2020
ms.openlocfilehash: e4c431cba395b8e0c732fa7ac4ab96942cac7144
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85728857"
---
# <a name="create-and-run-a-python-notebook"></a>Criar e executar um notebook do Python

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Este tutorial demonstra como criar e executar um notebook no Azure Data Studio usando o kernel do Python.

## <a name="prerequisites"></a>Pré-requisitos

- [Azure Data Studio instalado](download-azure-data-studio.md)

## <a name="new-notebook"></a>Novo notebook

As seguintes etapas mostram como criar um arquivo de notebook no Azure Data Studio:

1. Abra o Azure Data Studio. Se for solicitado que você se conecte a um SQL Server, você poderá se conectar ou clicar em **Cancelar**.

1. Selecione **Novo Notebook** no menu **Arquivo**.

1. Selecione **Python 3** para o **Kernel**.

   :::image type="content" source="media/notebook-tutorial-python/set-kernel-and-attach-to-python.png" alt-text="Definir o Kernel":::

1. Se for solicitado que você configure o Python, em **Configurar Python para Notebooks**, selecione:

   - **Nova instalação do Python** para instalar uma nova cópia do Python para o Azure Data Studio, ou
   - **Usar a instalação existente do Python** para especificar o caminho para uma instalação existente do Python

## <a name="run-a-notebook-cell"></a>Executar uma célula do notebook

Você pode criar células contendo código ou texto. Você pode executar uma célula de código e os resultados são mostrados no notebook após a conclusão da execução da célula. As células de texto permitem que você intercale a documentação formatada com o código.

### <a name="code"></a>Código

Adicione uma nova célula de código Python selecionando o comando **+Código** na barra de ferramentas.

:::image type="content" source="media/notebook-tutorial-python/notebook-toolbar-python.png" alt-text="Barra de ferramentas do notebook":::

Este exemplo faz cálculos matemáticos simples.

```python
a = 1
b = 2
c = a/b
print(c)
```
Execute a célula clicando no botão reproduzir à esquerda da célula. Os resultados aparecem abaixo.

:::image type="content" source="media/notebook-tutorial-python/run-notebook-cell-python.png" alt-text="Executar célula do notebook":::

### <a name="text"></a>Texto

Adicione uma nova célula de texto selecionando o comando **+Text** na barra de ferramentas.

:::image type="content" source="media/notebook-tutorial-python/notebook-toolbar-python-text.png" alt-text="Barra de ferramentas do notebook":::

A célula muda para o modo de edição e você pode digitar o markdown e ver a versão prévia ao mesmo tempo.

:::image type="content" source="media/notebook-tutorial-python/notebook-markdown-cell-python.png" alt-text="Célula de markdown":::

A seleção fora da célula de texto mostra apenas o texto markdown.

:::image type="content" source="media/notebook-tutorial-python/notebook-markdown-preview-python.png" alt-text="Texto de markdown":::

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre os notebooks:

- [Como usar notebooks com o SQL Server](notebooks-guidance.md)

- [Criar e executar um notebook do SQL Server](notebooks-tutorial-sql-kernel.md)

- [Como gerenciar notebooks no Azure Data Studio](notebooks-manage-sql-server.md)
