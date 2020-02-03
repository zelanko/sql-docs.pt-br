---
title: Criando um relatório de tabela básico (Tutorial do SSRS) | Microsoft Docs
ms.date: 04/16/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- walkthroughs [Reporting Services]
- tutorials [Reporting Services]
- reports [Reporting Services], creating
ms.assetid: 3b539b4b-26f2-4c0b-b506-80f175679a46
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: af41da75d553794019f1d01c8b8f5bb6aba80622
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "65103311"
---
# <a name="create-a-basic-table-report-ssrs-tutorial"></a>Criando um relatório de tabela básico (Tutorial do SSRS)

Neste tutorial, você usará a ferramenta do *Designer de Relatórios* no Visual Studio ou no SSDT (SQL Server Data Tools). Você criará um relatório paginado do SSRS (SQL Server Reporting Services). O relatório contém uma tabela de consulta criada a partir de dados no banco de dados AdventureWorks2016.

Conforme você progride neste tutorial, aprenderá a:
  
- criar um projeto de relatório.
- configurar uma conexão de dados.
- definir uma consulta.
- adicionar uma região de dados de tabela.
- formatar o relatório.
- campos de grupos e totais.
- visualizar o relatório.
- publicar o relatório opcionalmente.

## <a name="requirements"></a>Requisitos

Os seguintes componentes devem estar instalados no sistema para que você possa seguir este tutorial:

- Mecanismo de banco de dados do [!INCLUDE[msconame-md](../includes/msconame-md.md)] SQL Server.  
- SQL Server 2016 Reporting Services (SSRS) ou posteriores.
- O banco de dados AdventureWorks2016.  Para obter mais informações, confira os [Bancos de dados de exemplo do Adventure Works](https://github.com/Microsoft/sql-server-samples/releases).
- O [SQL Server Data Tools](../ssdt/download-sql-server-data-tools-ssdt.md) para o Visual Studio com a extensão do Reporting Services instalada para habilitar o acesso ao *Designer de Relatórios*.
  
Também é necessário ter permissões somente leitura para recuperar dados do banco de dados AdventureWorks2016.

**Tempo estimado para concluir o tutorial:** 30 minutos.

## <a name="next-steps"></a>Próximas etapas

[Lição 1: Criando um projeto do Servidor de Relatório &#40;Reporting Services&#41;](lesson-1-creating-a-report-server-project-reporting-services.md)

[Lição 2: Especificando informações sobre conexão &#40;Reporting Services&#41;](lesson-2-specifying-connection-information-reporting-services.md)

[Lição 3: Definindo um conjunto de dados para o relatório de tabela &#40;Reporting Services&#41;](lesson-3-defining-a-dataset-for-the-table-report-reporting-services.md)

[Lição 4: Adicionando uma tabela ao relatório &#40;Reporting Services&#41;](lesson-4-adding-a-table-to-the-report-reporting-services.md)

[Lição 5: Formatando um relatório &#40;Reporting Services&#41;](lesson-5-formatting-a-report-reporting-services.md)

[Lição 6: Adicionando agrupamentos e totais &#40;Reporting Services&#41;](lesson-6-adding-grouping-and-totals-reporting-services.md)

## <a name="see-also"></a>Confira também

[Tutoriais de Reporting Services](reporting-services-tutorials-ssrs.md) Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
