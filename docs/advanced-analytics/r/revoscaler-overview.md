---
title: RevoScaleR | Microsoft Docs
ms.custom: 
ms.date: 11/29/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 8f5df8a224b67be06e5459fc8a65277ddc05f4f6
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2018
---
# <a name="revoscaler"></a>RevoScaleR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

RevoScaleR é um pacote de funções de aprendizado de máquina, fornecido pela Microsoft, que oferece suporte a ciência de dados em grande escala.

+ Suportam a funções de importação de dados, transformação de dados, resumo, visualização e análise.

+ _Em escala_ significa que as operações podem ser executadas em grandes conjuntos de dados, em paralelo e distribuídas em sistemas de arquivos. Os algoritmos podem operar em conjuntos de dados que não cabem na memória, usando o agrupamento e pelos resultados de remontagem quando operações forem concluídas.

+ RevoScaleR fornece muitas melhorias em funções de R de software livre. Há funções de RevoScaleR correspondente a muitas das funções de base R mais populares. Funções de RevoScaleR são indicadas com um **rx** ou **Rx** prefixo para torná-los mais fáceis de identificar.

+ RevoScaleR serve como uma plataforma para ciência de dados distribuído. Por exemplo, você pode usar as transformações e contextos de computação RevoScaleR com os algoritmos de arte em [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-the-microsoftml-package). Você também pode usar [rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec) para executar funções básicas de R em paralelo.

Para obter exemplos de RevoScaleR em ação, consulte esses blogs: 

+ [Criar e implantar um modelo de previsão usando R e SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/)

+ [Previsões de um milhão por segundo, com o servidor de aprendizado de máquina](https://blogs.msdn.microsoft.com/mlserver/2017/10/15/1-million-predictionssec-with-machine-learning-server-web-service/)

+ [Prevendo dicas táxi usando MicrosoftML](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2017/01/17/predicting-nyc-taxi-tips-using-microsoftml/)

+ [Otimização de desempenho com rxExec](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2016/11/14/performance-optimization-when-using-rxexec-to-parallelize-algorithms/)

## <a name="how-to-get-revoscaler"></a>Como obter o RevoScaleR

O pacote RevoScaleR para R está instalado gratuitamente no cliente do Microsoft R. Se você tiver um servidor de aprendizado de máquina ou usando o R no SQL Server, RevoScaleR está incluído por padrão.

Se você estiver usando o Python, o [revoscalepy](../python/what-is-revoscalepy.md) pacote fornece funcionalidade equivalente.

> [!IMPORTANT]
> O pacote RevoScaleR não pode ser baixado ou usado independentemente de produtos e serviços que fornecem a ele.

## <a name="use-revoscaler-in-sql-server"></a>Usar RevoScaleR no SQL Server

Esses tutoriais e exemplos demonstram como usar funções de RevoScaleR para obter dados do SQL Server, criar modelos e salvar modelos para um banco de dados para pontuação.

+ [Aprenda a usar os contextos de computação](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [R para desenvolvedores SQL: treinar e utilizar um modelo](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [Exemplos de produtos da Microsoft no GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples)

## <a name="learn-more-about-revoscaler"></a>Saiba mais sobre o RevoScaleR

Esses tutoriais demonstram o uso de RevoScaleR em outros contextos de computação com suporte [Server de aprendizado de máquina](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server), incluindo o Hadoop.

+ [O que é RevoScaleR?](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-revoscaler)

+ [Explorar RevoScaleR em 25 funções](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler)

+ [Referência de pacote RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)

