---
title: "Referência de API para serviços de aprendizado de máquina do SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 10/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 4447df04e7bffe4d5103be1cb93791a151b81857
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2017
---
# <a name="api-reference-for-sql-server-machine-learning-services"></a>Referência de API para serviços de aprendizado de máquina do SQL Server

Este artigo fornece links para a documentação de referência para APIs usadas pelo SQL Server de aprendizado de máquina.

**Aplica-se a:** R Services do SQL Server 2016, SQL Server 2017 serviços de aprendizado de máquina

A maior parte do tempo, o SQL Server consome as mesmas bibliotecas de R e Python fornecidas no Microsoft R Server e o servidor de aprendizado de máquina do Microsoft. 

> [!NOTE]
> Documentação para todas as APIs é derivada do código-fonte e não foi editada. Se você encontrar erros, adicione um comentário na documentação de referência de API. 

## <a name="r"></a>R

+ [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)

    Algoritmos escalonáveis que oferecem suporte a várias fontes de dados e contextos de computação remota.

+ [MicrosoftML](https://docs.microsoft.com/machine-learning-serverr-reference/microsoftml/microsoftml-package)

    Máquina rápida e dimensionável transformações e algoritmos de aprendizado para R. requer RevoScaleR.

+ [olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr)

   Lê o esquema de fontes de dados OLAP e executa consultas MDX.

+ [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)

    Funções auxiliares para gerar um procedimento armazenado bem formado de código R.

+ [mrsdeploy](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)

   Funções para estabelecer uma sessão remota em um aplicativo de console e para publicar e gerenciar um serviço web que usa o código de R ou Python.

## <a name="python"></a>Python

+ [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)

    Equivalente de Python do pacote RevoScaleR para a linguagem R. Suporta as mesmas fontes de dados e contextos de computação.

+ [Microsoftml para Python](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)

    Equivalente a Python a MicrosoftML do pacote para oferece suporte a R. o mesmo contextos de computação e fontes de dados e inclui rápida, algoritmos escalonáveis e transformações da Microsoft. 

## <a name="related-apis"></a>APIs relacionadas

+ [Referência de função RevoPEMAR](https://docs.microsoft.com/machine-learning-server/r-reference/revopemar/pemar)

    Dá suporte ao desenvolvimento de algoritmos paralelos

+ [RevoUtils](https://docs.microsoft.com/machine-learning-server/r-reference/revoutils/revoutils)

    Funções de utilitário para uso com ambientes RevoScaleR

## <a name="other"></a>Outro

Tópicos "Como" e resumos específicos para usar esses R ou APIs de Python no SQL Server podem ser encontrados aqui:

+ [Funções scaleR para trabalhar com o SQL Server](scaler-functions-for-working-with-sql-server-data.md)
+ [Gerar um procedimento armazenado usando sqlrutils](generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)
+ [Ler dados do MDX em R usando olapR](how-to-create-mdx-queries-using-olapr.md)
