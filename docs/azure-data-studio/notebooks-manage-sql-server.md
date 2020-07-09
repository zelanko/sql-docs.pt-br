---
title: Como gerenciar um notebook
description: Aprenda a gerenciar notebooks no Azure Data Studio. Isso inclui abrir notebooks, salvá-los e alterar sua conexão SQL ou do kernel de Python.
author: markingmyname
ms.author: maghan
ms.reviewer: achatter, alayu, mikeray
ms.metadata: seo-lt-2019
ms.topic: conceptual
ms.prod: azure-data-studio
ms.technology: ''
ms.custom: ''
ms.date: 04/27/2020
ms.openlocfilehash: 326e0b0afc4809d13cf2fdfdbd76f53dafe1cbb9
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85774586"
---
# <a name="how-to-manage-notebooks-in-azure-data-studio"></a>Como gerenciar notebooks no Azure Data Studio

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Este artigo mostra como abrir e salvar arquivos de notebook no Azure Data Studio. Ele também demonstra como alterar sua conexão com o SQL Server ou o kernel de Python.

## <a name="open-a-notebook"></a>Abrir um notebook

Há várias maneiras de abrir a caixa de diálogo **Abrir Notebook**. Você pode usar o menu Arquivo, o Painel e a Paleta de Comandos. As seções a seguir descrevem cada método.

### <a name="file-menu"></a>Menu Arquivo

Selecione **Abrir Arquivo** no menu Arquivo CTRL+O (no Windows) e Cmd+O (no Mac).

![Abra a caixa de diálogo Abrir Arquivo selecionando Abrir Arquivo](./media/notebooks-manage-sql-server/open-file-1.png)

### <a name="dashboard"></a>Painel

Clique em **Abrir Notebook** no painel para abrir a caixa de diálogo Abrir Arquivo.

![Abrir a caixa de diálogo Abrir Arquivo selecionando Abrir Notebook no painel](./media/notebooks-manage-sql-server/open-file-2.png) 

### <a name="command-palette"></a>Paleta de Comandos

Use o comando **Arquivo: Abrir** da paleta de comandos digitando Ctrl+Shift+P (no Windows) e Cmd+Shift+P (no Mac).

![Abra a caixa de diálogo Abrir Arquivo inserindo Arquivo: Abrir na paleta de comandos](./media/notebooks-manage-sql-server/open-file-3.png)

## <a name="save-a-notebook"></a>Salvar um notebook

Atualmente, há uma forma de salvar um notebook. Selecione **Salvar** na barra de ferramentas do notebook.

![Salve o arquivo selecionando Salvar na barra de ferramentas do notebook](./media/notebooks-manage-sql-server/save-file-1.png)

> [!NOTE]
> Os métodos a seguir atualmente não salvam alterações em notebooks:
>
> - Os comandos **Salvar Arquivo**, **Salvar Arquivo como...** e **Salvar Tudo** do menu Arquivo.
> - Os comandos **Arquivo: Salvar** inseridos na paleta de comandos.

## <a name="change-the-sql-connection"></a>Alterar a conexão SQL

Para alterar a conexão SQL de um notebook:

1. Selecione o menu **Anexar a** na barra de ferramentas do notebook e, em seguida, **Alterar Conexão**.

   ![Clique no menu Anexar a na barra de ferramentas do notebook](./media/notebooks-manage-sql-server/select-attach-to-1.png)

2. Agora você pode selecionar um servidor de conexão recente ou inserir novos detalhes de conexão para se conectar.

   ![Selecione um servidor no menu Anexar a](./media/notebooks-manage-sql-server/select-attach-to-2.png)

## <a name="change-the-python-kernel"></a>Alterar o kernel do Python

Na primeira vez que você abre o Azure Data Studio, a página **Configurar Python para Notebooks** é exibida. Você pode selecionar:

- **Nova instalação do Python** para instalar uma nova cópia do Python para o Azure Data Studio, ou
- **Usar a instalação existente do Python** para especificar o caminho para uma instalação existente do Python para uso do Azure Data Studio

Para exibir o local e a versão do kernel ativo do Python, crie uma célula de código e execute os seguintes comandos do Python:

```python
import os
import sys
print(sys.version_info)
print(os.path.dirname(sys.executable))
```

Para alterar para uma instalação diferente do Python:

1. No menu **Arquivo**, selecione **Preferências** e **Configurações**.
1. Role até **Configuração do Notebook** em **Extensões**.
1. Em **Usar Python Existente**, desmarque a opção "Caminho local para uma instalação do Python preexistente usada por Notebooks".
1. Reinicie o Azure Data Studio.

Quando a página **Configurar Python para Notebooks** é exibida, você pode optar por criar uma instalação do Python ou especificar um caminho para uma instalação existente.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre notebooks SQL no Azure Data Studio, confira [Como usar notebooks no SQL Server 2019](notebooks-guidance.md).
