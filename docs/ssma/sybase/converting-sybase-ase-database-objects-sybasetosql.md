---
title: Convertendo objetos de banco de dados do SybaseToSQL (Sybase ASE) | Microsoft Docs
ms.custom: ''
ms.date: 12/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Converting Database Objects
ms.assetid: 509cb65d-2f54-427a-83d7-37919cc4e3e3
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: f52700e0b85c2630d30c7ffe32193cbd96ce9d1e
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87932277"
---
# <a name="converting-sap-ase-database-objects-sybasetosql"></a>Convertendo objetos de banco de dados SAP ASE (SybaseToSQL)
Depois de ter se conectado ao SAP Adaptive Server Enterprise (ASE), conectado ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou ao SQL do Azure e defina as opções de projeto e mapeamento de dados, você pode converter objetos de banco de dado do SAP Adaptive Server Enterprise (ase) em objetos de banco [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do dados SQL do Azure.  
  
## <a name="the-conversion-process"></a>O processo de conversão  
A conversão de objetos de banco de dados usa as definições de objeto do ASE, converte-os em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos semelhantes ou SQL Azure e, em seguida, carrega essas informações nos metadados do SSMA. Ele não carrega as informações na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL do Azure. Você pode exibir os objetos e suas propriedades usando o ou o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados do SQL do Azure.
  
Durante a conversão, o SSMA imprime as mensagens de saída no painel de saída e as mensagens de erro no painel de **lista de erros** . Use as informações de saída e erro para determinar se você precisa modificar seus bancos de dados ASE ou seu processo de conversão para obter os resultados de conversão desejados.  
  
## <a name="setting-conversion-options"></a>Configurando opções de conversão  
Antes de converter objetos, examine as opções de conversão do projeto na caixa de diálogo **configurações do projeto** . Usando essa caixa de diálogo, você pode definir como o SSMA converte funções e variáveis globais. Para obter mais informações, consulte [configurações do projeto &#40;conversão&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md).  
  
## <a name="converting-ase-database-objects"></a>Convertendo objetos de banco de dados do ASE  
Para converter objetos de banco de dados do ASE, primeiro selecione os objetos que você deseja converter e, em seguida, faça com que o SSMA execute a conversão. Para exibir mensagens de saída durante a conversão, no menu **Exibir** , selecione **saída**.  
  
**Para converter objetos do ASE em sintaxe SQL Server ou SQL Azure**  
  
1.  No Gerenciador de metadados do Sybase, expanda o servidor ASE e, em seguida, expanda **bancos de dados**.  
  
2.  Selecione os objetos a serem convertidos:  
  
    -   Para converter todos os bancos de dados, marque a caixa de seleção ao lado de **bancos de dados**.  
  
    -   Para converter ou omitir um banco de dados, marque ou desmarque a caixa de seleção ao lado do nome do banco de dados.  
  
    -   Para converter ou omitir esquemas individuais, expanda o banco de dados, expanda **esquemas**e marque ou desmarque a caixa de seleção ao lado do esquema.  
  
    -   Para converter ou omitir uma categoria de objetos, expanda o esquema e marque ou desmarque a caixa de seleção ao lado da categoria.  
  
    -   Para converter ou omitir objetos individuais, expanda a pasta categoria e marque ou desmarque a caixa de seleção ao lado do objeto.  
  
3.  Para converter todos os objetos selecionados, clique com o botão direito do mouse em **bancos de dados**e selecione **converter esquema**.  
  
    Você também pode converter objetos individuais ou categorias de objetos clicando com o botão direito do mouse no objeto ou na pasta que o contém e, em seguida, selecionando **converter esquema**.  
  
> [!NOTE]  
> Algumas das funções de sistema do SAP ASE não correspondem exatamente ao equivalente SQL Server funções do sistema no comportamento. Para emular o comportamento do SAP ASE, o SSMA gera funções definidas pelo usuário no banco de dados SQL Server convertido em um esquema chamado ' s 2SS '. Dependendo das configurações do projeto, algumas das funções do sistema SQL Server são substituídas por essas funções emuladas. O SSMA cria as seguintes funções definidas pelo usuário:  

:::row:::
    :::column:::
        **char_length_nvarchar**  
        **char_length_varchar**  
        **charindex_nvarchar**  
        **charindex_varchar**  
        **hextoint**  
        **index_colorder**  
    :::column-end:::
    :::column:::
        **inttohex**  
        **ssma_current_time**  
        **ssma_datediff**  
        **ssma_datepart**  
        **substring_nvarchar**  
        **substring_varbinary**  
    :::column-end:::
    :::column:::
        **substring_varchar**  
        **to_unichar**  
        **uhighsurr**  
        **ulowsurr**  
    :::column-end:::
:::row-end:::

## <a name="objects-not-supported-in-azure-sql"></a>Objetos sem suporte no SQL do Azure  
As seguintes palavras-chave do T-SQL são usadas pelo SSMA para SAP ASE durante a conversão para SQL Server local, mas não há suporte para essas palavras-chave SQL Azure sintaxe T-SQL:  

:::row:::
    :::column:::
        CHECKPOINT  
        CREATE/ALTER/DROP DEFAULT  
        CREATE/DROP RULE  
        DBCC TRACEOFF  
        DBCC TRACEON  
    :::column-end:::
    :::column:::
        GRANT/REVOKE/DENY ALL  
        KILL  
        READTEXT  
        SELECT INTO  
        SET OFFSETS  
    :::column-end:::
    :::column:::
        SETUSER  
        SHUTDOWN  
        WRITETEXT  
    :::column-end:::
:::row-end:::

## <a name="viewing-conversion-problems"></a>Exibindo problemas de conversão  
Alguns objetos do SAP ASE podem não ser convertidos. Você pode determinar as taxas de êxito da conversão exibindo o relatório de conversão de resumo.  
  
**Para exibir um relatório de resumo**  
  
1.  No Gerenciador de metadados do Sybase, selecione **bancos de dados**.  
  
2.  No painel direito, selecione a guia **relatório** .  
  
    Este relatório mostra o relatório de avaliação de resumo para todos os objetos de banco de dados que foram avaliados ou convertidos. Você também pode exibir um relatório de resumo para objetos individuais:  
  
    -   Para exibir o relatório de um banco de dados individual, selecione o banco de dados no Gerenciador de metadados do Sybase.  
  
    -   Para exibir o relatório de um objeto de banco de dados individual, selecione o objeto no Gerenciador de metadados do Sybase. Objetos que têm problemas de conversão têm um ícone de erro vermelho.  
  
Para objetos que falharam na conversão, você pode exibir a sintaxe que resultou na falha de conversão.  
  
**Para exibir problemas de conversão individuais**  
  
1.  No Gerenciador de metadados do Sybase, expanda **bancos de dados**.  
  
2.  Expanda o banco de dados que mostra um ícone de erro vermelho.  
  
3.  Expanda a pasta **esquemas** e, em seguida, expanda o esquema que mostra um ícone de erro vermelho.  
  
4.  No esquema, expanda uma pasta que tem um ícone de erro vermelho.  
  
5.  Selecione o objeto que tem um ícone de erro vermelho.  
  
6.  No painel direito, selecione a guia **relatório** .  
  
7.  Na parte superior da guia **relatório** está uma lista suspensa. Se a lista Mostrar **estatísticas**, altere a seleção para **origem**.  
  
    O SSMA exibirá o código-fonte e vários botões imediatamente acima do código.  
  
8.  Selecione **próximo problema**, um ícone de erro vermelho com uma seta apontando para a direita.  
  
    O SSMA para SAP ASE destacará o primeiro código-fonte problemático encontrado no objeto atual.  
  
Para cada item que não pôde ser convertido, você precisa determinar o que deseja fazer com esse objeto:  
  
-   Você pode editar o código-fonte para procedimentos e gatilhos na guia **SQL** .  
  
-   Você pode alterar o objeto do SAP ASE para remover ou revisar o código problemático. Para carregar o código atualizado no SSMA, você precisa atualizar os metadados. Para obter mais informações, consulte [conectando-se ao SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md).  
  
-   Você pode excluir o objeto da migração. No ou no Gerenciador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadados do SQL do Azure e no Gerenciador de metadados Sybase, desmarque a caixa de seleção ao lado do item antes de carregar os objetos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL do Azure e migrar dados do SAP ASE.  
  
## <a name="next-steps"></a>Próximas etapas  
A próxima etapa no processo de migração é [carregar objetos de banco de dados convertidos em SQL Server/SQL Azure (SybaseToSQL)](https://msdn.microsoft.com/4c59256f-99a8-4351-9559-a455813dbd06).  
  
## <a name="see-also"></a>Consulte também  
[Migrar bancos de dados do SAP ASE para o SQL Server-Azure SQL Database &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
