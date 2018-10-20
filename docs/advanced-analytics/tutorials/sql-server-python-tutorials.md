---
title: Tutoriais do Python do SQL Server | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 5cafb253cea118148bd654ea770234843f742838
ms.sourcegitcommit: b1990ec4491b5a8097c3675334009cb2876673ef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/17/2018
ms.locfileid: "49383331"
---
# <a name="sql-server-python-tutorials"></a>Tutoriais do Python do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo fornece uma lista de tutoriais e exemplos que demonstram o uso do Python com o SQL Server 2017. Por meio desses exemplos e demonstrações, você aprenderá:

+ Como executar o Python no T-SQL
+ Quais são os contextos de computação local e remoto e como você pode executar o código do Python usando o computador do SQL Server
+ Como encapsular o código do Python em um procedimento armazenado
+ Otimizando o código do Python para um ambiente de produção do SQL
+ Cenários do mundo real para a inserção de aprendizado de máquina em aplicativos

Para obter informações sobre os requisitos e instalação, consulte [pré-requisitos](#bkmk_Prerequisites).

## <a name="bkmk_pythontutorials"></a>Tutoriais do Python

+ [Execução de Python no T-SQL](run-python-using-t-sql.md)

   Conheça os fundamentos de como chamar o Python no T-SQL, usando o mecanismo de extensibilidade pioneiro no SQL Server 2016.

+ [Criar um modelo de machine learning no Python usando revoscalepy](use-python-revoscalepy-to-create-model.md)

   Esta lição demonstra como você pode executar o código de um terminal de Python remoto, usando o contexto de computação do SQL Server. Você deve ser um pouco familiarizado com os ambientes e ferramentas do Python. Código de exemplo é fornecido que cria um modelo usando **rxLinMod**, da nova **revoscalepy** biblioteca. 

+ [Análise de Python no banco de dados para desenvolvedores do SQL](sqldev-in-database-python-for-sql-developers.md)

    Este passo a passo de ponta a ponta demonstra o processo de criação de uma solução completa do Python usando procedimentos armazenados T-SQL. Todo o código Python é incluído.


## <a name="python-samples"></a>Exemplos de Python

Esses exemplos e demonstrações fornecidas pela equipe de desenvolvimento do SQL Server realçam maneiras que você pode usar a análise inserida em aplicativos do mundo real.

+ [Criar um modelo preditivo usando o Python e o SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)

  Saiba como uma empresa de aluguel de Esqui pode usar o aprendizado de máquina para prever o futuras locações, que ajuda a equipe e plano de negócios para atender às demandas futuras.

  > [!TIP]
  > Agora inclui a pontuação nativa de modelos em Python!

+ [Executar o cliente clustering usando o Python e o SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/)

    Saiba como usar o algoritmo Kmeans para executar o clustering sem supervisão de clientes.

## <a name="see-also"></a>Confira também

[Tutoriais de R para SQL Server](sql-server-r-tutorials.md)
