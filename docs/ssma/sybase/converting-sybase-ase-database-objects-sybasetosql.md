---
title: Converter objetos de banco de dados ASE Sybase (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Converting Database Objects
ms.assetid: 509cb65d-2f54-427a-83d7-37919cc4e3e3
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: a27ec04406e17a6fdb06aa708b443bba8ecd3d52
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="converting-sap-ase-database-objects-sybasetosql"></a>Converter objetos de banco de dados do SAP ASE (SybaseToSQL)
Depois que você se conectou ao SAP Adaptive Server Enterprise (ASE), conectado ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure e conjunto de projeto e as opções de mapeamento de dados, você pode converter objetos de banco de dados do SAP Adaptive Server Enterprise (ASE) para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados do SQL Azure objetos.  
  
## <a name="the-conversion-process"></a>O processo de conversão  
Converter objetos de banco de dados usa as definições de objeto do ASE, converte-os em semelhante [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure objetos e, em seguida, carrega essas informações para os metadados do SSMA. Não carrega as informações para a instância da [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure. Você pode exibir os objetos e suas propriedades usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou o Gerenciador de metadados do SQL Azure.
  
Durante a conversão, o SSMA imprime mensagens de saída para as mensagens de erro e de painel de saída para o **lista de erros** painel. Use as informações de saída e de erro para determinar se você precisa modificar seus bancos de dados ASE ou o processo de conversão para obter os resultados da conversão desejada.  
  
## <a name="setting-conversion-options"></a>Definindo opções de conversão  
Antes de converter objetos, examine as opções de conversão de projeto no **configurações de projeto** caixa de diálogo. Usando essa caixa de diálogo, você pode definir como o SSMA converte funções e variáveis globais. Para obter mais informações, consulte [configurações de projeto &#40;conversão&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md).  
  
## <a name="converting-ase-database-objects"></a>Converter objetos de banco de dados ASE  
Para converter objetos de banco de dados ASE, primeiro selecionar os objetos que você deseja converter e, em seguida, o SSMA executar a conversão. Para exibir mensagens de saída durante a conversão no **exibição** menu, selecione **saída**.  
  
**Para converter objetos ASE em sintaxe de SQL Server ou SQL Azure**  
  
1.  No Gerenciador de metadados do Sybase, expanda o servidor ASE e, em seguida, expanda **bancos de dados**.  
  
2.  Selecione objetos para converter:  
  
    -   Para converter todos os bancos de dados, selecione a caixa de seleção ao lado de **bancos de dados**.  
  
    -   Para converter ou omitir um banco de dados, marque ou desmarque a caixa de seleção ao lado do nome do banco de dados.  
  
    -   Para converter ou omitir esquemas individuais, expanda o banco de dados, **esquemas**e, em seguida, marque ou desmarque a caixa de seleção ao lado do esquema.  
  
    -   Para converter ou omitir uma categoria de objetos, expanda o esquema e, em seguida, marque ou desmarque a caixa de seleção ao lado da categoria.  
  
    -   Para converter ou omitir os objetos individuais, expanda a pasta de categoria e, em seguida, marque ou desmarque a caixa de seleção ao lado do objeto.  
  
3.  Para converter todos os objetos selecionados, clique com botão direito **bancos de dados**e, em seguida, selecione **converter esquema**.  
  
    Você também pode converter objetos individuais ou as categorias de objetos, clicando duas vezes o objeto ou a pasta que contém e, em seguida, selecionando **converter esquema**.  
  
> [!NOTE]  
> Algumas das funções do sistema SAP ASE corresponderem exatamente as funções do sistema do SQL Server equivalentes no comportamento. Para emular o comportamento do SAP ASE, SSMA gera funções definidas pelo usuário no banco de dados do SQL Server convertido em um esquema chamado 's2ss'. Dependendo das configurações de projeto, algumas das funções do sistema do SQL Server são substituídas por essas funções emuladas. O SSMA cria as seguintes funções definidas pelo usuário:  
  
||||  
|-|-|-|  
|**char_length_nvarchar**|**index_colorder**|**ssma_datepart**|  
|**char_length_varchar**|**inttohex**|**substring_nvarchar**|  
|**charindex_nvarchar**|**ssma_datediff**|**substring_varbinary**|  
|**charindex_varchar**|**hextoint**|**substring_varchar**|  
|**ulowsurr**|**to_unichar**|**ssma_current_time**|  
|**uhighsurr**|||  
  
## <a name="objects-not-supported-in-azure-sql"></a>Objetos sem suporte no SQL Azure  
As seguintes palavras-chave do T-SQL são usadas por SSMA para SAP ASE durante a conversão para o local do SQL Server, mas não há suporte para essas palavras-chave pela sintaxe do T-SQL do SQL Azure:  
  
||||  
|-|-|-|  
|CHECKPOINT|CREATE/ALTER/DROP DEFAULT|CREATE/DROP RULE|  
|DBCC TRACEOFF|DBCC TRACEON|TODOS OS GRANT/REVOKE/DENY|  
|KILL|READTEXT|SELECT INTO|  
|SET OFFSETS|SETUSER|SHUTDOWN|  
|WRITETEXT|||  
  
## <a name="viewing-conversion-problems"></a>Problemas de conversão de exibição  
Alguns objetos do SAP ASE não podem converter. Você pode determinar as taxas de sucesso de conversão exibindo o relatório de resumo de conversão.  
  
**Para exibir um relatório de resumo**  
  
1.  No Gerenciador de metadados do Sybase, selecione **bancos de dados**.  
  
2.  No painel direito, selecione o **relatório** guia.  
  
    Este relatório mostra o relatório de resumo de avaliação para todos os objetos de banco de dados que tenham sido avaliada ou convertidos. Você também pode exibir um relatório de resumo para objetos individuais:  
  
    -   Para exibir o relatório para um banco de dados individual, selecione o banco de dados no Gerenciador de metadados do Sybase.  
  
    -   Para exibir o relatório para um objeto de banco de dados individual, selecione o objeto no Gerenciador de metadados do Sybase. Objetos que têm problemas de conversão têm um ícone de erro vermelho.  
  
Para objetos que falha na conversão, você pode exibir a sintaxe que resultaram em falha de conversão.  
  
**Para exibir os problemas de conversão individuais**  
  
1.  No Gerenciador de metadados do Sybase, expanda **bancos de dados**.  
  
2.  Expanda o banco de dados que mostra um ícone de erro vermelho.  
  
3.  Expanda o **esquemas** pasta e, em seguida, expanda o esquema que mostra um ícone de erro vermelho.  
  
4.  No esquema, expanda uma pasta que tem um ícone de erro vermelho.  
  
5.  Selecione o objeto que tem um ícone de erro vermelho.  
  
6.  No painel direito, selecione o **relatório** guia.  
  
7.  Na parte superior do **relatório** guia é uma lista suspensa. Se a lista mostra **estatísticas**, altere a seleção do **fonte**.  
  
    O SSMA exibirá o código-fonte e vários botões imediatamente acima do código.  
  
8.  Selecione **próximo problema**, um ícone de erro vermelho com uma seta apontando para a direita.  
  
    SSMA para SAP ASE realçará o código-fonte problemático primeiro localiza no objeto atual.  
  
Para cada item que não puderam ser convertido, você deve determinar o que você deseja fazer com esse objeto:  
  
-   Você pode editar o código-fonte para procedimentos e gatilhos no **SQL** guia.  
  
-   Você pode alterar o objeto SAP ASE para remover ou revisar código problemática. Para carregar o código atualizado no SSMA, você precisa atualizar os metadados. Para obter mais informações, consulte [conectar-se ao SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md).  
  
-   Você pode excluir o objeto de migração. Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou Gerenciador de metadados do SQL Azure e o Gerenciador de metadados do Sybase, desmarque a caixa de seleção ao lado do item antes de carregar os objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure e migração de dados do SAP ASE.  
  
## <a name="next-steps"></a>Próximas etapas  
A próxima etapa no processo de migração é [carregar objetos de banco de dados convertidos para o SQL Server / SQL Azure (SybaseToSQL)](http://msdn.microsoft.com/en-us/4c59256f-99a8-4351-9559-a455813dbd06).  
  
## <a name="see-also"></a>Consulte também  
[Migrando SAP ASE bancos de dados do SQL Server - banco de dados SQL do Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
