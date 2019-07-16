---
title: Converter objetos de banco de dados ASE Sybase (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Converting Database Objects
ms.assetid: 509cb65d-2f54-427a-83d7-37919cc4e3e3
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 507ac2a61043260435a18c90fb473130988e7f35
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67948513"
---
# <a name="converting-sap-ase-database-objects-sybasetosql"></a>Converter objetos de banco de dados do SAP ASE (SybaseToSQL)
Depois de se conectar ao SAP Adaptive Server Enterprise (ASE), conectado ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL do Azure e defina o projeto e as opções de mapeamento de dados, você pode converter objetos de banco de dados do SAP Adaptive Server Enterprise (ASE) para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou banco de dados SQL do Azure objetos.  
  
## <a name="the-conversion-process"></a>O processo de conversão  
Converter objetos de banco de dados usa as definições de objeto do ASE, converte-os em semelhante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure objetos e, em seguida, carrega essas informações nos metadados SSMA. Não carrega as informações para a instância da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o SQL Azure. Em seguida, você pode exibir os objetos e suas propriedades usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou Gerenciador de metadados do SQL Azure.
  
Durante a conversão, o SSMA imprime mensagens de saída para mensagens de erro e o painel de saída para o **Error List** painel. Use as informações de erro e de saída para determinar se é preciso modificar seus bancos de dados do ASE ou de seu processo de conversão para obter os resultados da conversão desejada.  
  
## <a name="setting-conversion-options"></a>Definindo opções de conversão  
Antes de converter objetos, examine as opções de conversão de projeto na **configurações do projeto** caixa de diálogo. Usando essa caixa de diálogo, você pode definir como o SSMA converte funções e variáveis globais. Para obter mais informações, consulte [configurações do projeto &#40;conversão&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md).  
  
## <a name="converting-ase-database-objects"></a>Converter objetos de banco de dados do ASE  
Para converter objetos de banco de dados do ASE, primeiro selecione os objetos que você deseja converter e, em seguida, ter o SSMA realizar a conversão. Para exibir mensagens de saída durante a conversão na **modo de exibição** menu, selecione **saída**.  
  
**Para converter objetos de ASE a sintaxe do SQL Server ou SQL Azure**  
  
1.  No Gerenciador de metadados do Sybase, expanda o servidor do ASE e, em seguida, expanda **bancos de dados**.  
  
2.  Selecione objetos a ser convertida:  
  
    -   Para converter todos os bancos de dados, selecione a caixa de seleção ao lado **bancos de dados**.  
  
    -   Para converter ou omitir um banco de dados, marque ou desmarque a caixa de seleção ao lado do nome do banco de dados.  
  
    -   Para converter ou omitir esquemas individuais, expanda o banco de dados, expanda **esquemas**e, em seguida, selecione ou desmarque a caixa de seleção ao lado do esquema.  
  
    -   Para converter ou omitir uma categoria de objetos, expanda o esquema, selecione ou desmarque a caixa de seleção ao lado da categoria.  
  
    -   Para converter ou omitir os objetos individuais, expanda a pasta de categoria e, em seguida, selecione ou desmarque a caixa de seleção ao lado do objeto.  
  
3.  Para converter todos os objetos selecionados, clique com botão direito **bancos de dados**e, em seguida, selecione **converter esquema**.  
  
    Você também pode converter objetos individuais ou as categorias de objetos, clicando duas vezes o objeto ou a pasta recipiente e, em seguida, selecionando **converter esquema**.  
  
> [!NOTE]  
> Algumas das funções de sistema do SAP ASE não correspondem exatamente as funções do sistema do SQL Server equivalentes no comportamento. Para emular o comportamento do SAP ASE, o SSMA gera funções definidas pelo usuário no banco de dados do SQL Server convertido em um esquema chamado 's2ss'. Dependendo das configurações de projeto, algumas das funções de sistema do SQL Server são substituídas por essas funções emuladas. O SSMA cria as seguintes funções definidas pelo usuário:  
  
||||  
|-|-|-|  
|**char_length_nvarchar**|**index_colorder**|**ssma_datepart**|  
|**char_length_varchar**|**inttohex**|**substring_nvarchar**|  
|**charindex_nvarchar**|**ssma_datediff**|**substring_varbinary**|  
|**charindex_varchar**|**hextoint**|**substring_varchar**|  
|**ulowsurr**|**to_unichar**|**ssma_current_time**|  
|**uhighsurr**|||  
  
## <a name="objects-not-supported-in-azure-sql"></a>Objetos sem suporte no SQL Azure  
As seguintes palavras-chave do T-SQL são usadas pelo SSMA para SAP ASE durante a conversão para o SQL Server local, mas essas palavras-chave não é compatíveis com a sintaxe do T-SQL do SQL Azure:  
  
||||  
|-|-|-|  
|CHECKPOINT|CREATE/ALTER/DROP DEFAULT|CREATE/DROP RULE|  
|DBCC TRACEOFF|DBCC TRACEON|GRANT/REVOKE/DENY ALL|  
|KILL|READTEXT|SELECT INTO|  
|SET OFFSETS|SETUSER|SHUTDOWN|  
|WRITETEXT|||  
  
## <a name="viewing-conversion-problems"></a>Problemas de conversão de exibição  
Alguns objetos do SAP ASE não poderá ser convertida. Você pode determinar as taxas de sucesso de conversão, exibindo o relatório de resumo de conversão.  
  
**Para exibir um relatório de resumo**  
  
1.  No Gerenciador de metadados do Sybase, selecione **bancos de dados**.  
  
2.  No painel direito, selecione a **relatório** guia.  
  
    Este relatório mostra o relatório de resumo de avaliação para todos os objetos de banco de dados que foram avaliados ou convertidos. Você também pode exibir um relatório de resumo para objetos individuais:  
  
    -   Para exibir o relatório para um banco de dados individual, selecione o banco de dados no Gerenciador de metadados do Sybase.  
  
    -   Para exibir o relatório para um objeto de banco de dados individual, selecione o objeto no Gerenciador de metadados do Sybase. Objetos que têm problemas de conversão têm um ícone vermelho de erro.  
  
Para objetos que falha na conversão, você pode exibir a sintaxe que resultou em falha de conversão.  
  
**Para exibir os problemas de conversão individuais**  
  
1.  No Gerenciador de metadados do Sybase, expanda **bancos de dados**.  
  
2.  Expanda o banco de dados que mostra um ícone vermelho de erro.  
  
3.  Expanda o **esquemas** pasta e, em seguida, expanda o esquema que mostra um ícone vermelho de erro.  
  
4.  Sob o esquema, expanda uma pasta que tem um ícone vermelho de erro.  
  
5.  Selecione o objeto que tem um ícone vermelho de erro.  
  
6.  No painel direito, selecione a **relatório** guia.  
  
7.  Na parte superior do **relatório** guia é uma lista suspensa. Se a lista mostra **estatísticas**, altere a seleção **origem**.  
  
    O SSMA exibirá o código-fonte e vários botões imediatamente acima do código.  
  
8.  Selecione **próximo problema**, um ícone vermelho de erro com uma seta apontando para a direita.  
  
    O SSMA para SAP ASE realçará o código-fonte problemático primeiro que ele localiza no objeto atual.  
  
Para cada item que não pôde ser convertido, você deve determinar o que você deseja fazer com esse objeto:  
  
-   Você pode editar o código-fonte para os procedimentos e gatilhos na **SQL** guia.  
  
-   Você pode alterar o objeto de SAP ASE para remover ou revisar o código problemático. Para carregar o código atualizado no SSMA, você precisa atualizar os metadados. Para obter mais informações, consulte [conectar-se ao SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md).  
  
-   Você pode excluir o objeto da migração. Na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o Gerenciador de metadados do SQL Azure e o Gerenciador de metadados do Sybase, desmarque a caixa de seleção próxima ao item antes de carregar os objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL do Azure e a migração de dados do SAP ASE.  
  
## <a name="next-steps"></a>Próximas etapas  
É a próxima etapa no processo de migração [Carregando objetos de banco de dados convertidos no SQL Server / SQL Azure (SybaseToSQL)](https://msdn.microsoft.com/4c59256f-99a8-4351-9559-a455813dbd06).  
  
## <a name="see-also"></a>Confira também  
[Migrando SAP ASE bancos de dados SQL Server - banco de dados SQL do Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
