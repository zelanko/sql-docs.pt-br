---
title: SqlPackage em pipelines de desenvolvimento
description: Saiba como solucionar problemas de pipelines de desenvolvimento de banco de dados com SqlPackage.exe verificando o número de build instalado.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 198198e2-7cf4-4a21-bda4-51b36cb4284b
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan; sstein
ms.date: 11/4/2020
ms.openlocfilehash: 002d145328ca101fee467428e5b7c8b0ff1fdd95
ms.sourcegitcommit: 866554663ca3191748b6e4eb4d8d82fa58c4e426
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/16/2020
ms.locfileid: "97577779"
---
# <a name="sqlpackage-in-development-pipelines"></a>SqlPackage em pipelines de desenvolvimento

O **SqlPackage.exe** é um utilitário de linha de comando que automatiza diversas tarefas de desenvolvimento de banco de dados e pode ser incorporado em pipelines de CI/CD.

## <a name="managed-virtual-environments"></a>Ambientes virtuais gerenciados

Os ambientes virtuais usados para executores hospedados do GitHub Actions e imagens de VM do Azure Pipelines são gerenciados no repositório [virtual-environments](https://github.com/actions/virtual-environments) do GitHub.  O SqlPackage está incluído no ambiente `windows-latest`, e as atualizações das imagens são feitas dentro de algumas semanas de cada lançamento do SqlPackage.

## <a name="checking-the-sqlpackage-version"></a>Verificar a versão do SqlPackage

Durante os esforços de solução de problemas, é importante saber qual versão do SqlPackage está em uso.  Para capturar essas informações, você pode adicionar uma etapa ao pipeline para executar o SqlPackage com o parâmetro `/version`.  Abaixo, são fornecidos exemplos com base nos ambientes gerenciados da Microsoft e do GitHub; ambientes auto-hospedados podem ter caminhos de instalação diferentes para o diretório de trabalho.

### <a name="azure-pipelines"></a>Azure Pipelines

Ao usar a palavra-chave [script](https://docs.microsoft.com/azure/devops/pipelines/yaml-schema#script) em um Pipeline do Azure, uma etapa pode ser adicionada a um Pipeline do Azure, que gera o número da versão do SqlPackage.

```yaml
- script: sqlpackage.exe /version
  workingDirectory: C:\Program Files\Microsoft SQL Server\150\DAC\bin\
  displayName: 'get sqlpackage version'
```

### <a name="github-actions"></a>GitHub Actions

Ao usar a palavra-chave [run](https://docs.github.com/en/free-pro-team@latest/actions/reference/workflow-syntax-for-github-actions) no fluxo de trabalho de uma Ação do GitHub, uma etapa pode ser adicionada a uma Ação do GitHub, que gera o número da versão do SqlPackage.

```yaml
- name: get sqlpackage version
  working-directory: C:\Program Files\Microsoft SQL Server\150\DAC\bin\
  run: ./sqlpackage.exe /version
```

:::image type="content" source="media/sqlpackage-pipelines-github-action.png" alt-text="Saída da ação do GitHub exibindo o número de build 15.0.4897.1":::

## <a name="next-steps"></a>Próximas etapas

- Saiba mais sobre o [sqlpackage](sqlpackage.md)
