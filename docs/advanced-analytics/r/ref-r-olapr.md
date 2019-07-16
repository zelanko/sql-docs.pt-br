---
title: biblioteca de funções olapR R - serviços do SQL Server Machine Learning
description: Introdução à biblioteca de função olapR no SQL Server 2016 R Services e os serviços do SQL Server 2017 Machine Learning com R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 431fddf870b5755691cad92e576c95d0d3a83890
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962492"
---
# <a name="olapr-r-library-in-sql-server"></a>olapR (biblioteca de R no SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**olapR** é uma biblioteca da Microsoft de funções de R usados para consultas MDX em um cubo OLAP do Analysis Services do SQL Server. Funções não dão suporte a todas as operações de MDX, mas você pode criar consultas para essa fatia, fracione, corte, busca detalhada, pacote cumulativo de atualizações e dinamizar em dimensões. 

Este pacote não é pré-carregado em uma sessão do R. Execute o seguinte comando para carregar a biblioteca.

```R
library(olapR)
```

Você pode usar essa biblioteca em conexões com um cubo OLAP do Analysis Services em todas as versões com suporte do SQL Server. Não há suporte para conexões a um modelo tabular no momento.

## <a name="package-version"></a>Versão do pacote

Versão atual é 1.0.0 em todos os produtos somente para Windows e downloads fornecendo a biblioteca.

## <a name="full-reference-documentation"></a>Documentação de referência completo

O **olapr** biblioteca é distribuída em vários produtos da Microsoft, mas o uso é o mesmo se você obter a biblioteca no SQL Server ou outro produto. Porque as funções são os mesmos, [documentação para funções individuais sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) for publicado em apenas um local sob a [referência de R](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) para Microsoft Machine Learning Server. Deve qualquer produto específico comportamentos existirem, serão observadas o discrepâncias na página de ajuda de função.

## <a name="availability-and-location"></a>Disponibilidade e o local

Este pacote é fornecido nos seguintes produtos, bem como várias imagens de máquina virtual no Azure. Local do pacote varia de acordo.

Produto | Location |
--------|----------|
Serviços do SQL Server 2017 Machine Learning (com a integração do R) | C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library | 
SQL Server 2016 R Services | C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library
Microsoft Machine Learning Server (R Server) | C:\Program Files\Microsoft\R_SERVER\library |
Cliente do Microsoft R | C:\Program Files\Microsoft\R Client\R_SERVER\library |
Máquina de Virtual de ciência de dados (no Azure) | C:\Program Files\Microsoft\R Client\R_SERVER\library |
Máquina Virtual do SQL Server (no Azure) <sup>1</sup> | C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library |

<sup>1</sup> integração do R é opcional no SQL Server. A biblioteca olapR será instalada quando você adiciona o aprendizado de máquina ou o recurso do R durante a configuração da VM.


## <a name="see-also"></a>Confira também

[Como criar consultas MDX usando olapR](how-to-create-mdx-queries-using-olapr.md)
