---
title: "No banco de dados análise do Python para desenvolvedores em SQL | Microsoft Docs"
ms.custom: 
ms.date: 05/25/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 984ff8097b1f28cf11e28cc464c88dc3b9580a12
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="in-database-python-analytics-for-sql-developers"></a>No banco de dados análise do Python para desenvolvedores em SQL

O objetivo deste passo a passo é fornecer os programadores SQL com experiência prática na criação de uma solução no SQL Server de aprendizado de máquina. Este passo a passo, você aprenderá como incorporar Python em um aplicativo, adicionando o código Python para procedimentos armazenados.

> [!NOTE]
> Preferir R? Consulte [este tutorial](sqldev-in-database-r-for-sql-developers.md), que fornece uma solução semelhante, mas usa o R e eb que pode executar no SQL Server 2016 ou 2017 do SQL Server.

## <a name="overview"></a>Visão geral

O processo de criação de uma solução de ponta a ponta normalmente consiste na obtenção e limpeza de dados, exploração de dados e engenharia de recursos, treinamento do modelo e ajuste e, por fim, na implantação do modelo em produção. Desenvolvimento e teste do código real é mais bem executada usando um ambiente de desenvolvimento dedicado, como essas ferramentas Python:

+ PyCharm, um IDE popular
+ Spyder, que está incluído no [2017 do Visual Studio](https://blogs.msdn.microsoft.com/visualstudio/2017/05/12/a-lap-around-python-in-visual-studio-2017/) se você instalar o [cargas de trabalho de ciência de dados](https://blogs.msdn.microsoft.com/visualstudio/2016/11/18/data-science-workloads-in-visual-studio-2017-rc/)
+ [Extensões do Python para Visual Studio](https://docs.microsoft.com/visualstudio/python/python-in-visual-studio).

Depois de ter criado e testado a solução no IDE, você pode implantar o código Python para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimentos armazenados no ambiente familiar do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].

Neste passo a passo, vamos supor que você tenha recebido todo o código Python necessário para a solução, e você vai se concentrar em criar e implantar a solução usando o SQL Server.

- [Etapa 1: Baixar os dados de exemplo](sqldev-py1-download-the-sample-data.md)

  Baixe o conjunto de dados de exemplo e todos os arquivos de script para um computador local.

- [Etapa 2: Importar dados para o SQL Server usando o PowerShell](sqldev-py2-import-data-to-sql-server-using-powershell.md)

  Execute um script do PowerShell que cria um banco de dados e uma tabela na instância especificada e carrega os dados de exemplo para a tabela.

- [Etapa 3: Explorar e visualizar os dados](sqldev-py3-explore-and-visualize-the-data.md)

  Executar a exploração de dados básicos e visualização, pela chamada Python de [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimentos armazenados.

- [Etapa 4: Criar recursos de dados usando o T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

  Crie novos recursos de dados usando funções personalizadas do SQL.
  
- [Etapa 5: Treinar e salvar um modelo usando o T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

   Criar e salvar o modelo de aprendizado de máquina, usando Python em procedimentos armazenados.
  
-  [Etapa 6: Colocar o modelo em operação](sqldev-py6-operationalize-the-model.md)

  Depois que o modelo foi salvo no banco de dados, chame o modelo de previsão usando [!INCLUDE[tsql](../../includes/tsql-md.md)].

> [!NOTE]
> É recomendável que você não use [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para gravar ou testar o código Python. Se o código que você inserir em um procedimento armazenado tiver problemas, as informações que são retornadas pelo procedimento armazenado serão geralmente inadequadas entender a causa do erro.


### <a name="scenario"></a>Cenário

Esse passo a passo usa o conjunto de dados conhecido NYC Taxi. Para tornar este passo a passo rápido e fácil, os dados são amostrados. Usando esses dados, você criará um modelo de classificação binária que prevê se uma viagem específica é provável obter uma dica ou não, com base em colunas, como a hora do dia, distância e local de coleta.

### <a name="requirements"></a>Requisitos

Esse passo a passo é destinado a usuários já familiarizados com operações de banco de dados fundamentais, como criação de tabelas e bancos de dados, importação de dados em tabelas e criação de consultas SQL.

Todo o código Python é fornecido. Um programador experiente do SQL deve conseguir concluir esse passo a passo usando o [!INCLUDE[tsql](../../includes/tsql-md.md)] no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou executando os scripts do PowerShell fornecidos.

Antes de iniciar o passo a passo, você deve concluir esses preparativos:

- Instalar uma instância do SQL Server 2017 com serviços de aprendizado de máquina e Python habilitado (requer o CTP 2.0 ou posterior).
- O logon usado para este passo a passo deve ter permissões para criar bancos de dados e outros objetos, carregar dados, selecionar dados e executar procedimentos armazenados.

## <a name="next-step"></a>Próxima etapa

  [Etapa 1: Baixar os dados de exemplo](sqldev-py1-download-the-sample-data.md)

## <a name="see-also"></a>Consulte também

[Serviços de aprendizado de máquina com Python](../python/sql-server-python-services.md)



