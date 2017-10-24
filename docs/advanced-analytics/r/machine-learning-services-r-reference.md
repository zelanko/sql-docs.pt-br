---
title: "Referência de API para serviços de aprendizado de máquina do SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 07/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1c776c43d66d01a2f721b5d3d8bc540741bf8b13
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---

# <a name="api-reference-for-sql-server-machine-learning-services"></a>Referência de API para serviços de aprendizado de máquina do SQL Server

Este artigo fornece links para a documentação de referência para APIs usadas pelo SQL Server de aprendizado de máquina. 

**Aplica-se a:** R Services do SQL Server 2016, SQL Server 2017 serviços de aprendizado de máquina

A maior parte do tempo, o SQL Server consome as mesmas bibliotecas de R e Python fornecidas no Microsoft R Server e o servidor de aprendizado de máquina do Microsoft. 

> [!NOTE]
> Documentação para todas as APIs é derivada do código-fonte e não é editada após.

## <a name="r"></a>R

+ [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)

    Algoritmos escalonáveis que oferecem suporte a várias fontes de dados e contextos de computação remota.

+ [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)

    Máquina rápida e dimensionável transformações e algoritmos de aprendizado para R. requer RevoScaleR.

+ [olapR](https://docs.microsoft.com/r-server/r-reference/olapr/olapr)

   Lê o esquema de fontes de dados OLAP e executa consultas MDX.

+ [sqlrutils](https://docs.microsoft.com/r-server/r-reference/sqlrutils/sqlrutils)

    Funções auxiliares para gerar um procedimento armazenado bem formado de código R.

+ [mrsdeploy](https://docs.microsoft.com/r-server/r-reference/mrsdeploy/mrsdeploy-package)

   Funções para estabelecer uma sessão remota em um aplicativo de console e para publicar e gerenciar um serviço web que usa o código de R ou Python.

## <a name="python"></a>Python

+ [revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)

    Equivalente de Python do pacote RevoScaleR para a linguagem R. Suporta as mesmas fontes de dados e contextos de computação.

+ [Microsoftml para Python](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package)

    Equivalente a Python a MicrosoftML do pacote para oferece suporte a R. o mesmo contextos de computação e fontes de dados e inclui rápida, algoritmos escalonáveis e transformações da Microsoft.

## <a name="related-apis"></a>APIs relacionadas

+ [Referência de função RevoPEMAR](https://docs.microsoft.com/r-server/r-reference/revopemar/pemar)

    Dá suporte ao desenvolvimento de algoritmos paralelos

+ [RevoUtils](https://docs.microsoft.com/r-server/r-reference/revoutils/revoutils)

    Funções de utilitário para uso com ambientes RevoScaleR

## <a name="other"></a>Outro

Tópicos "Como" e resumos específicos para usar esses R ou APIs de Python no SQL Server podem ser encontrados aqui:

+ [Funções scaleR para trabalhar com o SQL Server](scaler-functions-for-working-with-sql-server-data.md)
+ [Gerar um procedimento armazenado usando sqlrutils](generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)
+ [Ler dados do MDX em R usando olapR](how-to-create-mdx-queries-using-olapr.md)

