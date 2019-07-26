---
title: biblioteca de funções olapr R
description: Introdução à biblioteca de funções olapr no SQL Server 2016 R Services e SQL Server 2017 Serviços de Machine Learning com R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 2363b9ba69f914f828d7445a88d6ee1c784bb096
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344881"
---
# <a name="olapr-r-library-in-sql-server"></a>olapr (biblioteca do R no SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

o olapr é uma biblioteca da Microsoft de funções do R usadas para consultas MDX em um SQL Server Analysis Services cubo OLAP. As funções não dão suporte a todas as operações de MDX, mas você pode criar consultas que fatiam, combuscam, acúmulos e dinamizações em dimensões. 

Este pacote não está pré-carregado em uma sessão de R. Execute o comando a seguir para carregar a biblioteca.

```R
library(olapR)
```

Você pode usar essa biblioteca em conexões a um Analysis Services cubo OLAP em todas as versões com suporte do SQL Server. Não há suporte para conexões a um modelo de tabela no momento.

## <a name="package-version"></a>Versão do pacote

A versão atual é a 1.0.0 em todos os produtos e downloads somente do Windows que fornecem a biblioteca.

## <a name="full-reference-documentation"></a>Documentação de referência completa

A  biblioteca olapr é distribuída em vários produtos da Microsoft, mas o uso é o mesmo se você obter a biblioteca em SQL Server ou em outro produto. Como as funções são as mesmas, a [documentação para funções individuais sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) é publicada em apenas um local sob a [referência de R](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) para Microsoft Machine Learning Server. Se existirem comportamentos específicos do produto, as discrepâncias serão indicadas na página de ajuda da função.

## <a name="availability-and-location"></a>Disponibilidade e local

Esse pacote é fornecido nos seguintes produtos, bem como em várias imagens de máquina virtual no Azure. O local do pacote varia de acordo.

Produto | Location |
--------|----------|
SQL Server 2017 Serviços de Machine Learning (com a integração do R) | C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library | 
SQL Server 2016 R Services | C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library
Microsoft Machine Learning Server (R Server) | C:\Arquivos de Files\Microsoft\R_SERVER\library |
Cliente do Microsoft R | C:\Arquivos de Files\Microsoft\R Client\R_SERVER\library |
Máquina Virtual de Ciência de Dados (no Azure) | C:\Arquivos de Files\Microsoft\R Client\R_SERVER\library |
SQL Server máquina virtual (no Azure) <sup>1</sup> | C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library |

<sup>1</sup> a integração de R é opcional em SQL Server. A biblioteca olapr será instalada quando você adicionar o Machine Learning ou o recurso de R durante a configuração da VM.


## <a name="see-also"></a>Confira também

[Como criar consultas MDX usando olapr](how-to-create-mdx-queries-using-olapr.md)
