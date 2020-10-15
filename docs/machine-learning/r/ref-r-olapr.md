---
title: Pacote de R olapR
description: O olapR é um pacote de R da Microsoft usado para consultas MDX em um cubo OLAP do SQL Server Analysis Services. As funções não são compatíveis com todas as operações de MDX, mas você pode criar consultas que fatiam, dividem, analisam detalhadamente, efetuam rollup e dinamizam em dimensões. O pacote está incluído nos Serviços de Machine Learning do SQL Server e no SQL Server 2016 R Services.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 07/14/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f34a6d26e48c1a77d7e289b197495d707bb9fd12
ms.sourcegitcommit: afb02c275b7c79fbd90fac4bfcfd92b00a399019
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2020
ms.locfileid: "91956867"
---
# <a name="olapr-r-package-in-sql-server-machine-learning-services"></a>olapR (pacote de R nos Serviços de Machine Learning do SQL Server)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

O **olapR** é um pacote de R da Microsoft usado para consultas MDX em um cubo OLAP do SQL Server Analysis Services. As funções não são compatíveis com todas as operações de MDX, mas você pode criar consultas que fatiam, dividem, analisam detalhadamente, efetuam rollup e dinamizam em dimensões. O pacote está incluído nos [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md) e no [SQL Server 2016 R Services](sql-server-r-services.md).

Você pode usar esse pacote em conexões com um cubo OLAP do Analysis Services em todas as versões compatíveis do SQL Server. Não há suporte para conexões a um modelo de tabela no momento.

## <a name="load-package"></a>Carregar pacote

O pacote **olapR** não é pré-carregado em uma sessão de R. Execute o comando a seguir para carregar o pacote.

```R
library(olapR)
```

## <a name="package-version"></a>Versão do pacote

A versão atual é a 1.0.0 em todos os produtos e downloads somente do Windows que fornecem o pacote.

## <a name="full-reference-documentation"></a>Documentação de referência completa

O pacote **olapr** é distribuído em vários produtos da Microsoft, mas o uso é o mesmo com o pacote no SQL Server ou em outro produto. Como as funções são as mesmas, a [documentação para funções individuais do sqlrutils](/machine-learning-server/r-reference/olapr/olapr) é publicada em apenas uma localização sob a [referência de R](/machine-learning-server/r-reference/introducing-r-server-r-package-reference) para o Microsoft Machine Learning Server. Se existirem comportamentos específicos do produto, as discrepâncias serão indicadas na página de ajuda da função.

## <a name="availability-and-location"></a>Disponibilidade e localização

Esse pacote é fornecido nos seguintes produtos, bem como em várias imagens de máquina virtual no Azure. A localização do pacote varia de acordo.

Produto | Location |
--------|----------|
Serviços de Machine Learning do SQL Server (com integração de R) | C:\Arquivos de Programas\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library | 
SQL Server 2016 R Services | C:\Arquivos de Programas\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library
Microsoft Machine Learning Server (R Server) | C:\Arquivos de Programas\Microsoft\R_SERVER\library |
Cliente do Microsoft R | C:\Arquivos de Programas\Microsoft\R Client\R_SERVER\library |
Máquina Virtual de Ciência de Dados (no Azure) | C:\Arquivos de Programas\Microsoft\R Client\R_SERVER\library |
Máquina Virtual do SQL Server (no Azure) <sup>1</sup> | C:\Arquivos de Programas\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library |

<sup>1</sup> A integração do R é opcional no SQL Server. O pacote olapR será instalado quando você adicionar o Machine Learning ou o recurso de R durante a configuração da VM.


## <a name="see-also"></a>Confira também

[Como criar consultas MDX usando olapR](how-to-create-mdx-queries-using-olapr.md)