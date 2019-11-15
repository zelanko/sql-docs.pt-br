---
title: Biblioteca de funções olapR de R
description: Introdução à biblioteca de funções olapR nos Serviços de R do SQL Server 2016 e nos Serviços de Machine Learning do SQL Server com R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 507bd04140880a3c15f1e72eed49c29ade56769c
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715001"
---
# <a name="olapr-r-library-in-sql-server"></a>olapR (biblioteca de R no SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

O **olapR** é uma biblioteca da Microsoft de funções do R usadas para consultas MDX em um cubo OLAP do SQL Server Analysis Services. As funções não são compatíveis com todas as operações de MDX, mas você pode criar consultas que fatiam, dividem, analisam detalhadamente, efetuam rollup e dinamizam em dimensões. 

Este pacote não está pré-carregado em uma sessão de R. Execute o seguinte comando para carregar a biblioteca.

```R
library(olapR)
```

Você pode usar essa biblioteca em conexões a um cubo OLAP do Analysis Services em todas as versões compatíveis do SQL Server. Não há suporte para conexões a um modelo de tabela no momento.

## <a name="package-version"></a>Versão do pacote

A versão atual é a 1.0.0 em todos os produtos e downloads somente do Windows que fornecem a biblioteca.

## <a name="full-reference-documentation"></a>Documentação de referência completa

A biblioteca **olapr** é distribuída em vários produtos da Microsoft, mas o uso é o mesmo com a biblioteca no SQL Server ou em outro produto. Como as funções são as mesmas, a [documentação para funções individuais do sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) é publicada em apenas uma localização sob a [referência de R](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) para o Microsoft Machine Learning Server. Se existirem comportamentos específicos do produto, as discrepâncias serão indicadas na página de ajuda da função.

## <a name="availability-and-location"></a>Disponibilidade e localização

Esse pacote é fornecido nos seguintes produtos, bem como em várias imagens de máquina virtual no Azure. A localização do pacote varia de acordo.

Product | Local |
--------|----------|
Serviços de Machine Learning do SQL Server (com integração de R) | C:\Arquivos de Programas\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library | 
SQL Server 2016 R Services | C:\Arquivos de Programas\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library
Microsoft Machine Learning Server (R Server) | C:\Arquivos de Programas\Microsoft\R_SERVER\library |
Cliente do Microsoft R | C:\Arquivos de Programas\Microsoft\R Client\R_SERVER\library |
Máquina Virtual de Ciência de Dados (no Azure) | C:\Arquivos de Programas\Microsoft\R Client\R_SERVER\library |
Máquina Virtual do SQL Server (no Azure) <sup>1</sup> | C:\Arquivos de Programas\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library |

<sup>1</sup> A integração do R é opcional no SQL Server. A biblioteca olapR será instalada quando você adicionar o Machine Learning ou o recurso de R durante a configuração da VM.


## <a name="see-also"></a>Confira também

[Como criar consultas MDX usando olapR](how-to-create-mdx-queries-using-olapr.md)
