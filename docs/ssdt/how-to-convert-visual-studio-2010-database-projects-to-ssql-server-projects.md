---
title: Converter projetos de banco de dados do Visual Studio 2010 em projetos de banco de dados do SQL Server
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
f1_keywords:
- sql.data.tools.projectconversion.dialog
- sql.data.tools.ImportDAC
ms.assetid: 7e5acf94-5c46-44c7-9ff5-ca7926f5332a
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: d81099054c52b90154bfe6fd42c9d450e17afa01
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75241546"
---
# <a name="how-to-convert-a-visual-studio-2010-database-projects-to-sql-server-database-projects-and-retarget-to-a-different-platform"></a>Como converter projetos de banco de dados do Visual Studio 2010 em projetos de banco de dados do SQL Server e redirecionar para uma plataforma diferente

No SSDT (SQL Server Data Tools), você pode converter projetos existentes de Banco de Dados, CLR e Aplicativo da Camada de Dados do SQL Server criados no Visual Studio 2010 no novo projeto de banco de dados do SQL Server. Ao fazer isso, você pode aproveitar as vantagens da nova experiência de desenvolvimento de bancos de dados proporcionada pelo SSDT, como uma experiência atualizada de edição do Transact\-SQL e a capacidade de redirecionar seu projeto para o Microsoft SQL Server 2012 e para o SQL Azure com validação de código. O processo de conversão converte objetos (tabela, exibições, procedimentos armazenados ou scripts) que tenham um tipo equivalente no SSDT, incluindo as respectivas permissões e os arquivos de política DAC. Artefatos que não podem ser convertidos são realçados em um log/relatório de conversão.  
  
A tabela a seguir lista todos os artefatos de projeto que podem ou não ser convertidos pelo SSDT.  
  
|Artefatos de projeto que podem ser convertidos|Artefatos de projeto que não podem ser convertidos|  
|-------------------------------------------|----------------------------------------------|  
|Arquivos de projeto<br /><br />Arquivos de projeto .dbproj (projetos do Banco de dados e do Servidor do Visual Studio 2010, projetos de Aplicativo da Camada de Dados)<br /><br />Os arquivos de projeto .csproj e .vbproj CLR podem ser convertidos, mas podem resultar em perda de dados|Projetos de teste de unidade de banco de dados<br /><br />Projetos parciais como itens de .files|  
|Arquivos de propriedades<br /><br />Arquivos * .sqldeployment, .sqlsettings e .sqlpolicy são convertidos para suas páginas de Propriedades de Projeto correspondentes<br /><br />Arquivos .sqlpermissions são convertidos em scripts Transact\-SQL|Propriedades do Projeto<br /><br />Server.sqlsettings<br /><br />Variáveis SQLCMD definidas em arquivos .sqlcmd|  
|Arquivos .sql são importados usando sua estrutura de pasta existente.|Arquivos de extensibilidade|  
|Scripts de pré-implantação e pós-implantação|As referências de banco de dados terão que ser restabelecidas manualmente depois da conversão do projeto.|  
|Arquivos de comparação de esquema|Arquivos de geração de dados.|  
  
### <a name="to-convert-a-project"></a>Para converter um projeto  
  
1.  Abra um projeto de banco de dados do SQL Server 2005 ou 2008.  
  
2.  O assistente **Converter em Projeto de Banco de Dados do SQL Server** é aberto automaticamente. Selecione **Converter em Projeto de Banco de Dados do SQL Server** e clique em **OK**. Mantenha a configuração padrão para fazer o backup de arquivos verificados existentes.  
  
3.  Um relatório de conversão é gerado automaticamente, listando todos os arquivos que foram convertidos. Para ler mais informações sobre o processo de conversão, clique no sinal **+** ao lado do nome de arquivo do projeto.  
  
4.  Observe que, no **Gerenciador de Soluções**, o arquivo de projeto, os arquivos de propriedade e os objetos de esquema são todos convertidos.  
  
### <a name="to-change-a-projects-target-platform"></a>Para alterar a plataforma de destino de um projeto  
  
1.  Clique com o botão direito do mouse no projeto convertido no **Gerenciador de Soluções** e selecione **Propriedades** para acessar a caixa de diálogo **Configurações de Projeto**.  
  
2.  Selecione as plataformas com suporte pelo SSDT na lista suspensa **Plataforma de Destino**.  
  
## <a name="see-also"></a>Consulte Também  
[Como alterar a plataforma de destino e publicar um projeto de banco de dados](../ssdt/how-to-change-target-platform-and-publish-a-database-project.md)  
  
