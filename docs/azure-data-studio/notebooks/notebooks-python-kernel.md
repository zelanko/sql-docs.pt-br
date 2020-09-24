---
title: Notebooks com o kernel do Python no Azure Data Studio
description: Este tutorial mostra como criar e executar um notebook do Python.
ms.topic: tutorial
ms.prod: azure-data-studio
ms.technology: azure-data-studio
author: garyericson
ms.author: garye
ms.reviewer: mikeray, alayu, maghan
ms.custom: ''
ms.date: 07/01/2020
ms.openlocfilehash: 38223789b149f0302005c39a42fdd18eb73ec2f6
ms.sourcegitcommit: e3460309b301a77d0babec032f53de330da001a9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91136554"
---
# <a name="create-and-run-a-python-notebook"></a>Criar e executar um notebook do Python

[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

Este tutorial demonstra como criar e executar um notebook no Azure Data Studio usando o kernel do Python.

## <a name="prerequisites"></a>Pré-requisitos

- [Azure Data Studio instalado](../download-azure-data-studio.md)

## <a name="create-a-notebook"></a>Criar um notebook

As seguintes etapas mostram como criar um arquivo de notebook no Azure Data Studio:

1. Abra o Azure Data Studio. Se for solicitado que você se conecte a um SQL Server, você poderá se conectar ou clicar em **Cancelar**.

1. Selecione **Novo Notebook** no menu **Arquivo**.

1. Selecione **Python 3** para o **Kernel**. **Anexar a** é definido como "localhost".

   :::image type="content" source="media/notebooks-python-kernel/set-kernel-and-attach-to-python.png" alt-text="Definir o Kernel":::

Você pode salvar o notebook usando o comando **Salvar** ou **Salvar como...** no menu **Arquivo**.

Para abrir um notebook, você pode usar o comando **Abrir arquivo...** no menu **Arquivo**, selecionar **Abrir arquivo** na página **Inicial** ou usar o comando **Arquivo: abrir** da paleta de comandos.

## <a name="change-the-python-kernel"></a>Alterar o kernel do Python

Na primeira vez em que você se conecta ao kernel do Python em um notebook, a página **Configurar Python para Notebooks** é exibida. Você pode selecionar:

- **Nova instalação do Python** para instalar uma nova cópia do Python para o Azure Data Studio, ou
- **Usar a instalação existente do Python** para especificar o caminho para uma instalação existente do Python para uso do Azure Data Studio

Para exibir o local e a versão do kernel ativo do Python, crie uma célula de código e execute os seguintes comandos do Python:

```python
import os
import sys
print(sys.version_info)
print(os.path.dirname(sys.executable))
```

Para se conectar a uma instalação diferente do Python:

1. No menu **Arquivo**, selecione **Preferências** e **Configurações**.
1. Role até **Configuração do Notebook** em **Extensões**.
1. Em **Usar Python Existente**, desmarque a opção "Caminho local para uma instalação do Python preexistente usada por Notebooks".
1. Reinicie o Azure Data Studio.

Quando o Azure Data Studio é iniciado e você se conecta ao kernel do Python, a página **Configurar Python para Notebooks** é exibida e você pode optar por criar uma instalação do Python ou especificar um caminho para uma instalação existente.

## <a name="run-a-code-cell"></a>Executar uma célula de código

Você pode criar células contendo código SQL que pode ser executado no local clicando no botão **Executar célula** (a seta preta redonda) à esquerda da célula. Os resultados são mostrados no notebook após a conclusão da execução da célula.

Por exemplo:

1. Adicione uma nova célula de código Python selecionando o comando **+Código** na barra de ferramentas.

   :::image type="content" source="media/notebooks-python-kernel/notebook-toolbar-python.png" alt-text="Barra de ferramentas do notebook":::

1. Copie e cole o exemplo a seguir na célula e clique em **Executar célula**. Este exemplo executa cálculos matemáticos simples e o resultado é exibido abaixo.

   ```python
   a = 1
   b = 2
   c = a/b
   print(c)
   ```

   :::image type="content" source="media/notebooks-python-kernel/run-notebook-cell-python.png" alt-text="Executar célula do notebook":::

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre os notebooks:

- [Estender o Python com Kqlmagic](./notebooks-kqlmagic.md)
- [Como usar notebooks no Azure Data Studio](./notebooks-guidance.md)
- [Criar e executar um notebook do SQL Server](./notebooks-sql-kernel.md)
